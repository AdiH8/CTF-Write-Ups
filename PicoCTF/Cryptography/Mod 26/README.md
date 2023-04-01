![](attachments/Pasted%20image%2020230401203131.png)

The text is encrypted in ROT13.
ROT13 is a simple letter substitution cipher that replaces a letter with the 13th letter after it in the alphabet.

![](attachments/Pasted%20image%2020230401203442.png)

Python script for decrypting ROT13 text using codecs library:

```python
import codecs

text = "cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_uJdSftmh}"
rot13 = codecs.encode(text, 'rot_13')
print(rot13)

```

>Output: picoCTF{next_time_I'll_try_2_rounds_of_rot13_hWqFsgzu}