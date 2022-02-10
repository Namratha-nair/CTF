# Bandit Level 22 → Level 23

## Level Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Commands you may need to solve this level
cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solution
Note:<br/>
Not all the commands given above are required.<br/>
<br/>
Cron is a time — based job scheduler in Unix or Unix-like computer operating systems. It schedules a command or script on your server to run automatically in the background, at a designated time and date.<br/>

```
                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit22@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit22@bandit.labs.overthewire.org's password: Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI 
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
bandit22@bandit:~$ ls /etc/cron.d/                                       #see the contents of the path given in the challenge
cronjob_bandit15_root  cronjob_bandit17_root  cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  cronjob_bandit25_root

bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23                      #since we want the password of bandit23, lets read cronjob_bandit23 file
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null              #@reboot -> run once after reboot
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null            # * * * * * -> run at every minute
                                                                         # the user bandit23 will run the command: /usr/bin/cronjob_bandit23.sh &> /dev/null

bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh                      #read the content of the file /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)                                                         #eventhough whoami in this level will produce bandit22, it is bandit23, as the cronjob is run by bandit23
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)            #so this command will be:  mytarget=$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget                            #the password is in the file /tmp/$mytarget


bandit22@bandit:~$ cat /tmp/$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)     #read the file in the path /tmp/$mytarget by substituting the value of mytarget as shown in the previous comment
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

bandit22@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
                                                   

```
#### Script explanation
```
The script seen in this level is as below:

mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

|       -> used in combining the 3 shell commands, to be executed in succession
$       -> to access the value stored in a variable
$myname = bandit23

md5sum  -> computes and checks 128-bit MD5 message digest or hashes
        -> used to verify that a file has not changed as a result of a faulty file transfer


Consider:
echo I am user $myname | md5sum

MD5 checksum is computed for the input string "I am user bandit23" and the output is 128–bit cryptographic hash.

bandit22@bandit:~$ echo I am user bandit23 | md5sum
8ca319486bfbbc3663ea0fbe81326349  -

Since the md5sum command returns a dash after the hash, to extract just the MD5 hash without the dash, cut command is used.

Cut command :
SYNTAX: cut -d -f filename.txt
Cut     -> Print selected parts of lines from each file to standard output.
-d      -> delimiter
-f      -> field

Here, in
8ca319486bfbbc3663ea0fbe81326349  -
the hash is field 1 and dash is field 2, seperated by delimiter space ' '.

So the command
cut -d ' ' -f 1
selects and displays only the 1st field of the line using the field delimiter: space ' '.
In this case, it  refers to 8ca319486bfbbc3663ea0fbe81326349.


Putting it all together, the command :
echo I am user bandit23 | md5sum | cut -d ‘ ‘ -f 1
will eventually return the MD5 hash: 8ca319486bfbbc3663ea0fbe81326349.

This output is then assigned to the variable mytarget via Command Substitution. This is the name of file in tmp directory.


Finally, cat /etc/bandit_pass/$myname > /tmp/$mytarget will redirects the bandit23‘s password to the 8ca319486bfbbc3663ea0fbe81326349 file, located in tmp. Here, $mytarget will access the value stored in variable mytarget and become the name of the file located in tmp directory.
    
```


#### Command-line help text
```
cron       -> Daemon to execute scheduled commands
crontab    -> Maintain crontab files for individual users
crontab(5) -> File formats
```

