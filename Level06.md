## Description

> The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
  human-readable  
  1033 bytes in size  
  not executable
---

To access this challenge, we need to login via ssh using bandit5 as the username and the password obtained in the last round. In this challenge we firstly use `ls` to find **inhere** directory. Upon entering,
using `cd`, we find multiple directories. Our task is to find a file with all the given properties and so we can use `find` command with its flags. We can use `man find` to see
all the different flags available. 

  **-size** : It allows you to enter the size of the file to be found. (1033c stands for 1033 bytes and c specifies ASCII characters ie Human readable)  
  **-type** : It allows you to specify what kind of file are you looking for. It can be a directory or maybe like in our case a regular file.  
  **-executable** : It searches for only those files which are executable.

    bandit5@bandit:~$ ls
    inhere
    bandit5@bandit:~$ cd inhere
    bandit5@bandit:~/inhere$ ls
    maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
    maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
    maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
    bandit5@bandit:~/inhere$ find -type f -size 1033c ! -executable
    ./maybehere07/.file2
    bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
    P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
