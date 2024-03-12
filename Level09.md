## Description

> The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.
---

To access this challenge, we need to login via ssh using bandit8 as the username and the password obtained in the last round. In this challenge we use `sort` command along with `uniq` command to omit the duplicate lines.

    bandit8@bandit:~$ ls
    data.txt
    bandit8@bandit:~$ sort data.txt | uniq -u
    EN632PlfYiZbn3PhVK3XOGSlNInNE00t
