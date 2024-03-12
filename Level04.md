## Description

> The password for the next level is stored in a hidden file in the inhere directory.
---

To access this challenge, we need to login via ssh using bandit3 as the username and the password obtained in the last round.
Here, the file containing the key is a hidden file in the **inhere** directory. If we use `ls`, we will not be able to see the hidden files and hence we need to use the flag `-a` to see the hidden files as well. 
Now that we are able to see the hidden files, we use cat to retrieve the password for the next round.

    bandit3@bandit:~$ ls
    inhere
    bandit3@bandit:~$ cd inhere
    bandit3@bandit:~/inhere$ ls
    bandit3@bandit:~/inhere$ ls -a
    .  ..  .hidden
    bandit3@bandit:~/inhere$ cat .hidden
    2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
