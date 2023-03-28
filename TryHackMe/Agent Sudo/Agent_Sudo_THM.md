![](Screenshots/Pasted%20image%2020230328223328.png)
[Agent Sudo THM](https://tryhackme.com/room/agentsudoctf)
## Enumerate

### 1. How many open ports ?
Run a nmap scan with default scripts and we see that ports 21,22,80 are open
![](Screenshots/Pasted%20image%2020230328224005.png)
>Answer: 3

### 2. How you redirect yourself to a secret page?	
![](Screenshots/Pasted%20image%2020230328224649.png)
>Answer: user-agent

### 3. What is the agent name? 
Given the clue that the user-agent code name is C. So we intercept the connection with burpsuite and we change the user-agent with C:
![](Screenshots/Pasted%20image%2020230328225712.png)

Then i got redirected to this page:
![](Screenshots/Pasted%20image%2020230328225858.png)
>Anwser: chris

## Hash cracking and brute-force 

### 1.FTP password

After brute forcing the ftp password with hydra we see:
![](Screenshots/Pasted%20image%2020230328232101.png)

>Answer: crystal

After logging in with ftp we see three files:

![](Screenshots/Pasted%20image%2020230328232435.png)

To_agentJ.txt :
![](Screenshots/Pasted%20image%2020230328234323.png)

After trying to extract files from the image files:
![](Screenshots/Pasted%20image%2020230328233231.png)

We see a new extracted directory
![](Screenshots/Pasted%20image%2020230328234138.png)

### 2.Zip file password
After brute forcing the zip file with john we found the zip password:
![](Screenshots/Pasted%20image%2020230328234550.png)
>Answer: alien

### 3.Steg password
Then i try to open the zip file and i see that message:
![](Screenshots/Pasted%20image%2020230328235913.png)

the 'QXJlYTUx' message is encrypted so i try to decode it from base64:
![](Screenshots/Pasted%20image%2020230329000154.png)

>Answer: Area51

### 4.Who is the other agent (in full name)?
Extracting the cute-alien.jpg with steghide we find a secret message:
![](Screenshots/Pasted%20image%2020230329002213.png)

![](Screenshots/Pasted%20image%2020230329002246.png)
> Answer: james

### 5.SSH password
>Answer: hackerrules