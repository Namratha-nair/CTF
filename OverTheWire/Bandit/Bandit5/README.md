# Bandit Level 5 → Level 6

## Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

## Commands you may need to solve this level
ls, cd, cat, file, du, find

## Solution

```
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit5@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit5@bandit.labs.overthewire.org's password: koReBOKuIDDepwhWk7jZC0RTdopnAYKh
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
bandit5@bandit:~$ ls
inhere

bandit5@bandit:~$ file ./inhere/*
./inhere/maybehere00: directory
./inhere/maybehere01: directory
./inhere/maybehere02: directory
./inhere/maybehere03: directory
./inhere/maybehere04: directory
./inhere/maybehere05: directory
./inhere/maybehere06: directory
./inhere/maybehere07: directory
./inhere/maybehere08: directory
./inhere/maybehere09: directory
./inhere/maybehere10: directory
./inhere/maybehere11: directory
./inhere/maybehere12: directory
./inhere/maybehere13: directory
./inhere/maybehere14: directory
./inhere/maybehere15: directory
./inhere/maybehere16: directory
./inhere/maybehere17: directory
./inhere/maybehere18: directory
./inhere/maybehere19: directory

bandit5@bandit:~$ find . -type f -readable ! -executable -size 1033c            
./inhere/maybehere07/.file2

bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7

bandit5@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```
#### Command-line help text
> . or ./         -> Refer to the Current Working Directory. <br/>
> -type f         -> File is of type : regular file   <br/>
> -readable       -> Matches files which are readable. <br/>
> -executable     -> Matches  files which are executable & directories which are searchable <br/>
> ! -executable   -> Matches  files which are not executable & directories which are not searchable <br/>
> -size 1033c     -> File uses 1033 units of space. c refer to bytes. <br/>

