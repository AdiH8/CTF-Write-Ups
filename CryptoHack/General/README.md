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

## XOR Properties

Below is a series of outputs where three random keys have been XOR'd together and with the flag. Use the above properties to undo the encryption in the final line to obtain the flag.  
  
KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313  
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e  
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1  
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf

### Solution

```python
KEY1 = "a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313"
KEY2_xor_KEY1 = "37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"
KEY2_xor_KEY3 = "c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"
FLAG_xor_KEYS = "04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"

KEY1 = int(KEY1, 16)
KEY2_xor_KEY1 = int(KEY2_xor_KEY1, 16)
KEY2_xor_KEY3 = int(KEY2_xor_KEY3, 16)
FLAG_xor_KEYS = int(FLAG_xor_KEYS, 16)

KEY2 = KEY1 ^ KEY2_xor_KEY1

KEY3 = KEY2 ^ KEY2_xor_KEY3

flag = KEY1 ^ KEY3 ^ KEY2 ^ FLAG_xor_KEYS

flag_hex = hex(flag)[2:]

flag_bytes = bytes.fromhex(flag_hex)

flag_str = flag_bytes.decode("ASCII")

print(flag_str)

```

flag:
>crypto{x0r_i5_ass0c1at1v3}

## Favourite byte

I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.  
  
`73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d`

### Solution

```python

data_hex = "73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d"

data_bytes = bytes.fromhex(data_hex)

for key in range(256):
    decrypted_bytes = bytes([byte ^ key for byte in data_bytes])
    
    decrypted_str = decrypted_bytes.decode("ASCII")
    if "crypto" in decrypted_str:   
    	print(decrypted_str)
```

flag:
>crypto{0x10_15_my_f4v0ur173_by7e}
