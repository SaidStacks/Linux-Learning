## 📄 Walkthrough Contents

Each level below includes:
- A short problem description
- The commands I used
- What I learned from it

---

### **Level 0** 
**Problem:** Log into the server using SSH.

**Solution:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```


---

### **Level 0 -> 1** 
**Problem:** 
To locate the password for the next level which is stored in a file called `readme` located in the home directory.

**Solution:**
```bash
pwd
ls
cat readme.txt
```
**Note:**
- ```pwd``` confirmed the current directory.
- ``ls`` showed the contents.
- `cat` displayed the password inside readme.
---

### **Level 1 -> 2** 
**Problem:** 
The password for the next level is stored in a file called `-` located in the home directory

**Solution:**
```bash
cat ./-
```
**Note:**
- Using `./-` treats it as a file name instead of an option.
- Prefixing with `./` is crucial in this case.
---

### **Level 2 -> 3** 
**Problem:** 
The password for the next level is stored in a file called `spaces in this filename` located in the home directory

**Solution:**
```bash
ls
cat "spaces in this filename"
```
**Note:**
- Quoting the file name allows the shell to treat it as one string.
- You can also escape spaces with `\.`
---
### **Level 3 -> 4** 
**Problem:** 
The password for the next level is stored in a hidden file in the `inhere` directory.

**Solution:**
```bash
cd inhere
ls -a
cat ./...Hiding-From-You
```
**Note:**
- `ls -a` reveals hidden files that start with a .
- `cat`  displays the hidden password.
---

### **Level 4 -> 5** 
**Problem:** 
The password for the next level is stored in the only human-readable file in the `inhere` directory. 

**Solution:**
```bash
file ./*
cat ./-file07
```
**Note:**
- file identifies the type of each file.
- I looked for ASCII text and then used `cat` to read it.
---

### **Level 5 -> 6** 
**Problem:** 
The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

**Solution:**
```bash
find . -type f -size 1033c ! -executable
cat ./inhere/maybehere07/.file2
```
**Note:**
- `-size 1033c` filters for size in bytes.
- `! -executable` excludes scripts or binaries.
---

### **Level 6 -> 7** 
**Problem:** 
The password for the next level is stored `somewhere on the server` and has all of the following properties:
- Owned by user bandit7
- Owned by group bandit6
- 33 bytes in size

**Solution:**
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```
**Note:**
- The command searches from the root.
- `2>/dev/null` hides permission denied errors.
---

### **Level 7 -> 8** 
**Problem:** 
The password for the next level is stored in the file `data.txt` next to the word `millionth`



**Solution:**
```bash
grep millionth data.txt
```
**Note:**
- `Grep` directly returns the line containing the password.
---

### **Level 8 -> 9** 
**Problem:** 
The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once

**Solution:**
```bash
sort data.txt | uniq -u
```
**Note:**
- `sort` groups identical lines.
- `uniq -u` filters for the unique one.
---

### **Level 9 -> 10** 
**Problem:** 
The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several ‘=’ characters.

**Solution:**
```bash
strings data.txt | grep ===

```
**Note:**
- `strings` pulls out human-readable strings.
- `grep` finds the one that looks like a password.
---

### **Level 10 -> 11** 
**Problem:** 
The password for the next level is stored in the file `data.txt`, which contains base64 encoded data


**Solution:**
```bash
base64 -d data.txt
```
**Note:**
- `base64 -d`decodes the contents and reveals the password.
---
### **Level 11 -> 12** 
**Problem:** 
The password for the next level is stored in the file `data.txt`, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Solution:**
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
**Note:**
- `tr` replaces each letter with its ROT13 counterpart.


---
### Ongoing process 
I’m continuing this journey and will update the walkthrough as I complete more levels.