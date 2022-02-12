# Bandit Level 30 → Level 31

## Level Goal
There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo. The password for the user bandit30-git is the same as for the user bandit30.

Clone the repository and find the password for the next level.

## Commands you may need to solve this level
git

## Solution
Clone the repository means to create a copy of the repository.
```                                                                                                                                                           
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit30@bandit.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
```
bandit30@bandit.labs.overthewire.org's password: 5b90576bedb2cc04c86a9e924ce42faf
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
bandit30@bandit:~$ mkdir /tmp/mybandit30                                                         #create a directory mybandit30 in temp

bandit30@bandit:~$ cd /tmp/mybandit30                                                            #navigate to mybandit30

bandit30@bandit:/tmp/mybandit30$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo   #create a copy of the given git repository using the clone command 
Cloning into 'repo'...
Could not create directory '/home/bandit30/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password: 5b90576bedb2cc04c86a9e924ce42faf                              #provide bandit30 password
remote: Counting objects: 4, done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (4/4), 298 bytes | 0 bytes/s, done.

bandit30@bandit:/tmp/mybandit30$ ls                                                             #view the contents of mybandit30 directory
repo                                                                                            #a directory named repo is present

bandit30@bandit:/tmp/mybandit30$ cd repo                                                        #navigate to repo

bandit30@bandit:/tmp/mybandit30/repo$ ls                                                        #list the contents of repo
README.md                                                                                       #a file named README.md is present

bandit30@bandit:/tmp/mybandit30/repo$ cat README.md                                             #read the file README.md
just an epmty file... muahaha
                                                                                                #git tag is a bookmarks pointing to a specific commit
bandit30@bandit:/tmp/mybandit30/repo$ git tag                                                   #check for it tags
secret                                                                                          #git tag named as secret is present

bandit30@bandit:/tmp/mybandit30/repo$ git show secret                                           #view the git tag named secret
47e603bb428404d265f59c42920d81e5

bandit30@bandit:/tmp/mybandit30/repo$ rm -rf /tmp/mybandit30                                    #delete the created mybandit30 directory 

bandit30@bandit:/tmp/mybandit30/repo$ exit                                                      #logout from bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.

```
#### Command-line help text
```
git           -> A version control system to keep track of changes to files and projects over time 
git clone     -> Clone a repository into a new directory
git show      -> Show various types of objects
git tag       -> Create, list, delete or verify a tag object signed with GPG
ls            -> List directory contents
cat           -> Concatenate files and print on the standard output 
```
