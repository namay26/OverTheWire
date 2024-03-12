## Description

> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
---

To access this challenge, we need to login via ssh using bandit19 as the username and the password obtained in the last round. Here if we `ls` the home directory, we find a setuid binary file which is owned by bandit20 but the group user is binary19. So if we execute it and run any command, it will be executed as bandit20. 
We can use this to obtain the password from `/etc/bandit_pass`.
    
    bandit19@bandit:~$ ls
    bandit20-do
    bandit19@bandit:~$ ls -la
    total 36
    drwxr-xr-x  2 root     root      4096 Oct  5 06:19 .
    drwxr-xr-x 70 root     root      4096 Oct  5 06:20 ..
    -rwsr-x---  1 bandit20 bandit19 14876 Oct  5 06:19 bandit20-do
    -rw-r--r--  1 root     root       220 Jan  6  2022 .bash_logout
    -rw-r--r--  1 root     root      3771 Jan  6  2022 .bashrc
    -rw-r--r--  1 root     root       807 Jan  6  2022 .profile
    bandit19@bandit:~$ ./bandit20-do
    bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
    VxCazJaVykI6W36BkBU0mJTCM8rR95XT
