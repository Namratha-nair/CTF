# Bandit Level 27 → Level 28

## Level Goal
There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27.

Clone the repository and find the password for the next level.

## Commands you may need to solve this level
git

## Solution
Clone the repository means to create a copy of the repository.
```                                                                                                                                                                    
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit27@bandit.labs.overthewire.org     
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
```
bandit27@bandit.labs.overthewire.org's password: 3ba3118a22e93127a4ed485be72ef5ea 
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
bandit27@bandit:~$ mkdir /tmp/mybandit27                                                             #create a directory under temp as mybandit27       

bandit27@bandit:~$ cd /tmp/mybandit27                                                                #navigate to mybandit27

bandit27@bandit:/tmp/mybandit27$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo       #create a copy of the given git repository using the clone command
Cloning into 'repo'...
Could not create directory '/home/bandit27/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit27/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit27-git@localhost's password: 3ba3118a22e93127a4ed485be72ef5ea                                   #provide bandit27 password
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done. 

bandit27@bandit:/tmp/mybandit27$ ls                                                                   #see the contents of mybandit27 directory
repo                                                                                                  #there is a directory named as repo 

bandit27@bandit:/tmp/mybandit27$ cd repo                                                              #navigate to repo  

bandit27@bandit:/tmp/mybandit27/repo$ ls                                                              #list the contents of the current diectory
README                                                                                                #there is a file named as README

bandit27@bandit:/tmp/mybandit27/repo$ cat README                                                      #read the README file
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2                                   #the password for bandit28

bandit27@bandit:/tmp/mybandit27/repo$ rm -rf /tmp/mybandit27                                          #delete the created mybandit directory

bandit27@bandit:/tmp/mybandit27/repo$ exit                                                            #logout from bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.
                        
```

#### Command-line help text
```
git       -> A version control system to keep track of changes to files and projects over time 
git clone -> Clone a repository into a new directory
ls        -> List directory contents
cat       -> Concatenate files and print on the standard output 
```
