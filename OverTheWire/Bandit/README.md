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


