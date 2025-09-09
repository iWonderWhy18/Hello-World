
Wargames

---

Level0

Answer:

```powershell
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**bandit.labs.overthewire.org**, port 2220
Username: bandit0
password: bandit0

---

Level1

```powershell
cat readme
```
Answer: 
```powershell
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

**bandit.labs.overthewire.org**, port 2220
Username: bandit1
Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

---

Level2

```powershell
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

Read files with a dash as its name
```powershell
cat ./-
```

Username: bandit2
Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

---

Level 3

```powershell
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

```powershell
cat ./"--spaces in this filename--"
```

Username: bandit3
Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

---

Level4

```powershell
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

```powershell
cat ...Hiding-From-You
```

Username: bandit4
Password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

---

Level5

# Bandit Level 4 → Level 5

## Level Goal

The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html)



```
-file00 = ��w��f�y�k��KSv�m�/��DGo��XI'
-file01 = �v��`�Rg.��v0>Oh        �]r�թ�i�L_ �L
-file02 = ����J��x"�.x�����l�x��m
-file03 = |�g򸌎�TU��uhjaW1���dS>�G��yc
-file04 = YQ�P��P���;�z�[;��ն�ë␦␦�
-file05 = ����o�xv��y�0lkG�N��J4"��R&�
-file06 = 1D��d
     ��M�l���1��nq�)�й
-file07 = ��M�l���1��nq�)�й
	4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
-file08 = 2;��ɸd$7_�n�F   9�����'uڢ��i
-file09 = I���0�V�;C r��A<D�t����`�
```

```python

bandit4@bandit:~/inhere$ xxd ./-file00
00000000: a0e9 9e77 07bc ec66 92d6 0879 c16b a2ba  ...w...f...y.k..
00000010: 4b53 76f0 6daa 2fe1 e544 476f b5af 5849  KSv.m./..DGo..XI
00000020: 27            


bandit4@bandit:~/inhere$ hexdump -C ./-file00
00000000  a0 e9 9e 77 07 bc ec 66  92 d6 08 79 c1 6b a2 ba  |...w...f...y.k..|
00000010  4b 53 76 f0 6d aa 2f e1  e5 44 47 6f b5 af 58 49  |KSv.m./..DGo..XI|
00000020  27                                                |'|
00000021

```

```powershell
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

```powershell
bandit4@bandit:~/inhere$ cat -- -file07
```

Username: bandit5
Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

---

# Bandit Level 5 → Level 6

## Level Goal

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html)

```python
bandit5@bandit:~/inhere/maybehere07$ cat -- .file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

```python
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

Username: bandit6
Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

```powershell
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

---

# Bandit Level 6 → Level 7

## Level Goal

The password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html) , [grep](https://manpages.ubuntu.com/manpages/noble/man1/grep.1.html)

```python
find / -type f -user bandit7 -group bandit6

Result:
/var/lib/dpkg/info/bandit7.password
```


Cat the file result below
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

Username: bandit7
Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

```powershell
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

---
# Bandit Level 7 → Level 8

## Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Commands you may need to solve this level

[man](https://manpages.ubuntu.com/manpages/noble/man1/man.1.html), grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

```powershell
ssh bandit7@bandit.labs.overthewire.org -p 2220
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

```python
bandit7@bandit:~$ grep 'millionth' data.txt
millionth   dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

---
# Bandit Level 8 → Level 9

## Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Helpful Reading Material

- [Piping and Redirection](https://ryanstutorials.net/linuxtutorial/piping.php)

```python
bandit8@bandit:~$ sort data.txt | uniq -u

dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---
# Bandit Level 9 → Level 10

## Level Goal

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd


```python
grep -a '==' data.txt
```

```
ssh bandit9@bandit.labs.overthewire.org -p 2220

Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

---

# Bandit Level 10 → Level 11

## Level Goal

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Helpful Reading Material

- [Base64 on Wikipedia](https://en.wikipedia.org/wiki/Base64)

```python
ssh bandit10@bandit.labs.overthewire.org -p 2220

FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

```python
cat data.txt
```

![[Pasted image 20250909101122.png]]

The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

---
# Bandit Level 11 → Level 12

## Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Helpful Reading Material

- [Rot13 on Wikipedia](https://en.wikipedia.org/wiki/ROT13)



```python
ssh bandit11@bandit.labs.overthewire.org -p 2220

dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

```python
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt

ITuyVUOup3A3o3WxVTymVTE0HwR3Z2MnF2VjHyWmERMGE3AaZyWKoaOBIzbmpIWlPt==
```

🔍 Breakdown of the Command

tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt

- `'A-Za-z'`: This defines the **input character set** — all uppercase (`A-Z`) and lowercase (`a-z`) letters.
- `'N-ZA-Mn-za-m'`: This defines the **output character set**, which is the input set **rotated by 13 positions**.

🔁 How the Rotation Works

🔡 Uppercase Letters:

- Input: `A B C D E F G H I J K L M N O P Q R S T U V W X Y Z`
- Output: `N O P Q R S T U V W X Y Z A B C D E F G H I J K L M`

So:

- `A` → `N`
- `B` → `O`
- ...
- `M` → `Z`
- `N` → `A`
- ...
- `Z` → `M`

🔠 Lowercase Letters:

- Input: `a b c d e f g h i j k l m n o p q r s t u v w x y z`
- Output: `n o p q r s t u v w x y z a b c d e f g h i j k l m`

So:

- `a` → `n`
- `b` → `o`
- ...
- `m` → `z`
- `n` → `a`
- ...
- `z` → `m`

🧠 Why It’s 13 Positions

The alphabet has 26 letters. ROT13 splits it in half:

- First 13 letters shift forward by 13
- Last 13 wrap around to the beginning

This makes ROT13 its own inverse — applying it twice returns the original text.

---
# Bandit Level 12 → Level 13

## Level Goal

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

## Helpful Reading Material

- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)


```python
ssh bandit12@bandit.labs.overthewire.org -p 2220

ITuyVUOup3A3o3WxVTymVTE0HwR3Z2MnF2VjHyWmERMGE3AaZyWKoaOBIzbmpIWlPt==
```