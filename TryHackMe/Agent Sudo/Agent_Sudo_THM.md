![](Screenshots/Pasted%20image%2020230328223328.png)

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