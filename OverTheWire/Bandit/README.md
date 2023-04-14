Bandit has 35 levels (including level 0). The Bandit server is accessible via Secure Shell (SSH). The credentials are provided to you at level 0, and completion of each level provides the password to the following level. There can be multiple ways to access the password file, but you only need to correctly do one to move on.

OverTheWire’s website: [https://overthewire.org/wargames/](https://overthewire.org/wargames/)

OverTheWire — Bandit: [https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

# Bandit Level 0

## Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

## Solution

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

# Bandit Level 0 → Level 1

## Level Goal

The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Solution

```bash
cat readme
```

password for Bandit1:
> NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

# Bandit Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called **-** located in the home directory

## Solution

```bash
cat ./-
```

password for Bandit2: 
>rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

# Bandit Level 2 → Level 3

## Level Goal

The password for the next level is stored in a file called **spaces in this filename** located in the home directory

## Solution

```bash
cat "spaces in this filename"
```

password for Bandit3:
>aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

# Bandit Level 3 → Level 4

## Level Goal

The password for the next level is stored in a hidden file in the **inhere** directory.

## Solution

```bash
cat inhere/.hidden 
```

password for Bandit4:
>2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

# Bandit Level 4 → Level 5

## Level Goal

The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

## Solution

```bash
file inhere/./-*
cat inhere/./-file07
```

password for Bandit5:
>lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

# Bandit Level 5 → Level 6

## Level Goal

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

-   human-readable
-   1033 bytes in size
-   not executable

## Solution

```bash
find inhere/ -type f -readable -not -executable -size 1033c

cat inhere/maybehere07/.file2
```

password for Bandit6:
>P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

# Bandit Level 6 → Level 7

## Level Goal

The password for the next level is stored **somewhere on the server** and has all of the following properties:

-   owned by user bandit7
-   owned by group bandit6
-   33 bytes in size

## Solution

```bash
find -type f -user bandit7 -group bandit6 -size 33c

cat /var/lib/dpkg/info/bandit7.password
```

password for Bandit7:
>z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

# Bandit Level 7 → Level 8

## Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Solution

```bash
cat data.txt | grep millionth
```

password for Bandit8:
>TESKZC0XvTetK0S9xNwm25STk5iWrBvP

# Bandit Level 8 → Level 9

## Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

```bash
cat data.txt | sort | uniq -u
```

password for Bandit9:
>EN632PlfYiZbn3PhVK3XOGSlNInNE00t

# Bandit Level 9 → Level 10

## Level Goal

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

## Solution

```bash
strings data.txt | grep ====
```

password for Bandit10:
>G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

# Bandit Level 10 → Level 11

## Level Goal

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

## Solution

```bash
cat data.txt | base64 --decode
```

password for Bandit11:
>6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

# Bandit Level 11 → Level 12

## Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Solution

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

password for Bandit12:
>JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

# Bandit Level 12 → Level 13

## Level Goal

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Solution

```bash
cat data.txt | xxd -r > data

mv data data2.gz
gzip -d data2.gz

mv data2 data3.bz
bzip2 -d data3.bz

mv data3 data4.gz
gzip -d data4.gz

mv data4 data5.tar
tar -xf data5.tar

mv data5.bin data6.tar
tar -xf data6.tar

mv data6.bin data7.bz
bzip2 -d data7.bz

mv data7 data8.tar
tar -xf data8.tar

mv data8.bin data9.gz
gzip -d data9.gz

cat data9
```

password for Bandit13:
>wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

# Bandit Level 13 → Level 14

## Level Goal

The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on
[SSH Key level 13](sshkey.private)
## Solution

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

chmod 700 sshkey.private

ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

# Bandit Level 14 → Level 15

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Solution

```bash
cat /etc/bandit_pass/bandit14
```

current password:
>fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

```bash
nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

password for Bandit15:
>jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

# Bandit Level 15 → Level 16

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

## Solution

```bash
openssl s_client -connect localhost:30001
```

password for Bandit16:
>JQttfApK4SeyHwDlI9SXGR50qclOAil1

# Bandit Level 16 → Level 17

## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Solution

```bash
nmap -sV localhost -p 31000-32000
```

password for Bandit17: [SSH Key lvl17](sshkey17.private)

# Bandit Level 17 → Level 18


## Level Goal

There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

## Solution

```bash 
diff passwords.old passwords.new
```

password for Bandit18:
>hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg

# Bandit Level 18 → Level 19

## Level Goal

The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

## Solution

Connevt to the bandit18:
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 -t "/bin/sh"
```

```bash
cat readme
```

password for bandit19:
>awhqfNnAbc1naukrpqDYcF95h7HoMTrC

# Bandit Level 19 → Level 20

## Level Goal

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Solution

```bash 
./bandit20-do cat /etc/bandit_pass/bandit20
```

password for Bandit20:
>VxCazJaVykI6W36BkBU0mJTCM8rR95XT

# Bandit Level 20 → Level 21

## Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think

## Solution

```bash
echo "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | netcat -lp 1234 &

./suconnect 1234
```


password for bandit21:
>NvEJF7oVjkddltPSrdKEFOllh9V1IBcq

# Bandit Level 21 → Level 22

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Solution

```bash
cat /etc/cron.d/cronjob_bandit22

cat /usr/bin/cronjob_bandit22

cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

password for bandit22:
>WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff

# Bandit Level 22 → Level 23

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Solution 

```bash
ls /etc/cron.d

cat /etc/cron.d/cronjob_bandit23

cat /usr/bin/cronjob_bandit23.sh

echo I am user bandit23 | md5sum | cut -d ' ' -f 1
>8ca319486bfbbc3663ea0fbe81326349

cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

password for bandit23:
>QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G

# Bandit Level 23 → Level 24

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

**NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Solution 

```bash
nano /var/spool/bandit24/script.sh
~~~~~~~~~~~~~~
#!/bin/bash  
cat /etc/bandit_pass/bandit24 > /tmp/bandit24_pass
~~~~~~~~~~~~~~
cat /tmp/bandit24_pass

```

password for bandit24:
>VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar

# Bandit Level 24 → Level 25

## Level Goal

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.  
You do not need to create new connections each time

## Solution

```bash
for i in {0000..9999}; do echo VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i; done | nc 127.0.0.1 30002 | grep -v Wrong
```

password for bandit25:
>p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d