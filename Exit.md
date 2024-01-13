This is a simple assembly program that exits with a success number of 0. By typing "echo $?" in the console you'll get this result after executing the program. 

Assembly programs programs start by defining a directive, In this case we define the _".section"_ directive followed by the _".data"_ argument. Here we can store datas of a certain type, like a long type, which we can then manipulate through registers   
    
###  .section .data

The next which follows is a directive related to the _".text"_ argument. This argument specifies to the assembler that this is where the executable section of the program starts, where the cpu instructions are located.

###  .section .text

Next follows a new Directive, the global one, or _".globl"_ This directive is important and tells us something very about the assembly language, which is that functions are always static, unlike other languages like C. So to make a function accessible  to the assembler and linker. Next we have the symbol "_start"_, which is the name of the functio we are going to work on. Something that may vary from assembler to assembler though, is that _"\_"_ is actually a global reference. Function following a _"\_"_ are global.

     .globl _start

Here we call the symbol "_start" again, but with a semicolon, which starts the editing section of the function 

### _start:

_"movl"_ is our first instruction to look at, _"%eax"_ our first register. The way it works is the following. First we have to think registers as  quantitized spaces, divided in by _x_ tiles, of which each has an address. In this case, _"eax"_ is called **General Purpose Register**. It is divided in 3 other registers which are _"ax, ah, al"_. Historically talking, the letter _a_ meant **accumulator**, but since IA-32 all integer registers can be used for every purpose (Base, Counter, Data, Source...). The letter _e_ stands for extended as this is a 32 bit register, the letter _x_, instead, for pair. Historically talking, back to the 8080 processor, registry could be paired up; with the 8086 processor, the letter _x_ was added to the name of the registers, therefore, from **BC** to **BX**, and so on, as these could go from 8bits to 16bits. Let's go back to our program though. _"movl"_ stands for "move long", taking 32 bits of size in account for our register. With the symbol _"$1"_ we are telling the CPU to move the number 1 in the said register. By storing 1 bit in the _"eax"_ register, we are telling the CPU, when making a system call (i.e. requesting a service from the OS) to exit from the function. 

###    movl $1, %eax

Next we have something similar, but this time using a different register, the _"ebx"_. Cutting it short, _"b"_ stands for **bsae** and in this case, giving it the number 0, will tell the system that the exit is successful. 

###    movl $0, %ebx

Lastly we have a system call which tells the system to interrupt the program by giving the immediate value (marked with _$_). The function _int_ is an interrupt signal which is sent directly to the CPU, and using the hexadecimal value 0x80 will trigger the exit from the program.

###    int $0x80
