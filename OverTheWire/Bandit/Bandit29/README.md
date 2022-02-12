# Bandit Level 29 → Level 30

## Level Goal
There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29.

Clone the repository and find the password for the next level.

## Commands you may need to solve this level
git

## Solution
Clone the repository means to create a copy of the repository.
```                                                                                
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit29@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit29@bandit.labs.overthewire.org's password: bbc96594b4e001778eee9975372716b2
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
bandit29@bandit:~$ mkdir /tmp/mybandit29                                                          #create a directory mybandit29 under temp

bandit29@bandit:~$ cd /tmp/mybandit29                                                             #navigate to mybandit29

bandit29@bandit:/tmp/mybandit29$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo    #create a copy of the given git repository using the clone command 
Cloning into 'repo'...
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password: bbc96594b4e001778eee9975372716b2                               #provide bandit29 password
remote: Counting objects: 16, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (16/16), 1.43 KiB | 0 bytes/s, done.
Resolving deltas: 100% (2/2), done.

bandit29@bandit:/tmp/mybandit29$ ls                                                               #view the contents of mybandit29 directory                                                               
repo                                                                                              #a directory named repo is present

bandit29@bandit:/tmp/mybandit29$ cd repo                                                          #navigate to repo

bandit29@bandit:/tmp/mybandit29/repo$ ls                                                          #list the contents of repo
README.md                                                                                         #a file named README.md is present

bandit29@bandit:/tmp/mybandit29/repo$ cat README.md                                               #read the file README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>

bandit29@bandit:/tmp/mybandit29/repo$ git branch -a                                               #view all the branches of this repo
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev                                                                              #let us view this branch
  remotes/origin/master
  remotes/origin/sploits-dev
  
bandit29@bandit:/tmp/mybandit29/repo$ git checkout dev                                            #navigate to the branch named as dev
Branch dev set up to track remote branch dev from origin.
Switched to a new branch 'dev'

bandit29@bandit:/tmp/mybandit29/repo$ ls                                                          #list the contents of this branch
code  README.md                                                                                   #a file named README.md is present

bandit29@bandit:/tmp/mybandit29/repo$ cat README.md                                               #read the file README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf                                                      #password for bandit30

bandit29@bandit:/tmp/mybandit29/repo$ rm -rf /tmp/bandit29                                        #delete the created mybandit29 directory

bandit29@bandit:/tmp/mybandit29/repo$ exit                                                        #logout from bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.
                                                   
```
#### Command-line help text
```
git           -> A version control system to keep track of changes to files and projects over time 
git clone     -> Clone a repository into a new directory
git branch    -> List, create, or delete branches
git checkout  -> Checkout a branch or paths to the working tree
ls            -> List directory contents
cat           -> Concatenate files and print on the standard output 
```
