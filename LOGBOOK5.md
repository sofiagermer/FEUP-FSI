## Task 1

We ran both binaries and as expected in both cases a shell was invoked.

[Logbook 5 - Task 1](/screenshots/logbook5-task1.png)

## Task 2

We successfully compiled the file. First using the commands given and then using the makefile.

[Logbook 5 - Task 2](/screenshots/logbook5-task2.png)

## Task 3

After debugging the program as suggested, we obtained the distance between the buffer's starting position and the position of the ebp (0xFFFFCA48-0xFFFFC9DC=0x6C=108).

[Logbook 5 - Task 3 - Part 1](/screenshots/logbook5-task3-1.png)

We chose the last bytes to place the shell code (start=517-length of the shell code).

As suggested, to get the buffer address, we included a printf in the stack.c code.

The offset is 108+4 because the return address is always at ebp+4.

To get our new return address, we added our offset (108 + 4) to the address of the buffer, plus 4 bytes (the space needed to write our 32 bit address). We could've added more bytes, since our shell code is located at the end of the 517 bytes.

[Logbook 5 - Task 3 - Part 2](/screenshots/logbook5-task3-2.png)

After running our exploit we ran the stack-L1 program and verified that the exploit had worked because the shell was invoked (see attached image).

[Logbook 5 - Task 3 - Part 3](/screenshots/logbook5-task3-3.png)

## CTF

### Challenge 1

First we analysed the program, and found that a 28 character long string was being written into a string variable with an allocated memory of only 20 characters. By inputting 20 random characters followed by "flag.txt", we were able to overwrite the contents of the meme_file variable and consequently access the contents of the flag.txt file.

### Challenge 2

The difference from the 1st challenge, was that in the second challenge, changing the value of meme_file variable wasn't enough. First we needed to overwrite a flag variable so that the content of the flag was 0xfefc2122, and only after that, could we overwrite the meme_file variable with the path to the flag file (flag.txt). In order to do this we wrote a python script that creates a 32 byte array (32 is the length scanned by the program), placed the flag after the 20 bytes used to fill the buffer and immediately after we placed the flag's path ("flag.txt").

Here is the script we wrote:

```python
#!/usr/bin/python3
from pwn import *
import sys

N=32
content = bytearray(0x0 for i in range(N))
number  = 0xfefc2122
content[20:24]  =  (number).to_bytes(4,byteorder='little')
content[24:32] = ("flag.txt").encode('latin-1')
DEBUG = False

if DEBUG:
    r = process('./program')
else:
    r = remote('ctf-fsi.fe.up.pt', 4000)

r.recvuntil(b":")
r.sendline(content)
r.interactive()
```