## Bounty Hacker

![](attachments/Pasted%20image%2020230414160847.png)

[Bounty Hacker THM](https://tryhackme.com/room/cowboyhacker)

### Find open ports

```bash
nmap -sV -sC 10.10.94.179
```

![](attachments/Pasted%20image%2020230414160919.png)

We see that 21,22,80 ports are open so we try to connect using ftp, because anonymous login is allowed

![](attachments/Pasted%20image%2020230414161152.png)

using _ls_ i we see two files called _locks.txt_ and _task.txt_ i _get_ them to my system

![](attachments/Pasted%20image%2020230414161835.png)

### Who wrote the task list?

![](attachments/Pasted%20image%2020230414162022.png)

Answer:
>lin

### What service can you bruteforce with the text file found?

The content second file _locks.txt_ are bunch of passwords that we can try to brute force with them

![](attachments/Pasted%20image%2020230414162310.png)

The question is what we can brute force? With the information about the open ports we see that the SSH port is open so we will try to brute force it using hydra

Answer:
>SSH

### What is the users password?

```bash
hydra -l lin -P locks.txt 10.10.94.179 ssh 
```

![](attachments/Pasted%20image%2020230414162624.png)

Answer:
>RedDr4gonSynd1cat3

### user.txt 

After connecting to the system using ssh, there is user.txt file in the directory, se we check the contents

![](attachments/Pasted%20image%2020230414163030.png)

Answer:
>THM{CR1M3_SyNd1C4T3}

### root.txt

we enter sudo -l and we see that we have permission of tar command as root.

![](attachments/Pasted%20image%2020230414163542.png)

we check [gtfobins]](https://gtfobins.github.io/) for exploiting the tar command for privilage escalation and i find this:

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

![](attachments/Pasted%20image%2020230414163756.png)

we have root access!

![](attachments/Pasted%20image%2020230414163900.png)

Answer:
>THM{80UN7Y_h4cK3r}

