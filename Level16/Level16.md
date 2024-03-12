## Description

> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
---

To access this challenge, we need to login via ssh using bandit15 as the username and the password obtained in the last round. Here we are needed to establish a SSL connection. For this we shall use the `openssl` command and connect to the given port.

```
bandit15@bandit:~$ echo "jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt" | openssl s_client -connect localhost:30001 -ign_eof
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
MIIDCzCCAfOgAwIBAgIEYi1LITANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjQwMzExMTYwMjIzWhcNMjQwMzExMTYwMzIzWjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDK
fxi+AhmDt6lpDRfe4y1uFysQztrIme8xlKoaVTgpdL/brWpCqCiKJotUqPq1OsOH
EnfuE7vCrUq4f7c2aWu+k7pH59I/lAvI8TQVDGZWek4FaBHBfkb6LZv5/ucHI2jL
LZo7LBbmnKNt1CIdgq7FwXqKMeoZk4R4OwyWSzwpyC4woGxNpjUla98lqXfnzxgu
c36Cyakk68K4oNdzv9oZ4qQ2ZcLYlvRTuE8YMAi9BJcEpQ9i1nDSnv1XeNXiJLjI
y4/sw5wGNUtcYr94VWvZPu+NHMqfthfbRMKssDDS5eHtD1NMhiulH0lptDjvKirD
3zEwInrbqKmOkerOKoKfAgMBAAGjZTBjMBQGA1UdEQQNMAuCCWxvY2FsaG9zdDBL
BglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0ZWQgYnkgTmNhdC4g
U2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3DQEBBQUAA4IBAQCl
l5TlvnTvocjhI9nEoD67RBk6buONR/xP7anvjWCrA+5r69geapeG51f7Kdtaqr9F
aZJUUoxJD5JzPNH7ae6R5WrFjvCATKzzB45i84ukKHHF892V6caqv6qC1y6403Uo
Uh4NG+GPOZi95jH/bteUms/F+e3Wmw85pds09CWQuMSaheNbFZl10z6WtERTdHC9
S9BpP7xthDsmr6toEHAqlu9EpASYmCGaC5QNG0/KP4/5N+JDwjh4SIcOB68y5uTD
ad9n2lf1smQkYCVNW0SFYiO3+0oAnZkAkaU+b4FIgWt5+pGlHYS2vLSaz41SGQOh
bapfl5nT1wQwJUZ53bZn
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
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 8F90EA1580632647BE7D4EA87230282CDD22F7E05039AC36C45C48BA1E8949EC
    Session-ID-ctx:
    Resumption PSK: 335C6436EC382F2F3597BCE8102FBFA9FB514B5D5C424FA51B0AB1A80831EF828E1CA2DA4892C749D273A3BFDE0EED48
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f8 9f 9c d7 65 f7 48 16-76 e3 01 51 04 07 de 1c   ....e.H.v..Q....
    0010 - 8d 4b f7 ae 2c 15 23 81-79 8d 49 36 b6 80 d9 0a   .K..,.#.y.I6....
    0020 - c6 88 04 0c a5 f9 d5 3c-1c 3a 20 e5 a6 7d da 90   .......<.: ..}..
    0030 - e6 f2 6a 8f d5 7e ba d7-15 da 4f 53 53 02 13 da   ..j..~....OSS...
    0040 - ad 4b d3 1e e2 ba aa 3f-ab 9b 66 d2 da f1 64 4f   .K.....?..f...dO
    0050 - 2a 56 46 90 60 fb cc 1d-6d ab bb 3a ff 51 f6 6d   *VF.`...m..:.Q.m
    0060 - 13 a4 7b 84 2c 6b 9f 81-96 73 98 50 e0 43 e2 8a   ..{.,k...s.P.C..
    0070 - 0d 0b 1a 76 c1 08 89 25-23 e7 21 9d 1a 82 5c 56   ...v...%#.!...\V
    0080 - 1c 8f 97 c0 31 23 8f 30-cf b0 23 37 b6 52 f3 70   ....1#.0..#7.R.p
    0090 - 41 7b 02 18 60 49 e2 4d-27 a5 81 6a 04 35 32 a4   A{..`I.M'..j.52.
    00a0 - ff b4 fa 70 73 95 02 68-84 ff 9a 03 6c 1c f4 82   ...ps..h....l...
    00b0 - bb 83 da 49 8e e4 be 99-f5 be 95 30 45 41 52 c9   ...I.......0EAR.
    00c0 - 1e 90 51 1c 5a 79 f7 94-15 2f 7c 39 35 7a 38 12   ..Q.Zy.../|95z8.

    Start Time: 1710258777
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1

closed
```
