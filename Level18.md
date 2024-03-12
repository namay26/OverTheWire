## Description

> There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
---

To access this challenge, we need to login via ssh using bandit17 as the username and the RSA key obtained in the last round. We have to find the difference between the two files and for that we can use the `diff` command.

```
bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
---
> hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
```
The second part is the password and the only thing that has changed from the first file.
