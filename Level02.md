## Description

> The password for the next level is stored in a file called - located in the home directory.
---

To connect to the next level, you have to again use ssh and this time the username 'bandit1' with the password obtained in the previous round.
Now, we firstly use `ls` to view the files and then we try to use `cat` but `cat` command can not read a file names **'-'** directly and hence we need to specify the path of the file to be read.

    bandit1@bandit:~$ ls
    -
    bandit1@bandit:~$ cat ./-
    rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
