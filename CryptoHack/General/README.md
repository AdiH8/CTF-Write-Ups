# Encoding

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

## Encoding Challenge

Can you pass all 100 levels to get the flag?  
  
The _13377.py_ file attached below is the source code for what's running on the server. The _pwntools_example.py_ file provides the start of a solution using the incredibly convenient pwntools library. which we recommend. If you'd prefer to use Python's in-built telnetlib, _telnetlib_example.py_ is also provided.  
  
For more information about connecting to interactive challenges, see the [FAQ](https://cryptohack.org/faq#netcat). Feel free to skip ahead to the cryptography if you aren't in the mood for a coding challenge!  
  
Connect at `nc socket.cryptohack.org 13377`

```python
from pwn import * # pip install pwntools
import json
from Crypto.Util.number import bytes_to_long, long_to_bytes
import base64
import codecs
import random
from binascii import unhexlify


r = remote('socket.cryptohack.org', 13377, level = 'debug')

def json_recv():
    line = r.recvline()
    return json.loads(line.decode())

def json_send(hsh):
    request = json.dumps(hsh).encode()
    r.sendline(request)

def list_to_string(s):
    output = ""
    return(output.join(s))

for i in range(0,101):
    received = json_recv()
    if "flag" in received:
        print("\n[*] FLAG: {}".format(received["flag"]))
        break

    print("\n[-] Cycle: {}".format(i))
    print("[-] Received type: {}".format(received["type"]))
    print("[-] Received encoded value: {}".format(received["encoded"]))

    word = received["encoded"]
    encoding = received["type"]

    if encoding == "base64":
        decoded = base64.b64decode(word).decode('utf8').replace("'", '"')
    elif encoding == "hex":
        decoded = (unhexlify(word)).decode('utf8').replace("'", '"')
    elif encoding == "rot13":
        decoded = codecs.decode(word, 'rot_13')
    elif encoding == "bigint":
        decoded = unhexlify(word.replace("0x", "")).decode('utf8').replace("'", '"')
    elif encoding == "utf-8":
        decoded = list_to_string([chr(b) for b in word])

    print("[-] Decoded: {}".format(decoded))
    print("[-] Decoded Type: {}".format(type(decoded)))

    to_send = {
        "decoded": decoded
    }

    json_send(to_send)
```

flag:
>crypto{3nc0d3_d3c0d3_3nc0d3}


# XOR
   
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

## You either know, XOR you don't
//To do

## Lemur XOR

I've hidden two cool images by XOR with the same secret key so you can't see them!  
  
This challenge requires performing a visual XOR between the RGB bytes of the two images - not an XOR of all the data bytes of the files.  
  
**Challenge files:**  
  - [lemur.png](https://cryptohack.org/static/challenges/lemur_ed66878c338e662d3473f0d98eedbd0d.png)  
  - [flag.png](https://cryptohack.org/static/challenges/flag_7ae18c704272532658c10b5faad06d74.png)

### Solution

```bash
pip3 install opencv-python
```

```python
import cv2

img1 = cv2.imread('image1.png')
img2 = cv2.imread('image2.png')

# Make sure they have the same dimensions
img1 = cv2.resize(img1, (img2.shape[1], img2.shape[0]))

# XOR the two images on each color channel
result_b = cv2.bitwise_xor(img1[:,:,0], img2[:,:,0])
result_g = cv2.bitwise_xor(img1[:,:,1], img2[:,:,1])
result_r = cv2.bitwise_xor(img1[:,:,2], img2[:,:,2])

# Merge the results into a single color image
result = cv2.merge((result_b, result_g, result_r))

# Write the result to a new image file
cv2.imwrite('result.png', result)

```

![](attachments/Pasted%20image%2020230416145203.png)

flag:
>crypto{X0Rly_n0t!}

# Mathematics

## Greatest Common Divisor

The Greatest Common Divisor (GCD), sometimes known as the highest common factor, is the largest number which divides two positive integers (a,b).  
  
For `a = 12, b = 8` we can calculate the divisors of a: `{1,2,3,4,6,12}` and the divisors of b: `{1,2,4,8}`. Comparing these two, we see that `gcd(a,b) = 4`.  
  
Now imagine we take `a = 11, b = 17`. Both `a` and `b` are prime numbers. As a prime number has only itself and `1` as divisors, `gcd(a,b) = 1`.  
  
We say that for any two integers `a,b`, if `gcd(a,b) = 1` then `a` and `b` are coprime integers.  
  
If `a` and `b` are prime, they are also coprime. If `a` is prime and `b < a` then `a` and `b` are coprime.  
  
Think about the case for `a` prime and `b > a`, why are these not necessarily coprime?  
  
There are many tools to calculate the GCD of two integers, but for this task we recommend looking up [Euclid's Algorithm](https://en.wikipedia.org/wiki/Euclidean_algorithm).  
  
Try coding it up; it's only a couple of lines. Use `a = 12, b = 8` to test it.  
  
Now calculate `gcd(a,b)` for `a = 66528, b = 52920` and enter it below.

### Solution

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

a = 66528 
b = 52920
print(gcd(a,b))
```

Answer:
>1512

## Extended GCD

Let `a` and `b` be positive integers.  
  
The extended Euclidean algorithm is an efficient way to find integers `u,v` such that  
  
`a * u + b * v = gcd(a,b)`  
  
Using the two primes `p = 26513, q = 32321`, find the integers `u,v` such that  
  
`p * u + q * v = gcd(p,q)`  
  
Enter whichever of `u` and `v` is the lower number as the flag.

### Solution 

```python
def egcd(a, b):
    if b == 0:
        return a, 1, 0
    else:
        gcd, u, v = egcd(b, a % b)
        return gcd, v, u - (a // b) * v

p = 26513
q = 32321
gcd, u, v = egcd(p, q)

print(min(u, v))

```

Answer:
>-8404

## Modular Arithmetic 1

Formally, "calculating time" is described by the theory of congruences. We say that two integers are congruent modulo m if `a ≡ b mod m`.  
  
Another way of saying this, is that when we divide the integer `a` by `m`, the remainder is `b`. This tells you that if m divides a (this can be written as `m | a`) then `a ≡ 0 mod m`.  
  
Calculate the following integers:  
  
11 ≡ x mod 6  
8146798528947 ≡ y mod 17  
  
The solution is the smaller of the two integers.

### Solution

```python
x = 11 % 6
y = 8146798528947 % 17

print(min(x, y))
```

Answer:
>4

