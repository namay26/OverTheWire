## Desciption

> The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
---

To access this challenge, we need to login via ssh using bandit9 as the username and the password obtained in the last round. Here we have to search for human-readable strings in data.txt which are preceded by '='. For human readable strings we can use `strings ` and then use `grep` to find the required password.

    bandit9@bandit:~$ ls
    data.txt
    bandit9@bandit:~$ cat data.txt | strings | grep ^=
    =2""L(
    ========== passwordk^
    ========== is
    =Y!m
    ========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
    =r=_
    =uea
