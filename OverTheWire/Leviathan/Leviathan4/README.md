# Leviathan Level 4 → Level 5
There is no information for this level, intentionally.

## Solution
```                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ ssh -p 2223 leviathan4@leviathan.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
leviathan4@leviathan.labs.overthewire.org's password: vuH0coox6m
```
Linux leviathan 4.18.12 x86_64 GNU/Linux
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
leviathan4@leviathan:~$ ls -al                                        #list the contents of the homedirectory of leviathan4
total 24
drwxr-xr-x  3 root root       4096 Aug 26  2019 .
drwxr-xr-x 10 root root       4096 Aug 26  2019 ..
-rw-r--r--  1 root root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root root       3526 May 15  2017 .bashrc
-rw-r--r--  1 root root        675 May 15  2017 .profile
dr-xr-x---  2 root leviathan4 4096 Aug 26  2019 .trash                 #there is a hidden directory

leviathan4@leviathan:~$ cd .trash                                      #navigate to the hidden directory named as trash

leviathan4@leviathan:~/.trash$ ls -al                                  #list the contents of the hidden directory trash
total 16
dr-xr-x--- 2 root       leviathan4 4096 Aug 26  2019 .
drwxr-xr-x 3 root       root       4096 Aug 26  2019 ..
-r-sr-x--- 1 leviathan5 leviathan4 7352 Aug 26  2019 bin                #there is a setuid file named as bin

leviathan4@leviathan:~/.trash$ ./bin                                    #execute the bin file
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010     #convert this binary data into ASCII format which gives Tith4cokei as the answer
                                                                         #this is the password for leviathan5
leviathan4@leviathan:~/.trash$ exit                                      #logout of leviathan.labs.overthewire.org
logout
Connection to leviathan.labs.overthewire.org closed.
```

### Command-line help text
```
ls      -> list directory contents
-a      -> do not ignore entries starting with .
-l      -> use a long listing format

cd      -> change directory
```
