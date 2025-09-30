
---

````markdown
# Bandit & Networking Cheat Sheet (commands)

A consolidated, non-duplicated, detailed reference of commands we discussed. Each entry explains **what the tool does**, **important options**, **how to use it (examples)**, **common use-cases**, and **security / gotchas**. Use this as your primary quick-reference while doing CTFs, network troubleshooting, or system administration.

> Tip: copy/paste examples and adjust paths, hostnames, or ports to your environment. Prefer working in a temp dir (`mktemp -d`) when manipulating challenge data.
````

---

## Contents

- File handling & compression: `xxd`, `file`, `hexdump`, `tar`, `gzip`/`gunzip`, `bzip2`/`bunzip2`, `xz`/`unxz`, `zip`/`unzip`, `7z`  
- Text processing: `cat`, `less`, `head`/`tail`, `grep`, `tr`, `strings`, `sed`, `sort`, `uniq`, `base64`  
- Filesystem/permissions: `ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `chmod`, `mktemp`, `du`  
- Networking & remote access: `ssh`, `scp`, `sftp`, `openssl s_client`, `nc` (netcat), `ncat`, `socat`, `telnet`, `nmap`, `ss`, `netstat`  
- Deep dives: **nmap (NSE scripts)**, **openssl s_client — output interpretation & tests**, **socat advanced patterns**  
- Utility & helpers: `man`, `ssh-agent`/`ssh-add`, `ssh-keygen`, `xargs`, `find`, `shred`, `uname`, `whoami`

---
# File handling & compression

## `xxd` 
**What:** Hex dump tool that can create hex views of binaries and reverse (hex → binary).  
**Important flags:**
- `-p` plain hexdump (no addresses)  
- `-r` reverse (hex → binary)

**How to use / Examples:**
```bash
# make a hex dump (with addresses)
xxd data.bin | head

# create a plain hex stream (no addresses)
xxd -p data.bin > data.hex

# revert a plain hex stream back to binary
xxd -r -p data.hex > data.bin
```


**Use cases:** restoring hexdumps (CTFs), inspecting magic bytes, simple binary editing.  
**Gotchas:** when reversing, ensure the hexdump is in plain format (`-p`) or use `xxd` specific formatting.

## `file`

**What:** Guess file type by inspecting file contents (magic numbers) and other heuristics.  
**How to use / Examples:**

```bash
file data.bin
# Output might be: "gzip compressed data" or "ASCII text"
```

**Use cases:** always run on unknown binaries to choose decompressor. `file` often saves time vs guessing by extension.  
**Gotchas:** `file` is heuristic-based — for ambiguous/obscure formats also check `xxd`/`hexdump`.

## `hexdump` (and `hexdump -C`)

**What:** Another hex viewer. `-C` produces canonical hex+ASCII output similar to `xxd`.  
**Examples:**

```bash
hexdump -C data.bin | head
```

**Use:** inspect first bytes (magic), offsets; useful when `file` is inconclusive.

## `tar`

**What:** Create or extract tar archives (archive container, not compression itself).  
**Key flags:** `-c` create, `-x` extract, `-t` list, `-f` filename, `-v` verbose, `-C` change directory, `-z` gzip, `-j` bzip2, `-J` xz.  
**Examples:**

```bash
# create
tar -cvf archive.tar dir/

# extract a plain tar
tar -xf archive.tar

# extract tar.gz
tar -xzf archive.tar.gz

# extract tar.bz2
tar -xjf archive.tar.bz2
```

**Use cases:** unpack nested archives; often used together with compression tools.  
**Gotchas:** option order matters (`-xf file`); use `-C` to avoid polluting current dir.

## `gzip` / `gunzip`

**What:** Compress/decompress `.gz` files (fast, common).  
**Important flags:** `-d` decompress; `-c` write to stdout; `-k` keep original.  
**Magic bytes:** `1f 8b` at file start.  
**Examples:**

```bash
gzip file       # -> file.gz (original removed)
gunzip file.gz  # -> file
gzip -dc file.gz > out  # decompress to stdout
```

**Use cases:** general-purpose compression; common layer in multi-compressed CTF artifacts.

## `bzip2` / `bunzip2`

**What:** Compress/decompress `.bz2` files (better compression ratio than gzip, slower).  
**Flags:** `-d` decompress; `-k` keep original; `-v` verbose.  
**Magic bytes:** starts with `42 5a 68` (`BZh`).  
**Examples:**

```bash
bzip2 file
bunzip2 file.bz2
bzip2 -dk file
```

**Gotchas:** `bunzip2` may output `Can't guess original name` and create `.out` file; rename as needed.

