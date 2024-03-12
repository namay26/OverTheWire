## Description

> The password for the next level is stored in the file data.txt next to the word millionth.
---

To access this challenge, we need to login via ssh using bandit7 as the username and the password obtained in the last round. In this challenge we have a 'data.txt' where we have to search for the word "millionth" next to which is our password for the next challenge.
For this, we can use the grep command.

    bandit7@bandit:~$ ls
    data.txt
    bandit7@bandit:~$ grep "millionth" data.txt
    millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
