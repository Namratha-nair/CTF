# Bandit Level 31 → Level 32

## Level Goal
There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo. The password for the user bandit31-git is the same as for the user bandit31.

Clone the repository and find the password for the next level.

## Commands you may need to solve this level
git

## Solution
Clone the repository means to create a copy of the repository.
```
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit31@bandit.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit31@bandit.labs.overthewire.org's password: 47e603bb428404d265f59c42920d81e5
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
bandit31@bandit:~$ mkdir /tmp/mybandit31                                                          #create a directory named mybandit31 in temp

bandit31@bandit:~$ cd /tmp/mybandit31                                                             #navigate to mybandit31 directory

bandit31@bandit:/tmp/mybandit31$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo    #create a copy of the given git repository using the clone command
Cloning into 'repo'...
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 47e603bb428404d265f59c42920d81e5                               #provide bandit31 password
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (4/4), done.

bandit31@bandit:/tmp/mybandit31$ ls                                                               #view the contents of mybandit28 directory
repo                                                                                              #a directory named repo is present

bandit31@bandit:/tmp/mybandit31$ cd repo                                                          #navigate to repo

bandit31@bandit:/tmp/mybandit31/repo$ ls                                                          #list the contents of repo
README.md                                                                                         #a file named README.md is present

bandit31@bandit:/tmp/mybandit31/repo$ cat README.md                                               #read the file README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master

                                                                                                  #do as stated in the READEME.md file
bandit31@bandit:/tmp/mybandit31/repo$ echo "May I come in?" > key.txt                             #create a file key.txt and insert "May I come in?" text in it

bandit31@bandit:/tmp/mybandit31/repo$ cat key.txt                                                 #verify the file
May I come in?

bandit31@bandit:/tmp/mybandit31/repo$ git add -f key.txt                                          #add key.txt & ignored files to the repository

bandit31@bandit:/tmp/mybandit31/repo$ git commit -m key.txt                                       #commit
[master 2f61bdd] key.txt
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
 
bandit31@bandit:/tmp/mybandit31/repo$ git push origin master                                      #push key.txt to master branch
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password: 47e603bb428404d265f59c42920d81e5                                 #provide the bandit31 password
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 318 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e                                                             #bandit32 password
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'

bandit31@bandit:/tmp/mybandit31/repo$ rm -rf /tmp/mybandit31                                          #delete the created mybandit31 directory

bandit31@bandit:/tmp/mybandit31/repo$ exit                                                            #logout of bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.

```

Command-line help text
```
git        -> A version control system to keep track of changes to files and projects over time 
git clone  -> Clone a repository into a new directory

git add    -> Add file contents to the index
-f         -> Allow adding otherwise ignored files

git commit -> Record changes to the repository
-m         -> Use the given <msg> as the commit message

git push   -> Update remote refs along with associated objects
ls         -> List directory contents
cat        -> Concatenate files and print on the standard output 
```