## `xz` / `unxz`

**What:** Compress/decompress `.xz` (LZMA-based) — high compression.  
**Examples:**

```bash
xz file
unxz file.xz
```

**Use cases:** sometimes used in deep compression chains.

## `zip` / `unzip` / `7z`

**What:** `zip`/`unzip` manage zip archives; `7z` supports many formats (bzip2/xz/tar combos).  
**Examples:**

```bash
unzip archive.zip -d outdir
7z x data.bz2    # extract using 7z
```

**Use cases:** cross-platform archives; use `7z` when native tools missing or on Windows.

---

# Text processing & inspection

## `cat`

**What:** Print files to stdout or concatenate files.  
**Examples:**

```bash
cat file.txt
cat a b > combined
```

**Use:** quick view, piping into other tools. For long files use `less`.

## `less`, `more`

**What:** Pagers — view files interactively. `less` preferred (back/forward, search).  
**Examples:**

```bash
less logfile
less +F logfile   # follow like tail -f
```

## `head` / `tail`

**What:** Show beginning/end of file; `tail -f` follows appended data.  
**Examples:**

```bash
head -n 20 file
tail -n 20 file
tail -f /var/log/syslog
```

## `grep`

**What:** Search text using regular expressions.  
**Important flags:** `-i` ignore case, `-r` recursive, `-n` show line numbers, `-E` extended regex, `-o` only matching part, `-c` count matches, `--include`/`--exclude` for recursive filtering.  
**Examples:**

```bash
grep -n "password" file
grep -r --include='*.py' "TODO" ./project
```

**Use cases:** find clues, search logs, filter command output.  
**Gotchas:** quote patterns; use `-F` for fixed-string search to avoid regex pitfalls.

## `tr`

**What:** Translate or delete characters in streams.  
**Examples:**

```bash
# ROT13
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
# uppercase
tr 'a-z' 'A-Z' < file
# delete CRs
tr -d '\r' < dosfile > unixfile
```

**Use cases:** simple transformations (ROT13 decoding, removing characters).

## `strings`

**What:** Extract printable strings from binaries.  
**Examples:**

```bash
strings binary | head
strings data.bin | grep -i password
```

**Use cases:** quick reconnaissance inside binaries before heavy analysis.

## `sed`

**What:** Stream editor for substitutions, extraction, small transformations.  
**Examples:**

```bash
# print lines 1-10
sed -n '1,10p' file

# substitute globally
sed 's/old/new/g' file

# extract PEM blocks from openssl output
... | sed -n '/-----BEGIN CERTIFICATE-----/,/-----END CERTIFICATE-----/p' > cert.pem
```

**Gotchas:** complex regexes can be tricky; test on sample.

## `sort` / `uniq`

**What:** `sort` sorts lines; `uniq` filters adjacent duplicates.  
**Examples:**

```bash
sort list.txt | uniq         # dedupe (sort first if needed)
sort list.txt | uniq -c | sort -rn  # frequency sort
```

**Gotchas:** `uniq` only removes adjacent duplicates; use `sort` before `uniq` for global dedupe.

## `base64`

**What:** Encode/decode Base64.  
**Examples:**

```bash
echo 'hi' | base64
echo 'aGkK' | base64 -d
base64 -w 0 file > file.b64  # produce single-line output
```

**Notes:** Not secure encryption—only encoding.

---

# Filesystem & permissions

## `ls`, `cd`, `pwd`

**What:** `ls` lists files; `cd` changes directories; `pwd` prints working dir.  
**Examples:**

```bash
ls -la
cd /tmp
pwd
```

## `cp`, `mv`, `rm`

**What:** Copy, move/rename, and remove files.  
**Examples:**

```bash
cp ~/data.txt .
mv data.txt hexdump_data
rm -f file
```

