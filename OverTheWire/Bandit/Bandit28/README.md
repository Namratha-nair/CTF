# Bandit Level 28 → Level 29

## Level Goal
There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28.

Clone the repository and find the password for the next level.

## Commands you may need to solve this level
git

## Solution
Clone the repository means to create a copy of the repository.
```                                                                               
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit28@bandit.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit28@bandit.labs.overthewire.org's password: 0ef186ac70e04ea33b4c1853d2526fa2
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
bandit28@bandit:~$ mkdir /tmp/mybandit28                                                          #create a directory mybandit28 under temp

bandit28@bandit:~$ cd /tmp/mybandit28                                                             #navigate to mybandit28 directory

bandit28@bandit:/tmp/mybandit28$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo    #create a copy of the given git repository using the clone command 
Cloning into 'repo'...
Could not create directory '/home/bandit28/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit28/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit28-git@localhost's password: 0ef186ac70e04ea33b4c1853d2526fa2                               #provide bandit28 password
remote: Counting objects: 9, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done. 

bandit28@bandit:/tmp/mybandit28$ ls                                                               #view the contents of bandit28 directory
repo                                                                                              #a directory named repo is present

bandit28@bandit:/tmp/mybandit28$ cd repo                                                          #navigate to repo

bandit28@bandit:/tmp/mybandit28/repo$ ls                                                          #list the contents of repo
README.md                                                                                         #a file named README.md is present

bandit28@bandit:/tmp/mybandit28/repo$ cat README.md                                               #read te file README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx                                                                            #the password is made to be not visible
                                                                                                  #check the git log to study the history of the repository

bandit28@bandit:/tmp/mybandit28/repo$ git log
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak                                                                                 #view this activity using 'git show' to its commit id 

commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data

commit de2ebe2d5fd1598cd547f4d56247e053be3fdc38
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    initial commit of README.md


bandit28@bandit:/tmp/mybandit28/repo$ git show edd935d60906b33f0619605abd1689808ccdd5ee           #to view more about the 'fix info leak' commit
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak

diff --git a/README.md b/README.md
index 3f7cee8..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: bbc96594b4e001778eee9975372716b2                                                      #bandit29 password
+- password: xxxxxxxxxx

bandit28@bandit:/tmp/mybandit28/repo$ rm -rf /tmp/bandit28                                         #delete the created bandit28 directory

bandit28@bandit:/tmp/mybandit28/repo$ exit                                                         #logout from bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.

```
#### Command-line help text
```
git       -> A version control system to keep track of changes to files and projects over time 
git clone -> Clone a repository into a new directory
git log   -> Show commit logs
git show  -> Show various types of objects
ls        -> List directory contents
cat       -> Concatenate files and print on the standard output 
```
