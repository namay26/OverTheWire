# Description

> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
---

To access this challenge, we need to login via ssh using bandit18 as the username and the password obtained in the last round. We are locked out from logging in through ssh. SSH not only allows us a remote connection but also remote execution of commands. So we will retrieve the password without actually logging into bandit18 by remotely executing the commands.

    $ssh bandit18@bandit.labs.overthewire.org -p 2220 ls
    bandit18@bandit.labs.overthewire.org's password:

When we enter the password it returns **readme**.
To access this we will again run the `cat` command remotely.

    $ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
    bandit18@bandit.labs.overthewire.org's password:

After this it will return the password.

    awhqfNnAbc1naukrpqDYcF95h7HoMTrC
