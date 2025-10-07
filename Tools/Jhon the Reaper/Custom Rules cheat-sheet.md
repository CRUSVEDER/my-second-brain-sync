# John the Ripper — **Custom Rules** cheat-sheet (short, practical & memory-proof)

Quick intro: **Rules** are tiny programs (one-line command sequences) you put in `john.conf` (or a separate rules file) that dynamically mangle words from your wordlist so John generates variations (e.g. `Polopassword1!`) without storing huge files. Rules let you reproduce human patterns (capitalize first letter, append numbers/symbols, swap letters, etc.). ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))

---

# 1) Minimal workflow (copy-paste)

1. Edit `john.conf` (usually `/etc/john/john.conf` or `/opt/john/john.conf`). ([openwall.com](https://www.openwall.com/john/doc/CONFIG.shtml?utm_source=chatgpt.com "John the Ripper - how to customize the configuration file"))
    
2. Add a rule section header and rules, e.g.
    

```
[List.Rules:PoloPassword]
c$[0-9]$[!£$%@]
```

3. Test what that rule _produces_ without cracking:
    

```
john --wordlist=/path/to/words.txt --stdout --rules:PoloPassword | head
```

4. Use it against a hash file:
    

```
john --wordlist=/path/to/words.txt --rules:PoloPassword /path/to/hashes.txt
```

Notes: `--rules` can specify a named ruleset or `--rules:file:myrules.conf` for external files. Use `--stdout` to preview generated words. ([LabEx](https://labex.io/tutorials/kali-apply-rules-to-wordlists-for-advanced-cracking-594186?utm_source=chatgpt.com "Apply Rules to Wordlists in John the Ripper"))

---

# 2) Super-compact reference for rule parts (the stuff you’ll forget)

## Character classes (preprocessor `?[x]`)

- `?d` = digits `[0-9]`
    
- `?l` = lowercase `[a-z]`
    
- `?u` = uppercase `[A-Z]`
    
- `?a` = letters `[a-zA-Z]`
    
- `?s` = symbols (`$%^&*()-_+=|\<>[]{}#@/~`)
    
- Complement by uppercasing (e.g. `?D` = not digits). ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))
    

## Simple commands (most used)

- `:` no-op
    
- `l` → all lowercase
    
- `u` → all uppercase
    
- `c` → capitalize (first char uppercase, rest unchanged)
    
- `C` → lowercase first char and uppercase the rest
    
- `t` → toggle case of all chars
    
- `$X` → append single character `X` (use `$[0-9]` to append any digit via preprocessor)
    
- `^X` → prefix character `X`
    
- `AN"STR"` → insert string `STR` at position `N` (`Az"str"` appends string)
    
- `<N` / `>N` → reject unless length < or > N
    
- `'N` → truncate to length N
    
- `r` → reverse word
    
- `d` → duplicate (wordword)
    
- `sXY` → replace all occurrences of `X` with `Y`
    
- `[` `]` → delete first / last char
    
- `iNX` → insert char `X` at position `N`  
    (There are many more—see Openwall rules page for advanced commands.) ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))
    

---

# 3) Preprocessor / ranges — how to compactly express many rules

Write `$[0-9]$[!@]` to mean “append any digit, then append any of `!` or `@`.” The preprocessor expands such ranges into separate rules (so `password1!`, `password2!`, ..., `password9@`, etc.). Ordering is natural: right-to-left expansion. Use `\r`, `\p` backrefs for advanced sets. ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))

---

# 4) Real examples & what they do (copy/paste ready)

1. **Capitalize first char + append digit + symbol**
    

```
[List.Rules:PoloPassword]
c$[0-9]$[!£$%@]
```

- Input `polopassword` → `Polopassword1!`, `Polopassword2£`, etc. (preprocessor expands digits and symbols).
    

2. **Prefix `202` then uppercase**
    

```
[List.Rules:YearCaps]
^202u
```

- `password` → `202PASSWORD`.
    

3. **Common leet replacements** (replace `a`→`@`, `o`→`0`)
    

```
[List.Rules:Leet]
sa@sb0
```

- `sXY` replace `X` with `Y`, so `password` → `p@ssw0rd`.
    

4. **Append 2 digits**
    

