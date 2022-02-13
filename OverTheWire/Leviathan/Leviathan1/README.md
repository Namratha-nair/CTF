# Leviathan Level 1 → Level 2
There is no information for this level, intentionally.

## Solution

```                                                                                                                                                                       
┌──(kali㉿kali)-[~]
└─$ ssh -p 2223 leviathan1@leviathan.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
leviathan1@leviathan.labs.overthewire.org's password: rioGegei8m
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
leviathan1@leviathan:~$ ls -al                                                   #list the contents of the homedirectory of leviathan1
total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan2 leviathan1 7452 Aug 26  2019 check                      #there is a file named check with elevated permissions run by levianth2
-rw-r--r--  1 root       root        675 May 15  2017 .profile

leviathan1@leviathan:~$ file check                                               #see if it is executable
check: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=c735f6f3a3a94adcad8407cc0fda40496fd765dd, not stripped

leviathan1@leviathan:~$ ./check                                                   #since it is an executable file, just execute it     
password: rioGegei8m                                                              #providing leviathan1 password here 
Wrong password, Good Bye ...                                                      #states that it is wrong password
                                                                                  #we have to find the password 
                                                                                  #ltace intercepts every system call, function call and displays every parameter a function can take
                                                                                  
leviathan1@leviathan:~$ ltrace ./check                                            #perform ltrace with the setuid file named as check
__libc_start_main(0x804853b, 1, 0xffffd784, 0x8048610 <unfinished ...>            #press enter to view more response
printf("password: ")                                                                                   = 10
getchar(1, 0, 0x65766f6c, 0x646f6700password: 
)                                                                  = 10
getchar(1, 0, 0x65766f6c, 0x646f6700
)                                                                  = 10
getchar(1, 0, 0x65766f6c, 0x646f6700
)                                                                  = 10
strcmp("\n\n\n", "sex")                                                                                = -1    #there is strcmp, i.e, the password we input is compared with the word "sex"
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...                                                #therefore the password to execute the file check is "sex"
)                                                                   = 29
+++ exited (status 0) +++


leviathan1@leviathan:~$ ./check                                                   #try executing this file again
password: sex                                                                     #enter the password

$ cat /etc/leviathan_pass/leviathan2                                              #we have gained acces; now read the password file
ougahZi8Ta                                                                        #leviathan2 password

$ exit                                                                            #exit

leviathan1@leviathan:~$ exit                                                      #logout from leviathan.labs.overthewire.org
logout
Connection to leviathan.labs.overthewire.org closed.
                            
```
#### Command-line help text
```
ls      -> list directory contents
-a      -> do not ignore entries starting with .
-l      -> use a long listing format

cat     -> concatenate files and print on the standard output
ltrace  -> A library call tracer
```
