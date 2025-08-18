---
dg-publish: true
---
---
![](../_attachments/Pasted%20image%2020250629112800.png)



# ctf: Too Small I Guess (500)
![](../_attachments/Pasted%20image%2020250628153414.png)



![](../_attachments/Pasted%20image%2020250628153445.png)

downloaded the file value.txt

![](../_attachments/Pasted%20image%2020250628153333.png)
 cat the file 

i got : 
c = 799827088267
N = 2214361715201
e = 65537

![](../_attachments/Pasted%20image%2020250628154346.png)

used exiftool to check the file details

- Ciphertext `c = 799827088267`
    
- Modulus `N = 2214361715201`
    
- Public exponent `e = 65537`



## Challenge Description

The challenge provides a file `values.txt` containing three values:

- Ciphertext: ( c = 799827088267 )
- Modulus: ( N = 2214361715201 )
- Public exponent: ( e = 65537 )

The goal is to decrypt the ciphertext to recover the flag, which follows the format `BMCTF{...}`. This is a classic RSA encryption problem, where the ciphertext is computed as ( c = m^e \mod N ), and we need to find the plaintext ( m ).

## Solution Approach

## 🛠 Step 1: Spotting the Weakness

RSA is only secure when the modulus `N` is huge (e.g., 2048 bits).  
Here, `N` is only ~41 bits (`log2(N) ≈ 40.7`) – tiny enough to factor instantly.

So our approach is clear: **factor N → calculate φ(N) → compute private key d → decrypt.**

---

## 🛠 Step 2: Factoring N

Using Python’s `sympy.factorint`:

`from sympy import factorint  N = 2214361715201 print(factorint(N))`

Output:

`{1299709: 1, 1704709: 1}`

So:

- `p = 1299709`
    
- `q = 1704709`
    

Check: `p * q = N 

---

## 🛠 Step 3: Euler’s Totient

Formula:

φ(N)=(p−1)(q−1)\varphi(N) = (p-1)(q-1)φ(N)=(p−1)(q−1)

`p = 1299709 q = 1704709 phi_N = (p-1) * (q-1) print(phi_N)`

Output:

`2214358710784`

---

## 🛠 Step 4: Private Key (d)

The private key `d` is the modular inverse of `e` modulo φ(N):

`from sympy import mod_inverse  e = 65537 d = mod_inverse(e, phi_N) print(d)`

Output:

`1156154451217`

---

## 🛠 Step 5: Decryption

Now decrypt the ciphertext:

m=cdmod  Nm = c^d \mod Nm=cdmodN

`c = 799827088267 m = pow(c, d, N) print(m)`

Output:

`1635730432794`

So plaintext `m = 1635730432794`.

---

## 🛠 Step 6: Interpreting m

Convert to hex:

`hex_m = hex(m)[2:] print(hex_m)`

Output:

`17d8d6b6b2aa`

The bytes weren’t printable ASCII. But in CTFs, flags sometimes just use the raw decimal/hex values.

`BMCTF{17d8d6b6b2aa}`

---
# ctf: XORRY (50)

downloaded the file and cat command on 

![](../_attachments/Pasted%20image%2020250628161152.png)
The binary didn’t have execute permissions initially, so I fixed that:

`chmod +x XORyy`

![](../_attachments/Pasted%20image%2020250628161341.png)

Now I could run it:

`./XORyy`

Output:

`Enter the secret key:`

If I entered something random (`test, key, etc`), it just said:

`Incorrect key. Try again.`


![](../_attachments/Pasted%20image%2020250628161439.png)
## 🛠 Step 2: Static Analysis with `strings`

Next move: check if the flag is simply embedded in the binary. Classic beginner trick.

`strings XORyy | less`

Found some interesting strings:

`Enter the secret key: Incorrect key. Try again. Congratulations! You found the flag: BMCTF{X0R_Is_Fun} xor_crypt strcmp`

![](../_attachments/Pasted%20image%2020250628161705.png)

flag found after reading list

---
# ctf: idkwhattonamethis

![](../_attachments/Pasted%20image%2020250628162405.png)

## downloaded and runned cat command its same as above using ELF (Executable and Linkable Format) binary file.

![](../_attachments/Pasted%20image%2020250628163152.png)

used chmod +x and later tried random key and also string commands

![](../_attachments/Pasted%20image%2020250628163453.png)


![](../_attachments/Pasted%20image%2020250628170348.png)

to analyse i used radare2 too

![](../_attachments/Pasted%20image%2020250628170412.png)


```
[0x000010d0]> afl (View the functions in the binary)

0x00001030    1      6 sym.imp.puts
0x00001040    1      6 sym.imp.strlen
0x00001050    1      6 sym.imp.printf
0x00001060    1      6 sym.imp.srand
0x00001070    1      6 sym.imp.strtol
0x00001080    1      6 sym.imp.time
0x00001090    1      6 sym.imp.ptrace
0x000010a0    1      6 sym.imp.__isoc99_scanf
0x000010b0    1      6 sym.imp.exit
0x000010c0    1      6 sym.imp.__cxa_finalize
0x000010d0    1     33 entry0
0x00001100    4     34 sym.deregister_tm_clones
0x00001130    4     51 sym.register_tm_clones
0x00001170    5     54 entry.fini0
0x000011b0    1      9 entry.init0
0x0000129c    6     93 sym.flibberVMCheck
0x000012f9    1     36 sym.gizmoXOR
0x00001644    1      9 sym._fini
0x00001587    6    155 sym.bamboozler
0x0000131d    1     67 sym.squibbleIndex
0x000011b9    3     68 sym.wibbleWobble
0x00001360    4    551 sym.scrumbleFlaginator
0x00001622    1     33 main
0x000011fd    6    159 sym.zoinkifyLogic
0x00001000    3     23 sym._init
```
![](../_attachments/Pasted%20image%2020250628171230.png)

![](../_attachments/Pasted%20image%2020250628171250.png)


![](../_attachments/Pasted%20image%2020250628174404.png)

---
# ctf: Disk Message

The challenge provided a disk image (or file disguised as one). The name _Disk Message_ suggests that some data was hidden inside the file system or raw disk sectors.  
Goal: extract the hidden message/flag `BMCTF{...}`.


![](../_attachments/Pasted%20image%2020250628184421.png)

---
# ctf: takiya
We’re given an image file. The name _takiya_ hints at hiding something in plain sight. Goal: extract the hidden flag.

## 🛠 Step 1: Inspect the File

I ran `exiftool` on the file:

`exiftool takiya`

Output:

`File Name        : takiya File Size        : 240 kB File Type        : TXT File Type Extension: txt MIME Type        : text/plain MIME Encoding    : us-ascii Line Count       : 1 Word Count       : 1`

So the file is **just one huge ASCII line**.
![](../_attachments/Pasted%20image%2020250628225747.png)

---

## 🛠 Step 2: Hex Dump

To see the raw contents, I opened it with `xxd`:

`xxd takiya | head -n 20`

Output (snippet):

`00000000: 6666 6666 6666 6666 6666 6666 6666 6666  ffffffff 00000010: 6666 6666 6666 6666 6666 6666 6666 6666  ffffffff 00000020: 6666 6666 6666 6666 6666 6666 6666 6666  ffffffff ...`

The entire file was full of `66` in hex (`f` in ASCII). Basically an endless block of **f’s**.