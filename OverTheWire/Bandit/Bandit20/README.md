# Bandit Level 20 → Level 21

## Level Goal
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

## Commands you may need to solve this level
ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

## Solution

```                                                                                 
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit20@bandit.labs.overthewire.org 
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit20@bandit.labs.overthewire.org's password: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

Linux bandit.otw.local 5.4.8 x86_64 GNU/Linux
```
      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org
```

Welcome to OverTheWire!

If you find any problems, please report them to Steven or morla on
irc.overthewire.org.

--[ Playing the games ]--

  This machine might hold several wargames.
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.

  Write-access to homedirectories is disabled. It is advised to create a
  working directory with a hard-to-guess name in /tmp/.  You can use the
  command "mktemp -d" in order to generate a random and hard to guess
  directory in /tmp/.  Read-access to both /tmp/ and /proc/ is disabled
  so that users can not snoop on eachother. Files and directories with
  easily guessable or short names will be periodically deleted!

  Please play nice:

    * don't leave orphan processes running
    * don't leave exploit-files laying around
    * don't annoy other players
    * don't post passwords or spoilers
    * again, DONT POST SPOILERS!
      This includes writeups of your solution on your blog or website!

--[ Tips ]--

  This machine has a 64bit processor and many security-features enabled
  by default, although ASLR has been switched off.  The following
  compiler flags might be interesting:

    -m32                    compile for 32bit
    -fno-stack-protector    disable ProPolice
    -Wl,-z,norelro          disable relro

  In addition, the execstack tool can be used to flag the stack as
  executable on ELF binaries.

  Finally, network-access is limited for most levels by a local
  firewall.

--[ Tools ]--

 For your convenience we have installed a few usefull tools which you can find
 in the following locations:

    * gef (https://github.com/hugsy/gef) in /usr/local/gef/
    * pwndbg (https://github.com/pwndbg/pwndbg) in /usr/local/pwndbg/
    * peda (https://github.com/longld/peda.git) in /usr/local/peda/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /usr/local/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)
    * checksec.sh (http://www.trapkit.de/tools/checksec.html) in /usr/local/bin/checksec.sh

--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us through IRC on
  irc.overthewire.org #wargames.

  Enjoy your stay!
  
```
bandit20@bandit:~$ ls -l
total 12
-rwsr-x--- 1 bandit21 bandit20 12088 May  7  2020 suconnect                   #suconnect has setuid permission (the s bit in the user permission class)

bandit20@bandit:~$ file suconnect                                             #to know the file type
suconnect: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=74c0f6dc184e0412b6dc52e542782f43807268e1, not stripped

bandit20@bandit:~$ ./suconnect                                                #since it is an executable file, just execute it
Usage: ./suconnect <portnumber>                                               #the usage format of this file can be seen here 
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.

bandit20@bandit:~$ nmap localhost                                             #to check for the ports that are in use

Starting Nmap 7.40 ( https://nmap.org ) at 2022-02-10 06:22 CET
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00022s latency).
Not shown: 997 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
113/tcp   open  ident
30000/tcp open  ndmps

Nmap done: 1 IP address (1 host up) scanned in 0.09 seconds
```


### Note: 
Use a port that is not in session. The ports obtained from nmap are currently in use. So use any port other than that listed by nmap. <br/> 
I consider port number 1111 (a random port that is not in use). <br/> 
Now netcat is used to transmit and listen to the password. When the current level password is transmitted, the next level password will be received. <br/> 
Consider the current terminal as terminal1 and open another terminal - terminal2. In the terminal2, log in to bandit20 as done with terminal1. <br/> 
Terminal1 will be used as netcat listener. <br/> 
Terminal2 will be used by suconnect to receive the input current level password by terminal1, and transmit the next level password back to terminal1. <br/> 
Connect both netcat and suconnect to the port 1111. <br/> 

```
#Terminal1                                                    | #Terminal2
                                                              |
bandit20@bandit:~$ nc -lp 1111                                | bandit20@bandit:~$ ./suconnect 1111
GbKksEFF4yrVs6il55v6gwY5aVje5f0j   #current level password    | Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr   #next level password       | Password matches, sending next password
                                                              |
bandit20@bandit:~$ exit                                       | bandit20@bandit:~$ exit
logout                                                        | logout
Connection to bandit.labs.overthewire.org closed.             | Connection to bandit.labs.overthewire.org closed.     

```

#### Command-line help text
```
ssh              -> OpenSSH SSH client (remote login program)
cat              -> Concatenate files & print on the stdout
bash             -> GNU Bourne-Again Shell
screen           -> Screen manager with terminal emulation
tmux             -> Terminal multiplexer
Unix job control -> Unix job control command list

nc               -> netcat; TCP/IP swiss army knife
-l               -> To specify that nc should listen for an incoming connection rather than initiate a connection to a remote host.
-p <Port Number> -> Specifies the Port Number nc should use.
```