```
[List.Rules:TwoDigits]
$[0-9]$[0-9]
```

- `pass` → `pass01`, `pass02`, ..., `pass99`.
    

5. **Insert `!` at end (using string insert)**
    

```
[List.Rules:AddBang]
Az"!"
```

- `secret` → `secret!`.
    

Tip: to build the Polo pattern with `Az` string syntax you'd use `cAz"1!"` only if you want to append literal `1!`. For variable digits/symbols prefer `$[0-9]` and `$[!£$%@]`. ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))

---

# 5) Testing & debugging (never skip this)

- Use `--stdout` to **preview** results:  
    `john --wordlist=words.txt --stdout --rules:PoloPassword | head -n 50`
    
- If you see duplicates or missing cases, simplify a rule and retest.
    
- If your rule line contains `[` or `]` use `\[` or `\]` or start the line with `:` to avoid preprocessor confusion.
    
- Use John’s default `Jumbo` rules to learn patterns — inspect `john.conf` around the Jumbo rules (many examples there). ([Count Upon Security](https://countuponsecurity.com/wp-content/uploads/2016/09/jtr-cheat-sheet.pdf?utm_source=chatgpt.com "JTR CHEAT SHEET | Count Upon Security"))
    

---

# 6) Where to put rules (quick)

- System (global): `/etc/john/john.conf` or `.../john.conf` depending on install. TryHackMe AttackBox often has it at `/opt/john/john.conf`. You can also create your own file and use `--rules:file:/path/to/my.rules`. ([openwall.com](https://www.openwall.com/john/doc/CONFIG.shtml?utm_source=chatgpt.com "John the Ripper - how to customize the configuration file"))
    

---

# 7) Quick mnemonic to recall main commands

Think **CUT-A-PREPEND-APPEND-CASE**:

- C (case): `l`, `u`, `c`, `C`, `t`
    
- U (undo/change chars): `sXY`, `iNX`, `oNX`, `[` `]`
    
- T (transform): `r`, `d`, `f`
    
- A (add): `^X` (prefix), `$X` (append), `AN"STR"` (insert)
    
- PREPROCESSOR (ranges): `[...]` for many choices
    

---

# 8) Common pitfalls

- Confusing `Az"..."` (literal append of whole string) vs `$[0-9]` (preprocessor expand each digit). Use `$[...]` for ranges. ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))
    
- Forgetting to test with `--stdout` — you might produce millions of candidates. Always preview. ([LabEx](https://labex.io/tutorials/kali-apply-rules-to-wordlists-for-advanced-cracking-594186?utm_source=chatgpt.com "Apply Rules to Wordlists in John the Ripper"))
    
- Using `[` or `]` unescaped in rules will trigger preprocessor behavior.
    

---

# 9) Short cheat table (for copy/paste)

```
:     = no-op
l     = lowercase all
u     = uppercase all
c     = capitalize first char
C     = lowercase first char + uppercase rest
t     = toggle case
$[0-9] = append any digit (preprocessor)
^X    = prefix char X
$X    = append char X
AN"STR" = insert STR at pos N (Az = append STR)
sXY   = replace X with Y
r     = reverse
d     = duplicate word
'N    = truncate to N
<N    = require length < N
>N    = require length > N
```

---

# 10) Final example — full scenario (Polo password)

Add to `john.conf`:

```
[List.Rules:PoloPassword]
c$[0-9]$[!£$%@]
```

Preview:

```
john --wordlist=/usr/share/wordlists/rockyou.txt --stdout --rules:PoloPassword | head
```

Then run against hashes:

```
john --wordlist=/usr/share/wordlists/rockyou.txt --rules:PoloPassword hashes.txt
```

This will try `Polopassword1!`, `Polopassword2£`, etc., for each base word. ([openwall.com](https://www.openwall.com/john/doc/RULES.shtml "John the Ripper - wordlist rules syntax"))

---

If you want, I can:

- convert this cheat-sheet into a printable 1-page PDF,
    
- generate a set of ready-to-run example rules for common corporate patterns (e.g., Capital + two digits + symbol, Year + Name variants), or
    
- inspect a rule you already wrote and tell you what it does and how many candidates it will produce.
    

Which of those would help you most right now?