**Gotchas:** `mv` will overwrite without prompt; use `-i` to ask.

## `chmod`

**What:** Change file modes/permissions.  
**Common use:** secure SSH key: `chmod 600 key`.

## `mktemp`

**What:** Create unique temporary file or directory.  
**Examples:**

```bash
mktemp -d               # prints new temp dir
workdir=$(mktemp -d); cd "$workdir"
```

**Why:** avoids predictable /tmp names and race conditions.

## `du`

**What:** Show disk usage.  
**Examples:**

```bash
du -sh *
du -h --max-depth=1 /var
```

---

# Networking & remote access

## `ssh`

**What:** Secure remote shell, file transfer, port forwarding.  
**Important flags:** `-p` port, `-i` identity file, `-L` local port forward, `-R` remote forward, `-C` compression, `-o` pass options.  
**Examples:**

```bash
ssh bandit12@host -p 2220
ssh -i id_rsa -p 2220 bandit14@host
ssh -L 8080:internal:80 user@bastion
ssh user@host 'uname -a'    # run command remotely
```

**Security:** always secure private keys with `chmod 600` and verify host key on first connect.

## `scp`

**What:** Secure copy (over SSH).  
**Flags:** `-P` port (capital P!), `-r` recursive.  
**Example:**

```bash
scp -P 2220 bandit13@host:sshkey.private .
```

**Gotchas:** `scp` uses `-P` (capital). `rsync` or `sftp` are alternatives.

## `sftp`

**What:** Interactive file transfer over SSH (safer alternative to scp for interactive work).  
**Example:**

```bash
sftp -P 2220 bandit13@host
# then use get/put commands inside sftp shell
```

## `openssl s_client`

**What:** TLS/SSL client for testing handshakes, retrieving server certs, and manual TLS traffic.  
**Useful flags:** `-connect host:port`, `-showcerts`, `-servername` (SNI), `-CAfile`, `-tls1_2`/`-tls1_3`.  
**Examples:**

```bash
openssl s_client -connect localhost:31790 -showcerts </dev/null
printf 'GET / HTTP/1.1\r\nHost: host\r\nConnection: close\r\n\r\n' | openssl s_client -connect host:443 -servername host
```

**Use:** certificate inspection, TLS debugging, manual HTTPS requests. End interactive session with Ctrl-D or `</dev/null` to auto-close.

### Interpreting `openssl s_client` output (quick guide)

When you run:

```bash
openssl s_client -connect host:443 -servername host
```

you'll see sections — here's what they mean:

- **CONNECTED(...)** — TCP-level connection was established.
    
- **Certificate chain** — PEM blocks printed: first is the server cert, then intermediates (if any). Use `-showcerts` to see full chain.
    
- **Server certificate** — details of the leaf certificate. Look for `subject=` (who the cert is for) and `issuer=` (who signed it).
    
- **-----BEGIN CERTIFICATE----- ...** — raw PEM blocks. Save these to a file to inspect with `openssl x509 -in cert.pem -noout -text`.
    
- **SSL handshake summary** — shows protocol version (e.g., TLSv1.2, TLSv1.3) and negotiated cipher (e.g., `ECDHE-RSA-AES256-GCM-SHA384`).
    
- **Session details** — key sizes and compression info.
    
- **OCSP / status** — if server staples OCSP, it's shown with `OCSP Response:` section (use `-status` to request).
    
- **Verify return code:** `0 (ok)` means OpenSSL could verify the chain using trusted CA roots (or verification was successful). Non-zero means verification failed (untrusted CA, expired, name mismatch).
    

**Practical commands:**

- Save certs:
    

```bash
openssl s_client -connect host:443 -showcerts </dev/null 2>/dev/null \
  | sed -n '/-----BEGIN CERTIFICATE-----/,/-----END CERTIFICATE-----/p' > certs.pem
openssl x509 -in certs.pem -noout -text
```

- Test specific TLS versions:
    

```bash
openssl s_client -connect host:443 -tls1_2
openssl s_client -connect host:443 -tls1_3
```

- Force a cipher (test server support):
    

```bash
openssl s_client -connect host:443 -cipher 'ECDHE-RSA-AES128-GCM-SHA256'
```

