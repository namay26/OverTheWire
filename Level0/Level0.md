## Description

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0.

---
We have to connect to the game using SSH. The port, host and username is given. We enter the command 

`ssh bandit0@bandit.labs.overthewire.org -p 2220`

The -p flag allows you to enter the port to connect to.
'bandit0' is your username and bandit.labs.overthewire.org is the host.

`ssh {user}@{Host} -p {port_no}`

Once you enter this, it will ask you to enter the password which is given in the description.
