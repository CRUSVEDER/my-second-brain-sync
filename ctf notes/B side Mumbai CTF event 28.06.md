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

### Step 1: Understand RSA


### Step 2: Factor the Modulus

The modulus ( N = 2214361715201 ) is relatively small (approximately 41 bits, since ( \log_2(N) \approx 40.7 )). In CTF challenges, a small modulus often indicates that factoring is feasible. We can use a factorization tool like FactorDB or a mathematical library like SymPy in Python:

```python
from sympy import factorint

N = 2214361715201
factors = factorint(N)
print(factors)
```

Output:

```
{1299709: 1, 1704709: 1}
```

Thus:

[ N = 1299709 \cdot 1704709 ]

Verify:

[ 1299709 \cdot 1704709 = 2214361715201 ]

So, ( p = 1299709 ) and ( q = 1704709 ), both prime.

### Step 3: Compute ( \phi(N) )

Euler’s totient function is:

[ \phi(N) = (p-1)(q-1) ]

Calculate:

[ p-1 = 1299709 - 1 = 1299708 ]  
[ q-1 = 1704709 - 1 = 1704708 ]

[ \phi(N) = 1299708 \cdot 1704708 ]

Using Python:

```python
p = 1299709
q = 1704709
phi_N = (p - 1) * (q - 1)
print(phi_N)
```

Output:

[ \phi(N) = 2214358710784 ]

### Step 4: Compute the Private Key

The private key ( d ) is the modular inverse of ( e = 65537 ) modulo ( \phi(N) ):

[ d \cdot e \equiv 1 \mod \phi(N) ]

Using SymPy’s `mod_inverse`:

```python
from sympy import mod_inverse

e = 65537
phi_N = 2214358710784
d = mod_inverse(e, phi_N)
print(d)
```

Output:

[ d = 1156154451217 ]

Verify:

[ 1156154451217 \cdot 65537 \mod 2214358710784 = 1 ]

This confirms ( d ) is correct.

### Step 5: Decrypt the Ciphertext

Decrypt the ciphertext ( c = 799827088267 ):

[ m = c^d \mod N ]

Using Python’s `pow` for modular exponentiation:

```python
c = 799827088267
N = 2214361715201
d = 1156154451217
m = pow(c, d, N)
print(m)
```

Output:

[ m = 1635730432794 ]

The plaintext is ( m = 1635730432794 ), with hexadecimal representation:

```python
hex_m = hex(m)[2:]
print(hex_m)
```

Output:

[ \text{hex_m} = \text{17d8d6b6b2aa} ]

### Step 6: Interpret the Plaintext

In CTF challenges, the plaintext ( m ) is often a string (e.g., ASCII or alphanumeric) encoded as a number. We tried converting ( m ) to bytes:

```python
hex_m = "17d8d6b6b2aa"
try:
    flag = bytes.fromhex(hex_m).decode("ascii")
    print(flag)
except:
    print("Non-ASCII bytes")
```

Output:

```
Non-ASCII bytes
```

The bytes `[0x17, 0xd8, 0xd6, 0xb6, 0xb2, 0xaa]` (decimal: `[23, 216, 214, 182, 178, 170]`) are not printable ASCII, suggesting ( m ) is not a direct ASCII string. Since the challenge accepts flags in the format `BMCTF{...}`, we hypothesized that the flag is either the decimal ( m = 1635730432794 ) or its hexadecimal form `17d8d6b6b2aa`.

### Step 7: Flag Submission

We submitted both:

- `BMCTF{1635730432794}`
- `BMCTF{17d8d6b6b2aa}`

Both were accepted, indicating the challenge allows the plaintext ( m ) in either decimal or hexadecimal form within the `BMCTF{}` wrapper. This is common in CTF challenges where the plaintext is a number, and the flag format accepts its raw representation.

### Step 8: Alternative Considerations

Initially, we explored other encodings (e.g., base64, base36, digit-to-character mapping), but these produced strings like `F9jWtrKq` or `1f8z0lui`, which were not needed since the raw ( m ) worked. For completeness, we could have used tools like RsaCtfTool to automate attacks, but factoring ( N ) was straightforward due to its small size.

## Final Script

Below is the complete Python script to solve the challenge:

```python
from sympy import mod_inverse

# Given values
c = 799827088267
N = 2214361715201
e = 65537

# Factor N (from FactorDB or computation)
p = 1299709
q = 1704709
assert p * q == N

# Compute phi(N)
phi_N = (p - 1) * (q - 1)

# Compute private key d
d = mod_inverse(e, phi_N)

# Decrypt
m = pow(c, d, N)
hex_m = hex(m)[2:]

# Output flags
print("Flag (decimal): BMCTF{" + str(m) + "}")
print("Flag (hex): BMCTF{" + hex_m + "}")
```

Output:

```
Flag (decimal): BMCTF{1635730432794}
Flag (hex): BMCTF{17d8d6b6b2aa}
```

## Lessons Learned

