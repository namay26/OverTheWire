## Description

> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!).
---

To access this challenge, we need to login via ssh using bandit12 as the username and the password obtained in the last round. In this challenge firstly we need to create a new directory and copy the existing data.txt file to it. 
Now data.txt is a hexdump and we must first reverse it using `xxd`. Now if we use the `file` command, we see that it is now a gzip file but it doesnt have the suffix and hence we can not directly unzip it. So firstly, we will use `mv` command to give it the proper suffix. And then unzip it using `gzip -d`. 
The resultant file is now a bzip2 file and we must firstly give it the proper suffix(.bz) using `mv` and then unzip it. We must continuosly do the process to retrieve the password.
We will fall upon the following zips during this challenge:  
1) Gzip : The suffix for this type of compressed file is *.gz* and the command to unzip is `gzip -d`.
2) Bzip2 : The suffix for this type of compressed file is *.bz* and the command to unzip is `bzip2 -d`.
3) Tar : The suffix for this type of compressed file is *.tar* and the command to unzip is `tar -xf`.  

 ```
 bandit12@bandit:~$ ls
 data.txt
 bandit12@bandit:~$ mkdir /tmp/chk12
 bandit12@bandit:~$ cp data.txt /tmp/chk12
 bandit12@bandit:~$ cd /tmp/chk12
 bandit12@bandit:/tmp/chk12$ ls
 data.txt
 bandit12@bandit:/tmp/chk12$
 bandit12@bandit:/tmp/chk12$ xxd -r data.txt > data
 bandit12@bandit:/tmp/chk12$ ls
 data data.txt
 bandit12@bandit:/tmp/chk12$ mv data data2.gz
 bandit12@bandit:/tmp/chk12$ ls
 data2.gz data.txt
 bandit12@bandit:/tmp/chk12$ gzip -d data2.gz
 bandit12@bandit:/tmp/chk12$ ls
 data2 data.txt
 bandit12@bandit:/tmp/chk12$ file data2
 data2: bzip2 compressed data, block size = 900k
 bandit12@bandit:/tmp/chk12$ mv data2 data3.bz
 bandit12@bandit:/tmp/chk12$ bzip2 -d data3.bz
 bandit12@bandit:/tmp/chk12$ ls
 data3 data.txt
 bandit12@bandit:/tmp/chk12$ file data3
 data3: gzip compressed data, was "data4.bin", last modified: Thu Oct 5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 20480
 bandit12@bandit:/tmp/chk12$ mv data3 data4.gz
 bandit12@bandit:/tmp/chk12$ gzip -d data4.gz
 bandit12@bandit:/tmp/chk12$ ls
 data4 data.txt
 bandit12@bandit:/tmp/chk12$ file data4
 data4: POSIX tar archive (GNU)
 bandit12@bandit:/tmp/chk12$ mv data4 data5.tar
 bandit12@bandit:/tmp/chk12$ tar -xf data5.tar
 bandit12@bandit:/tmp/chk12$ ls
 data5.bin data5.tar data.txt
 bandit12@bandit:/tmp/chk12$ file data5.bin
 data5.bin: POSIX tar archive (GNU)
 bandit12@bandit:/tmp/chk12$ mv data5.bin data6.tar
 bandit12@bandit:/tmp/chk12$ tar -xf data6.tar
 bandit12@bandit:/tmp/chk12$ ls
 data5.tar data6.bin data6.tar data.txt
 bandit12@bandit:/tmp/chk12$ file data6.bin
 data6.bin: bzip2 compressed data, block size = 900k
 bandit12@bandit:/tmp/chk12$ mv data6.bin data7.bz
 bandit12@bandit:/tmp/chk12$ bzip2 -d data7.bz
 bandit12@bandit:/tmp/chk12$ ls
 data5.tar data6.tar data7 data.txt
 bandit12@bandit:/tmp/chk12$ file data7
 data7: POSIX tar archive (GNU)
 bandit12@bandit:/tmp/chk12$ mv data7 data8.tar
 bandit12@bandit:/tmp/chk12$ tar -xf data8.tar
 bandit12@bandit:/tmp/chk12$ ls
 data5.tar data6.tar data8.bin data8.tar data.txt
 bandit12@bandit:/tmp/chk12$ file data8.bin
 data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Oct 5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 49
 bandit12@bandit:/tmp/chk12$ mv data8.bin data9.gz
 bandit12@bandit:/tmp/chk12$ gzip -d data9.gz
 bandit12@bandit:/tmp/chk12$ ls
 data5.tar data6.tar data8.tar data9 data.txt
 bandit12@bandit:/tmp/chk12$ file data9
 data9: ASCII text
 bandit12@bandit:/tmp/chk12$ cat data9
 The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
