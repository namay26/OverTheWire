## Description

> The password for the next level is stored in the file data.txt, which contains base64 encoded data.
---

To access this challenge, we need to login via ssh using bandit10 as the username and the password obtained in the last round. Here we have to decode the password from base64.

    bandit10@bandit:~$ ls
    data.txt
    bandit10@bandit:~$ cat data.txt
    VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==
    bandit10@bandit:~$ cat data.txt | base64 --decode
    The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
