## Description

> The password for the next level is stored somewhere on the server and has all of the following properties:  
  owned by user bandit7  
  owned by group bandit6  
  33 bytes in size  
---

To access this challenge, we need to login via ssh using bandit6 as the username and the password obtained in the last round. Here we again have to find a file with certain properties which can be stores anywhere in the system.
We use the find command with following flags:  

  -size : Specifies the size.  
  -user : Can be used to specify the owner of the file.  
  -group : Can be used to specify the group owner of the file.  

    bandit6@bandit:/home$ find -size 33 -user bandit7 -group bandit6
    /var/lib/dpkg/info/bandit7.password
    bandit6@bandit:/home$ cat /var/lib/dpkg/info/bandit7.password
    z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
