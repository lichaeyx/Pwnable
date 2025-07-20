# Dreamhack : baby-bof
[ Author : L1ya ]

**1. Analysis**

name size = 16, Receiving = 15\n
We want to call the function 'win'
win's address is '40125b'
return address is '0x7fffffffdfd8'

**2. Vulnerabilities**

if you input more than 15, over the sixteenth letters overflow
if you input more than 4, last letter overflow to return address

**3. Exploitation**

I write the name: '123456781234567' and add the win address '40125b'
And, I find the return address is in the fourth floor
So I input the number over than 4

**4. Result**

I can call 'win' function!
I can get flag!!

You mustn't be here! It's a vulnerability!

// It is important to Receiving value << size value ==> BoF?
// I want to challenge more difficult question!
