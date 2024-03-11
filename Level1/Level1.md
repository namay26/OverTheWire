## Description

> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

--- 

Once you have entered the game, you have to use the command `ls` to access the files in the host. You wll see the file **Readme**. To read the file, you use the command `cat Readme` and you will get the password for the next level.
  
    bandit0@bandit:~$ ls
    readme  
    bandit0@bandit:~$ cat readme
    NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

