+++
title = "ARM32 Assembly On Android"
date = "2022-07-14"
author = "KutKut"
description = "This is a short blog about how to write arm assembly on android"
+++

Hello, and welcome to my blog about writing "Hello World" in ARM assembly on an Android device!

First, let's briefly review what ARM assembly is. 

ARM stands for Advanced RISC Machine, which is a type of processor architecture commonly used in mobile devices and other embedded systems. 

Assembly language is a low-level programming language that directly corresponds to machine code, which is the binary code that actually executes on the processor. So, by writing assembly code, we can control the behavior of the processor and perform various tasks on the device.

To get started, you will need an Android device or emulator with an ARM processor, and a text editor or IDE to write your code. I will be using the Termux app, which provides a Linux terminal environment on Android.

Now, let's open up the terminal and create a new file for our assembly code. I will use the command "vi hello.s" to create a file called "hello.s" and open it in the vim text editor.

In this file, we will write the assembly code to print out "Hello World" to the terminal. Here is the code:

```

/* hello world in arm assembly */

.global _start
_start:
  MOV R7, #4       @ Syscall number
  MOV R0, #1       @ Stdout is monitor
  LDR R1,=hello    @ string located at hello:
  MOV R2, #12      @ string is 19 chars long
  SWI 0            @ ask linux to exit the program

_exit:
  MOV R7, #1      @ Syscall exit 
  MOV R0, #0      @ Return 0
  SWI 0           @ Software interrupt

.data
hello:
  .ascii "Hello World\n"

```

Let's go through this code line by line. Firstly, we declare a global symbol called "_start", which is the entry point of our program.

Inside the "_start" function, we first use syscall for using the moniter and tell where we found that with R0

Next, we move the lenght of the characters into R2 and load the address of the "hello" string into the register R0 using the "ldr" instruction. This instruction loads the data at the memory address specified by its operand, in this case the symbol "hello".

After that, we use _exit label to exit the program.

The "hello" string is defined after the "_exit" label using the ".ascii" directive. This directive allows us to define a string of characters directly in our code.

Now that we have written our code, let's assemble and link it using the commands 
```
as hello.s -o hello.o
ld hello.o -o hello 
``` 
These commands invoke the assembler and linker tools to produce an executable file called "hello".

Finally, we can run the program using the command "./hello", and we should see the output "Hello World" printed to the console!

That's it for this blog on writing "Hello World" in ARM assembly on Android. I hope you found it informative and helpful. Stay tuned for more blogs about programming and technology!
