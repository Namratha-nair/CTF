# Bandit Level 12 → Level 13

## Level Goal
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Commands you may need to solve this level
grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

## Solution

```
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit12@bandit.labs.overthewire.org
```

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

```
bandit12@bandit.labs.overthewire.org's password: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu 
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
bandit12@bandit:~$ ls                                                #to see the available files in home directory
data.txt

bandit12@bandit:~$ mkdir /tmp/mybandit12                             #make a directory mybandit12 inside the directory temp

bandit12@bandit:~$ cp data.txt /tmp/mybandit12                       #copy the file data.txt into the directory mybandit12

bandit12@bandit:~$ cd /tmp/mybandit12                                #change the current directory into mybandit12       

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data.txt

bandit12@bandit:/tmp/mybandit12$ file data.txt                       #to see the file-type of file data.txt
data.txt: ASCII text

bandit12@bandit:/tmp/mybandit12$ cat data.txt | xxd -r > data        #since it's given that its an hexdump file, perform reverse hex dump and store it in the file named as data
                                                                     # -r : reverse hexdump
                                                                     # > : redirects output; in this case into file named data

bandit12@bandit:/tmp/mybandit12$ file data                           #to see the file type of the file named data 
data: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/mybandit12$ mv data data2.gz                    #since it's a gzip file, rename the file data as data2.gz

bandit12@bandit:/tmp/mybandit12$ gzip -d data2.gz                    #perform gzip decompression on data2.gz
                                                                     # -d : decompress

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data2  data.txt

bandit12@bandit:/tmp/mybandit12$ file data2                          #to check the file-type of file data2
data2: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/mybandit12$ mv data2 data3.bz                   #since it's a bzip file, rename the file data2 as data3.bz

bandit12@bandit:/tmp/mybandit12$ bzip2 -d data3.bz                   #perform bzip decompression on data3.bz
                                                                     # -d : decompress

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data3  data.txt

bandit12@bandit:/tmp/mybandit12$ file data3                          #to check the file-type of file data3
data3: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/mybandit12$ mv data3 data4.gz                   #since it's a gzip file, rename the file data3 as data4.gz

bandit12@bandit:/tmp/mybandit12$ gzip -d data4.gz                    #perform gzip decompression on data4.gz
                                                                     # -d : decompress

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data4  data.txt

bandit12@bandit:/tmp/mybandit12$ file data4                          #to see the file-type of file data4
data4: POSIX tar archive (GNU)

bandit12@bandit:/tmp/mybandit12$ mv data4 data5.tar                  #since it's a tar file, rename the file data4 as data5.tar

bandit12@bandit:/tmp/mybandit12$ tar -xf data5.tar                   #perform tar decompression on data5.tar
                                                                     # -x : extract file
                                                                     # -f : use archive file

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data5.bin  data5.tar  data.txt

bandit12@bandit:/tmp/mybandit12$ file data5.bin                      #to see the file-type of file data5.bin
data5.bin: POSIX tar archive (GNU)

bandit12@bandit:/tmp/mybandit12$ mv data5.bin data6.tar              #since it's a tar file, rename the file data5.bin as data6.tar

bandit12@bandit:/tmp/mybandit12$ tar -xf data6.tar                   #perform tar decompression on data6.tar
                                                                     # -x : extract file
                                                                     # -f : use archive file

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data5.tar  data6.bin  data6.tar  data.txt

bandit12@bandit:/tmp/mybandit12$ file data6.bin                      #to see the file-type of file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/mybandit12$ mv data6.bin data7.bz               #since it's a bzip file, rename the file data6.bin as data7.bz

bandit12@bandit:/tmp/mybandit12$ bzip2 -d data7.bz                   #perform bzip decompression on data7.bz
                                                                     # -d : decompress

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data5.tar  data6.tar  data7  data.txt

bandit12@bandit:/tmp/mybandit12$ file data7                          #to see the file-type of file data7
data7: POSIX tar archive (GNU)

bandit12@bandit:/tmp/mybandit12$ mv data7 data8.tar                  #since it's a tar file, rename the file data7 as data8.tar 

bandit12@bandit:/tmp/mybandit12$ tar -xf data8.tar                   #perform tar decompression on data8.tar 
                                                                     # -x : extract file
                                                                     # -f : use archive file

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data5.tar  data6.tar  data8.bin  data8.tar  data.txt

bandit12@bandit:/tmp/mybandit12$ file data8.bin                      #to see the file-type of file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/mybandit12$ mv data8.bin data9.gz               #since it's a gzip file, rename the file data8.bin as data9.gz

bandit12@bandit:/tmp/mybandit12$ gzip -d data9.gz                    #perform gzip decompression on data9.gz
                                                                     # -d : decompress

bandit12@bandit:/tmp/mybandit12$ ls                                  #to see the available files in mybandit12 directory
data5.tar  data6.tar  data8.tar  data9  data.txt

bandit12@bandit:/tmp/mybandit12$ file data9                          #to see the file-type of file data9
data9: ASCII text

bandit12@bandit:/tmp/mybandit12$ cat data9                           #to display the contents of file data9
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

bandit12@bandit:/tmp/mybandit12$ cd ~                                #to go to the home directory

bandit12@bandit:~$ rm -rf /tmp/mybandit12                            #to delete the created mybandit12 directory

bandit12@bandit:/tmp/mybandit12$ exit                                #to exit from bandit.labs.overthewire.org
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
> mkdir  -> Make directories <br/>
> cp      -> Copy files and directories <br/>
> mv      -> Move (rename) files <br/>
> file    -> determine file type <br/>

#### Note:

> Check the file type and rename the file extension with respect to the file type.

