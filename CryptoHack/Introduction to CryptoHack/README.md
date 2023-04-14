[Intro to CryptoHack](https://cryptohack.org/challenges/introduction/)

## Finding flags

Each challenge is designed to help introduce you to a new piece of cryptography. Solving a challenge will require you to find a "flag".  
  
These flags will usually be in the format `crypto{y0ur_f1rst_fl4g}`. The flag format helps you verify that you found the correct solution.  
  
Try submitting this flag into the form below to solve your first challenge.

flag: 
>crypto{y0ur_f1rst_fl4g}

## Great Snakes

Run the attached Python script and it will output your flag.  
  
**Challenge files:**  
  - [great_snakes.py](https://cryptohack.org/static/challenges/great_snakes_35381fca29d68d8f3f25c9fa0a9026fb.py)  
  
### Solution
flag:
>crypto{z3n_0f_pyth0n}

## ASCII

ASCII is a 7-bit encoding standard which allows the representation of text using the integers 0-127.  
  
Using the below integer array, convert the numbers to their corresponding ASCII characters to obtain a flag.  
  
`[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]`

### Solution

```python
nums = [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]

for n in nums:
	print(chr(n), end="")
```

flag:
>crypto{ASCII_pr1nt4bl3}

## Hex

Included below is a flag encoded as a hex string. Decode this back into bytes to get the flag.  
`63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d`

### Solution

```python
hex_string = '63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d'
flag = bytes.fromhex(hex_string)
print(flag.decode())

```

flag:
>crypto{You_will_be_working_with_hex_strings_a_lot}

## Base64

Take the below hex string, _decode_ it into bytes and then _encode_ it into Base64.  
  
`72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf`

### Solution

```python
import base64

hex_string= '72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf'
flag = bytes.fromhex(hex_string)
print( base64.b64encode(flag))
```

flag:
>crypto/Base+64+Encoding+is+Web+Safe/

## Bytes and big integers

Convert the following integer back into a message:  
  
`11515195063862318899931685488813747395775516287289682636499965282714637259206269`

### Solution

```python
from Crypto.Util.number import *

num = 11515195063862318899931685488813747395775516287289682636499965282714637259206269
print(long_to_bytes(num))
```

flag:
>crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}

   
## XOR Starter

Given the string `label`, XOR each character with the integer `13`. Convert these integers back to a string and submit the flag as `crypto{new_string}`.

### Solution

```python
label = 'label'
for c in label:
    print(chr(ord(c) ^ 13), end='')

```

flag:
>crypto{aloha}