## Description

> The password for the next level is stored in a file called spaces in this filename located in the home directory
---

To access this challenge, we need to login via ssh using bandit2 as the username and the password obtained in the last round. 
Here firstly we use `ls` to view the file but we see that the file name has spaces in between.
We can not directly use `cat` to read the file. So we have two options:
    
    bandit2@bandit:~$ ls
    spaces in this filename
    bandit2@bandit:~$ cat "spaces in this filename"
    aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
    bandit2@bandit:~$ cat spaces\ in\ this\ filename
    aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

Either put the filename in quotes or use backslash(\\) followed by a space to create a space in the filename.
