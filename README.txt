Brian Lee
3620101
brianslee@umail.ucsb.edu

CMPSC 177 - Homework 4

Problem 1:
The secret phrase is CS177isawesome! I found this by setting breakpoints at the location for the main and authenticate functions.
Then, I used 'info r' to find the ebp value, which was 0xbffffc48. Using 'disas main', I found the target address that I wanted the function to return to,
which was 0x08048650, which was the location right after the else if statement in main. The 'disas authenticate' command helped me find the size of the buffer,
which was 0x15 or 21 in decimal. So, I set my buffer killing password as a series of 21 'A's, the ebp, and the target address, the latter two in little endian format.

However, as this gave me garbage, I switched from 0x41 to 0x60, which got me the proper output.

Problem 2a:
I created a SHELLCODE environment variable using the 'export SHELLCODE="(shellcode here)"' command. Then, I used gdb to find the address of the code, the command
'x/s *((char **)environ+1)' got me the address of the variable, at least in gdb. In actuality, it was a few bytes smaller. From there, I overloaded the buffer again with
enough '0x60's to fill the 92 byte offset. After that, I set the ebp to the edp of main, which was 'bffffc18'.
In summation: my buffer killer password was 92 '0x60s' followed by the ebp followed by the address of the environment variable.

Note: This is unreliable, as it stopped working after my first attempt.

Problem 2b:
I did the same thing as in 2a, except I used 21 '0x60's instead of 92.

Same note applies.
