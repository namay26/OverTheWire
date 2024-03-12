## Description

> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
---

To access this challenge, we need to login via ssh using bandit20 as the username and the password obtained in the last round. Using `nc`, we can create a connection in server mode, which will listen for connection. To send the password through netcat, we use echo along with the | operator and then we use (&) to let the process run in the background. This way, when we will run the binary setuid, it will be able to connect with our pre-running netcat server and recieve the password which we echoed.
    
    bandit20@bandit:~$ ls
    suconnect
    [2]-  Done                    [1] 24661echo -n 'GbKksEFF4yrVs6il55v6gwY5aVje5f0j' | nc -l -p 1234
    bandit20@bandit:~$ ls -la
    total 36
    drwxr-xr-x  2 root     root      4096 Oct  5 06:19 .
    drwxr-xr-x 70 root     root      4096 Oct  5 06:20 ..
    -rw-r--r--  1 root     root       220 Jan  6  2022 .bash_logout
    -rw-r--r--  1 root     root      3771 Jan  6  2022 .bashrc
    -rw-r--r--  1 root     root       807 Jan  6  2022 .profile
    -rwsr-x---  1 bandit21 bandit20 15600 Oct  5 06:19 suconnect
    bandit20@bandit:~$ echo -n 'VxCazJaVykI6W36BkBU0mJTCM8rR95XT' | nc -l -p 15600 &
    [5] 2309233
    bandit20@bandit:~$ ./suconnect 15600
    Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
    Password matches, sending next password
    NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
