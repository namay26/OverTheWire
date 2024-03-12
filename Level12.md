## Description

> The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.
---

To access this challenge, we need to login via ssh using bandit11 as the username and the password obtained in the last round. The text in data.txt is encoded using ROT13 algorithm where all the letters have been shifted by 13 positions. To decode this we can use  `tr` command which will take two input sets.
It looks up the character in the first set and replaces it with the character at the same position in the second set.

    bandit11@bandit:~$ ls
    data.txt
    bandit11@bandit:~$ cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
    The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

First set -   
[ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz]  
Second set-   
[NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm]