- Fetch a simple HTTP response over TLS (non-interactive):
    

```bash
printf 'GET / HTTP/1.1\r\nHost: host\r\nConnection: close\r\n\r\n' \
  | openssl s_client -connect host:443 -servername host
```

## `nc` (netcat)

**What:** Lightweight TCP/UDP client & server — banner grabbing, simple transfers, port checks.  
**Common flags:** `-l` listen, `-p` port (implementation-dependent), `-u` UDP, `-z` zero-I/O scan, `-v` verbose, `-w` timeout.  
**Examples:**

```bash
nc host 80
printf 'HEAD / HTTP/1.0\r\n\r\n' | nc host 80
nc -l 9001 > received.file
nc -zv host 1-1024
```

**Gotchas:** multiple `nc` variants; `ncat` is more featureful.

## `ncat`

**What:** Nmap's modern netcat with TLS, proxy and scripting features.  
**Examples:**

```bash
ncat --ssl -l 4443
ncat --ssl example.com 4443
ncat --proxy-type http --proxy proxy:3128 target 80
```

## `socat`

**What:** SOcket CAT — flexible bidirectional data relay between two addresses (files, sockets, pipes, SSL endpoints).  
**Examples:**

```bash
# simple TCP listener that runs a command for each connection
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:/bin/bash

# SSL client wrap
socat STDIO OPENSSL:remote:443,verify=0
```

**Use cases:** advanced port bridging, SSL wrapping, serial-to-socket forwarding.  
**Security:** extremely powerful; misconfiguration can expose shells to network.

### Socat advanced recipes & safety

`socat` uses address specifications of the form `TYPE:ADDRESS,options`. A few useful, practical recipes:

1. **SSL wrapper for legacy service**  
    Wrap a plaintext local service and expose it as SSL:
    

```bash
# Accept SSL connections on 8443 and forward to local HTTP 8080 (no client cert verification)
socat TCP-LISTEN:8443,reuseaddr,fork OPENSSL:127.0.0.1:8080,verify=0
```

Use-case: test an HTTPS client against a local HTTP server without changing the server.

2. **Expose a local TCP port over a remote tunnel (reverse):**
    

```bash
# On remote host run (listening) and forward to local: local-side uses - client
socat TCP-LISTEN:9000,reuseaddr,fork TCP:localhost:22
```

Caution: ensure authentication and firewall rules are correct; do NOT expose shells publicly.

3. **Serial-to-network bridge**
    

```bash
socat -d -d /dev/ttyUSB0,raw,echo=0 TCP-LISTEN:5000,reuseaddr
```

Use-case: access a serial console over the network for embedded devices.

4. **Restricted shell that only allows one command and logs**
    

```bash
socat TCP-LISTEN:4444,reuseaddr,fork SYSTEM:'echo `date` Connection from $SOCAT_PEERADDR >> /var/log/socat.log; /usr/bin/some-helpful-script'
```

**Security tips:**

- Avoid `EXEC:/bin/sh` or `EXEC:/bin/bash` exposed to internet.
    
- Use `fork` to handle multiple connections; combine with `bind`/firewall restrictions.
    
- For SSL, provide server cert/key: `OPENSSL-LISTEN:8443,reuseaddr,cert=server.pem,key=server.key` and set `verify=1` for mutual TLS when needed.
    

## `telnet`

**What:** Plaintext TCP client. Good for quick protocol testing (SMTP, HTTP) but insecure for credentials.  
**Example:**

```bash
telnet host 25
```

## `nmap`

**What:** Network mapper and port scanner with service detection and NSE scripts.  
**Important flags:** `-sS` SYN scan, `-sT` TCP connect scan, `-sU` UDP, `-p` ports, `-sV` version probe, `-A` aggressive, `-oN` output to file.  
**Examples:**

```bash
nmap -sV target
nmap -p22,80,443 target
nmap -A target
```

**Ethics:** scan only systems you own or have permission to test.

### Nmap deep dive: NSE (Nmap Scripting Engine)

NMap includes **NSE** scripts (`/usr/share/nmap/scripts/`) for tasks like banner grabs, vuln checks, auth bruteforce, HTTP enumeration, SMB checks, SSH hostkey gathering.

