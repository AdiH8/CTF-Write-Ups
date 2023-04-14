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

```bash
python3 great_snakes.py
```

flag:
>crypto{z3n_0f_pyth0n}

## Network Attacks

Python makes such network communication easy with the `telnetlib` module. Conveniently, it's part of Python's standard library, so let's use it for now.  
  
For this challenge, connect to `socket.cryptohack.org` on port `11112`. Send a JSON object with the key `buy` and value `flag`.  
  
*The example script below contains the beginnings of a solution for you to modify, and you can reuse it for later challenges. *
  
Connect at `nc socket.cryptohack.org 11112`

**Challenge files:**  
  - [telnetlib_example.py](https://cryptohack.org/static/challenges/telnetlib_example_dbc6ff5dc4dcfac568d7978a801d3ead.py)

### Solution

```python
#!/usr/bin/env python3

import telnetlib
import json

HOST = "socket.cryptohack.org"
PORT = 11112

tn = telnetlib.Telnet(HOST, PORT)


def readline():
    return tn.read_until(b"\n")

def json_recv():
    line = readline()
    return json.loads(line.decode())

def json_send(hsh):
    request = json.dumps(hsh).encode()
    tn.write(request)


print(readline())
print(readline())
print(readline())
print(readline())


request = {
    "buy": "flag"
}
json_send(request)

response = json_recv()

print(response)

```

flag:
>crypto{sh0pp1ng_f0r_fl4g5}

