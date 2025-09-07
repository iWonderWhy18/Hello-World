
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


