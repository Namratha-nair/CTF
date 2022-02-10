# Bandit Level 11 → Level 12

## Level Goal
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Solution
Note:
Not all the commands given above is required.
```                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit11@bandit.labs.overthewire.org
```
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit11@bandit.labs.overthewire.org's password: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
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
bandit11@bandit:~$ ls
data.txt

bandit11@bandit:~$ file data.txt
data.txt: ASCII text

bandit11@bandit:~$ cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

bandit11@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

#### Command-line help text

> grep    -> Print lines matching a pattern <br/>
> sort    -> Sort lines of text files <br/>
> uniq    -> Report or omit repeated lines <br/>
> strings -> Print the strings of printable characters in files <br/>
> base64  -> base64 encode/decode data and print to standard output <br/>
> tr      -> Translate or delete characters <br/>
> tar     -> The GNU version of the tar archiving utility <br/>
> gzip    -> Compress or expand files <br/>
> bzip2   -> A block-sorting file compressor, v1.0.6 <br/>
> xxd     -> Make a hexdump or do the reverse <br/>
> cat     -> concatenate files and print on the standard output <br/>
> |       -> A  pipeline is a sequence of one or more commands separated by one of the control operators | or |&. <br/>
 
#### Note
```
The letters in the data.txt file is rotated by 13 letters. So A will be N, B will be Q and so on. 
Similarly for the lower-case letters. 

A B C D E F G H I J K L M 
| | | | | | | | | | | | | 
N O P Q R S T U V W X Y Z 

With tr command, the letters to be mapped must be provided. 
i.e, A-Z will be mapped to N-Z along with A-M (A is mapped to N; Z is mapped to M).
Upper case: Map from A-Z to N-ZA-M. 

Similarly, a-z will be mapped to n-z and a-m (a is mapped to n; z is mapped to m). 
Lower case: Map from a-z to n-za-m. 

In the expression form, it can be given as 
tr "A-Za-z" "N-ZA-Mn-za-m" 
```


