# Linux Basics

**Week:** 1 ·
<br>**Tools:** Linux, Ubuntu Desktop, Oracle VirtualBox, Bash, OverTheWire Bandit

## Goal

To learn Linux fundamentals through YouTube, freeCodeCamp, Ubuntu installation, and OverTheWire Bandit exercises.

## What I did

- I watched YouTube, freeCodeCamp — Introduction to Linux – Full Course for Beginners.
- I installed Ubuntu Desktop in Oracle VirtualBox.
- I played OverTheWire exercises Level 0–10.

## OverTheWire Bandit Notes

### Level 0

**Username:** bandit0

**Password:** bandit0

**Command:**

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### Level 0 to Level 1

**Goal:** Find the password in the readme file.

**Commands:**

```bash
ls
cat readme
```

### Level 1 to Level 2

**Goal:** Find the password in the /- file (stdin/stdout).

**Commands:**

```bash
ls -la
find
du
cat /home/bandit1/-
```

Such files require full file path to open them.

### Level 2 to Level 3

**Goal:** Find the password in the --spaces in this filename--

**Commands:**

```bash
ls -la
find
du
cat /home/bandit2/'--spaces in this filename--'
```

Such files require the quotations to open them.

### Level 3 to Level 4

**Goal:** Find the password in the hidden file.

**Commands:**

```bash
ls -la
find
du
cat ...Hiding-From-You
```

Such files require the cat and followed by file name to open them.

### Level 4 to Level 5

**Goal:** Find the password in the folder 'inhere' but with 9 other '-files'.

**Commands:**

```bash
ls -la
find
du
cat -- -file00
```

I checked files from `-file00` to `-file09` and then I chose the readable strings.

Such files require the cat and followed by -- then filename inorder to open them.

### Level 5 to Level 6

**Goal:** Find the password in the folder 'inhere' with some characteristics but with 20 other files and each file has other children too.

**Commands:**

```bash
ls -la
find
du
find inhere -type f -size 1033c ! -executable
```

Then:

```bash
cat inhere/maybeinhere07/.file2
```

Such files require find command to locate the needed folder that match the criteria then cat command to open it.

### Level 6 to Level 7

**Goal:** Find the password stored somewhere in the server with specified characteristics.

**Commands:**

```bash
ls -la
find
du
grep
find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
```

Then cat the given file location.

Such files require find command to locate the needed folder that match the criteria then cat command to open it.

The `2>/dev/null` is for hiding the permission denied messages.

### Level 7 to Level 8

**Goal:** Find the password stored in a file data.txt with millions of data and its next to word millionth.

**Commands:**

```bash
ls -la
find
du
grep
grep "millionth" data.txt
```

Only grep is needed here, its the simplest way, its syntax is `grep "word" filename`.

### Level 8 to Level 9

**Goal:** Find the password stored in a file data.txt with millions of data and it is the only line of text that occurs only once.

**Commands:**

```bash
grep
sort
uniq
strings
base64
tr
tar
gzip
bzip2
xxd
sort data.txt | uniq -u
```

`sort data.txt` sorts the data in alphabetically order.

`|` is a pipeline symbol that directs the output of `sort data.txt` to the next command.

`uniq -u` finally prints only the data that appears once.

### Level 9 → Level 10

**Goal:** Find the password in readable text inside a binary file.

**Command:**

```bash
strings data.txt | grep "=="
```

**Skills learned:**

- Extracting readable text using strings
- Searching output using grep
- Combining commands with pipes

### Level 10 → Level 11

**Goal:** Decode Base64 data to reveal the password.

**Command:**

```bash
base64 -d data.txt
```

**Skill learned:**

- Decoding Base64-encoded text in Linux.
