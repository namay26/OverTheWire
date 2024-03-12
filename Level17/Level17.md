## Description

> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
---

To access this challenge, we need to login via ssh using bandit16 as the username and the password obtained in the last round. In this challenge, we have to find open ports in the range of 31000 to 32000 providing ssl services. For this we can use `nmap` command on the localhost.

```
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
Starting Nmap 7.80 ( https://nmap.org ) at 2024-03-12 17:24 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00015s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```
It shows that only 5 ports are open and only 2 of them (31518 and 31790) provide ssl service. Port 31518 provides only echo service and hence 31790 port is our target. 

```
bandit16@bandit:~$ openssl s_client -connect localhost:31790
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = localhost
verify error:num=10:certificate has expired
notAfter=Mar 11 16:03:23 2024 GMT
verify return:1
depth=0 CN = localhost
notAfter=Mar 11 16:03:23 2024 GMT
verify return:1
---
Certificate chain
 0 s:CN = localhost
   i:CN = localhost
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA1
   v:NotBefore: Mar 11 16:02:23 2024 GMT; NotAfter: Mar 11 16:03:23 2024 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDCzCCAfOgAwIBAgIEDXN4CDANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjQwMzExMTYwMjIzWhcNMjQwMzExMTYwMzIzWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDN
8S1Sprko4yLIa1SgClrXUK8/YSF5CXWS1A9/4PKNlWVKIuXWsvtVHvIxW7WmZ2Bh
VokOKhH+dUGUuIDeoX2b1lyVNZWslzi0p0ejnOJLrWJJK6bNFwd2aR9Tp8GH7zxw
DjxdzmzhPFkNmq8exoeyhuBaE7t5l4zeY4uzbPp6+7qxOHo7dXxltvv9Hc7DDBhf
Er4Yqq5AyTvfjjSboaGqbLUU84H0xd3Abfnzg8A+aELky70iWPrW9k9URO1PqztW
aOjrKebpikpmbAE4zQmFblrQUswlHEhVR7wDSIZ0OBkT/vCamdvUW07JkV+gPb0e
rL0vWi/XT+pSU7tT/HWdAgMBAAGjZTBjMBQGA1UdEQQNMAuCCWxvY2FsaG9zdDBL
BglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0ZWQgYnkgTmNhdC4g
U2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3DQEBBQUAA4IBAQBq
nrEKKT+VUhKOJWURrha9CO0q3EqgsWoA4AIyOed8/JAfWH/hBQrZi7tIh9fPvMYG
CWV62aGV2JEBrplSjCl+ky6O6J9iAqUaZjfebpC6bG9X1B6CN/G97MjCcOoLUm9O
7mlK1WYVm9KXZxYAKKreuSsCmWzySMVYEaB9q5D844rxVsyDFcTiqMFhC/R7HNJW
mb52tvzMoYc5pCS9HlGaFoPaqruxvcUzNxNtLApFxusVNE0jeBdHSV/gFMJs1xGQ
alJaAWX6APoUQtf6n1nkbaxoXffjbg18tZUpsrkZq/pDrgSpbCL4Wv8/pb7ZtvLK
146IVOFCAqkuMylLctC6
-----END CERTIFICATE-----
subject=CN = localhost
issuer=CN = localhost
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1339 bytes and written 373 bytes
Verification error: certificate has expired
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 10 (certificate has expired)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: CE8F2AD9DA74284A696B3FCC97AA5FA9522E2D3B403A2DB2FFC140C5B21C252F
    Session-ID-ctx:
    Resumption PSK: 33247F01E205993A0323599C9BD8EE2B6B7954C6BFF346D1190F9957BF2DA3A13323EE8F16AB2520B56B6D73B5C50B19
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 6f 09 9c 1a bd 9d 27 03-38 43 a7 76 ab 40 83 20   o.....'.8C.v.@.
    0010 - bb 6a cf 08 a9 8f 5f 4b-94 77 38 6b 7a be e7 0d   .j...._K.w8kz...
    0020 - b5 4f ce 88 08 83 86 91-bf ab eb ac 57 d2 78 65   .O..........W.xe
    0030 - 7b 52 5a 54 8c 97 c3 ba-8d 72 c2 7d c2 67 ac c5   {RZT.....r.}.g..
    0040 - 28 2f 5d a2 8c 22 65 a0-de 2f a8 71 08 89 69 2f   (/].."e../.q..i/
    0050 - 21 ec 6c ff 19 cc 34 54-96 bb 70 f8 d3 10 be 10   !.l...4T..p.....
    0060 - 16 5b d0 f6 7d 6d bf e8-45 af 95 d3 6f af 51 1a   .[..}m..E...o.Q.
    0070 - 1a 54 98 77 22 5d e5 a7-34 18 31 2a ba c5 fd 98   .T.w"]..4.1*....
    0080 - f5 f6 a5 12 ca f1 52 cc-77 e1 c6 2b 4d c5 63 5e   ......R.w..+M.c^
    0090 - 25 d5 88 99 87 b6 0d 51-2c c9 4d 35 8f 84 a8 7a   %......Q,.M5...z
    00a0 - 70 b9 65 e8 d3 c4 75 c1-0f 55 11 5b 5d 22 30 4c   p.e...u..U.[]"0L
    00b0 - 28 76 8f a9 76 a2 89 45-51 9a 2b 68 e0 1a b4 77   (v..v..EQ.+h...w
    00c0 - 8c 2a fd bb 49 12 d5 42-e2 42 1d 7c 3a 40 e8 6c   .*..I..B.B.|:@.l

    Start Time: 1710264395
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 0FA85F8C79B452BE8960C307166DE5290CBB81ED384F1A6F41F978EAED446CDA
    Session-ID-ctx:
    Resumption PSK: 285DC9329166DC97022EFE5792427AD70DBAE10B01C95A989F754D0D0EDFC59424F01EA94B40FD5C20FBF0E83417C612
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 6f 09 9c 1a bd 9d 27 03-38 43 a7 76 ab 40 83 20   o.....'.8C.v.@.
    0010 - e4 c4 bd 94 98 82 aa b7-61 4e 46 23 d3 55 4e 28   ........aNF#.UN(
    0020 - 59 03 b9 c4 aa b6 92 50-19 1d ed 77 3a c6 be 81   Y......P...w:...
    0030 - cf 33 dd 42 db 81 47 71-02 51 30 ac 39 de 1d 89   .3.B..Gq.Q0.9...
    0040 - 39 75 2f 0b a0 8d 15 b8-d0 7e 78 a0 bb 2d be e7   9u/......~x..-..
    0050 - fb 5a 67 e8 1c 72 de 0b-c2 de b3 a6 da 02 c4 d8   .Zg..r..........
    0060 - aa 4e 0a 68 a0 ff b5 fe-53 a5 df 1b 73 37 bc 22   .N.h....S...s7."
    0070 - 71 7b 4c 07 e6 e9 9b 19-d8 f6 1c 48 ab 42 f3 28   q{L........H.B.(
    0080 - 6c 13 b8 d0 bf d0 d5 4c-c0 72 76 0b 97 4f da 13   l......L.rv..O..
    0090 - 90 d1 83 fd 6d 32 9c 15-6c 6a ce 58 95 81 4f 74   ....m2..lj.X..Ot
    00a0 - df 1d 35 8d 1f d1 64 3f-dc 15 48 14 00 be 55 fa   ..5...d?..H...U.
    00b0 - 32 1b 7c 40 68 95 9d 16-b2 38 60 a5 66 a7 75 79   2.|@h....8`.f.uy
    00c0 - 5c 9a 5c df f2 b0 58 09-16 ac 2a 37 1e 6e 2e ea   \.\...X...*7.n..

    Start Time: 1710264395
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
JQttfApK4SeyHwDlI9SXGR50qclOAil1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

Now, we have recieved a RSA key which can be used to access the next challenge so you need to store it somewhere. 

```
bandit16@bandit:/tmp$ mkdir /tmp/hello123
bandit16@bandit:/tmp/hello123$ touch sshkey2.private
bandit16@bandit:/tmp/hello123$ ls
sshkey2.private
bandit16@bandit:/tmp/hello123$ nano sshkey2.private
bandit16@bandit:/tmp/hello123$ cat sshkey2.private
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
```
