# Bandit Level 18 → Level 19

## Level Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

## Commands you may need to solve this level
ssh, ls, cat

## Solution

The interesting fact about SSH is that along with connecting to the server, it lets us to run commands. Since .bashrc is modified, it is not possible to login with SSH. It is mentioned that the password is in the readme file in the homedirectory. Let us read that file without actually logging in, using SSH.

```                                                                                                                                                           
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit18@bandit.labs.overthewire.org ls -a                                      #to list all the files in the homedirectory
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
.
..
.bash_logout
.bashrc
.profile
readme
                                                                                                                                                           
┌──(kali㉿kali)-[~]
└─$ ssh -p 2220 bandit18@bandit.labs.overthewire.org cat readme                                  #to read the readme file
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```


#### Command-line help text
```
ls      -> list directory contents
-a      -> all

cat     -> concatenate files and print on the standard output
ssh     -> OpenSSH SSH client (remote login program)
```