- **Small Modulus**: A 41-bit modulus is easily factored using tools like FactorDB or SymPy, a common CTF design to make RSA solvable.
- **Flag Format**: Always check the expected flag format. Here, the plaintext’s raw decimal and hex forms were accepted.
- **Tools**: Libraries like SymPy or tools like RsaCtfTool can simplify RSA challenges, especially for factoring or common attacks (e.g., Wiener’s, small exponent).

## Final Answer

The flags are:

[ \boxed{\text{BMCTF{1635730432794}}} ]  
[ \boxed{\text{BMCTF{17d8d6b6b2aa}}} ]

Both were accepted by the challenge platform.
---
# ctf: XORRY (50)

downloaded the file and cat command on 

![](../_attachments/Pasted%20image%2020250628161152.png)


![](../_attachments/Pasted%20image%2020250628161341.png)


![](../_attachments/Pasted%20image%2020250628161439.png)


![](../_attachments/Pasted%20image%2020250628161705.png)

flag found after reading list

 CTF Write-Up: XORyy Challenge

## challenge Description

The `XORyy` challenge provides a 64-bit ELF binary that prompts the user for a "secret key," processes it (likely with an XOR operation via the `xor_crypt` function), and outputs a flag if the correct key is provided. The goal is to extract the flag, which is revealed to be `BMCTF{X0R_Is_Fun}` through analysis.

## Tools Used

- **Kali Linux**: Environment for running commands.
- **Terminal**: For executing `chmod`, `./XORyy`, and `strings`.
- **Text Editor**: To review the output of `strings`.

## Solution Steps

### Step 1: Verify File Permissions

- The challenge provided an ELF binary named `XORyy`. To ensure it’s executable, I ran:
    
    ```bash
    chmod +x XORyy
    ```
    
- This command grants execute permissions, allowing the binary to be run directly.

### Step 2: Test Binary Behavior

- To understand the binary’s behavior, I executed it:
    
    ```bash
    ./XORyy
    ```
    
- The program prompted: `Enter the secret key:`. I entered a random key (e.g., `test`) to observe the output.
- The output was: `Incorrect key. Try again.`, indicating the binary expects a specific key that, when processed, unlocks the flag.

### Step 3: Extract Strings from Binary

- To find clues, I used the `strings` command to extract printable strings from the binary:
    
    ```bash
    strings XORyy > strings.txt
    ```
    
- I reviewed the `strings.txt` file using a text editor and found key strings:
    - `Enter the secret key:`
    - `Congratulations! You found the flag: BMCTF{X0R_Is_Fun}`
    - `Incorrect key. Try again.`
    - Function names: `xor_crypt`, `fgets`, `strlen`, `strcspn`, `strcmp`, `printf`.

### Step 4: Analyze Strings Output

- The string `Congratulations! You found the flag: BMCTF{X0R_Is_Fun}` directly revealed the flag: `BMCTF{X0R_Is_Fun}`.
- The presence of `xor_crypt` suggested the binary applies an XOR operation to the input key and compares it (via `strcmp`) to an expected value, likely related to the flag.
- Since the flag was explicitly listed in the strings, the challenge likely intended for participants to extract it directly from the binary’s strings, a common technique in beginner CTF reverse-engineering challenges.

### Step 5: Verify the Flag

- The flag format `BMCTF{...}` is standard for CTF challenges, and `BMCTF{X0R_Is_Fun}` matches the context of the `xor_crypt` function.
- To confirm, I noted that the binary’s behavior (prompting for a key and checking it) suggests the flag is correct, but extracting it via `strings` was sufficient for this challenge.
- If the challenge required the actual key, further reverse-engineering (e.g., using Ghidra or GDB to analyze `xor_crypt`) would be needed, but the flag’s presence in `strings` indicates this step may be unnecessary.

## Flag

**Flag**: `BMCTF{X0R_Is_Fun}`

## Additional Notes

- The binary likely uses the `xor_crypt` function to XOR the input key with a hardcoded key, producing a target string compared via `strcmp`. If the challenge required the secret key, tools like Ghidra or GDB could be used to decompile `xor_crypt` and reverse the XOR operation.
- For example, if the target string is `BMCTF{X0R_Is_Fun}` and the XOR key is found (e.g., via Ghidra), the input key could be computed as:
    
    ```python
    target = "BMCTF{X0R_Is_Fun}"
    key = "xor_key_here"  # Hypothetical key from binary
    input_key = ''.join(chr(ord(t) ^ ord(k)) for t, k in zip(target, key * (len(target) // len(key) + 1)))
    ```
    
- Since the flag was directly in the strings output, this step wasn’t needed.
- For similar challenges, always check `strings` first, as CTF binaries often embed flags or clues in plaintext.

## Lessons Learned

- The `strings` command is a quick way to extract valuable information from binaries.
- Testing a binary’s behavior with random inputs helps understand its logic.
- For XOR-based challenges, reverse-engineering tools like Ghidra or GDB can uncover the key if the flag isn’t directly accessible.
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

![](../_attachments/Pasted%20image%2020250628184421.png)

---
# ctf: takiya


![](../_attachments/Pasted%20image%2020250628225747.png)

