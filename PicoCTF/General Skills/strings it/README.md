![](attachments/Pasted%20image%2020230401220556.png)

file : 

![](attachments/Pasted%20image%2020230401220817.png)

running _strings_ command:

![](attachments/Pasted%20image%2020230401220910.png)

the output is too large, so there is no way finding the flag with just looking through the strings,
so i pipe the output to the grep command with _picoCTF_ to try to find the flag:

![](attachments/Pasted%20image%2020230401221131.png)

and there it is.

>flag: picoCTF{5tRIng5_1T_827aee91}