**How to run scripts:**

- Run a single script:
    

```bash
nmap --script http-title -p 80 target
```

- Run a category of scripts (e.g., `vuln`, `auth`, `discovery`):
    

```bash
nmap --script vuln target
```

- Run multiple scripts:
    

```bash
nmap --script "http-*,ssl-*" -p 443 target
```

**Useful NSE examples:**

- `ssl-enum-ciphers` — enumerate supported TLS ciphers:
    

```bash
nmap --script ssl-enum-ciphers -p 443 target
```

- `http-enum` — enumerate common web paths:
    

```bash
nmap --script http-enum -p 80 target
```

- `ssh-hostkey` — fetch SSH host keys:
    

```bash
nmap --script ssh-hostkey -p 22 target
```

- `vulners` (if installed) — vulnerability checks via feeds:
    

```bash
nmap --script vulners -sV target
```

**Interpreting NSE results:**

- Script output is printed under the port/service section. It may show additional details, warnings, or CVE references.
    
- Use `-oN` or `-oX` to save output for later analysis.
    
- _Performance:_ running many scripts can be slow — scope targets and scripts appropriately.
    

## `ss` / `netstat`

**What:** Show active sockets and listening ports. `ss` is the modern replacement for `netstat`.  
**Examples:**

```bash
ss -tuln          # list listening TCP/UDP ports
ss -tulpn | grep :22  # show process using port 22
# legacy
netstat -tuln
```

**Use:** find services bound to ports, troubleshoot connections.

---

# Utilities & helpers

## `man`

**What:** Read the manual for commands. Use `man <command>` and `man -k <keyword>`.

## `ssh-agent`, `ssh-add`, `ssh-keygen`

**What:** manage SSH keys and fingerprints.  
**Examples:**

```bash
eval "$(ssh-agent -s)"
ssh-add sshkey.private
ssh-keygen -lf sshkey.private   # prints fingerprint
```

**Use:** avoid repeatedly entering passphrases, inspect key details.

## `find`

**Use:** find files by name, size, age; combine with `-exec` or `xargs` to process results.

## `xargs`

**What:** build command lines from stdin.  
**Example:**

```bash
find . -name '*.log' -print0 | xargs -0 grep -H "ERROR"
```

## `shred`, `rm`

**What:** remove files. `shred -u` overwrites multiple times before deleting (not perfect on all filesystems).

## `uname`, `whoami`, `pwd`

**What:** system/user context helpers.

---

# Quick magic numbers (file signatures)

- **gzip:** `1F 8B`
    
- **bzip2:** `42 5A 68` (`BZh`)
    
- **zip:** `50 4B 03 04` (`PK..`)
    
- **tar (ustar):** `75 73 74 61 72` at offset 257 (ASCII `ustar`)
    
- **png:** `89 50 4E 47`
    
- **pdf:** `%PDF-`
    

---

# Typical Bandit repair workflow (concise, no duplicates)

```bash
# 1) make a safe working directory
workdir=$(mktemp -d /tmp/bandit.XXXXXX); cd "$workdir"

# 2) copy & rename original hexdump
cp ~/data.txt .; mv data.txt hexdump_data

# 3) revert hexdump -> binary
xxd -r -p hexdump_data > data.bin
file data.bin
hexdump -C data.bin | head

# 4) decompress based on `file` output or magic bytes; repeat until plain text
# (examples)
mv data.bin data.gz; gunzip data.gz; mv data data.bin; file data.bin
mv data.bin data.bz2; bunzip2 data.bz2; mv data data.bin; file data.bin
mv data.bin data.tar; mkdir extracted; tar -xf data.tar -C extracted; # inspect extracted

# 5) when `file` prints "text", show it
cat data.bin
```

---

If you want this exported as a downloadable **plain `.md`** or **`.txt`** file, or converted to a **PDF**, tell me which format and I will prepare it.  
If you want deeper examples (like a sample `nmap` reconnaissance playbook, or step-by-step `openssl s_client` output annotation for a real server output you paste), paste the output and I’ll walk through it line-by-line.

```

---

Would you like the file saved and provided as a download (Markdown `.md`), plain text `.txt`, or converted to a PDF?
```