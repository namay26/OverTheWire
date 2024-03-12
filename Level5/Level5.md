## Description

> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
---

To access this challenge, we need to login via ssh using bandit4 as the username and the password obtained in the last round.
In this challenge, our aim is to find the only human-readable file which contains the password. Firstly we use `ls` to find a **inhere** directory, when we use `ls` again, we find multuple files. Now, the easiest way to do this is to look at the properties of the file using the `file` command.

    bandit4@bandit:~/inhere$ file ./*
    ./-file00: data
    ./-file01: data
    ./-file02: data
    ./-file03: data
    ./-file04: data
    ./-file05: data
    ./-file06: data
    ./-file07: ASCII text
    ./-file08: data
    ./-file09: data
    bandit4@bandit:~/inhere$ cat ./-file07
    lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

This way, we can clearly see that file07 is the only human readable file and hence it must contain the password. 
