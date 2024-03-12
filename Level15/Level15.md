## Description

> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
---

Here we have to establish a connection with the localhost on port 30000 and then send the password obtained in the previous challenge. For this, we can use netcat or `nc` command which follows the syntax `nc [ip] [port]`.  

    bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 | nc localhost 30000
    Correct!
    jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
