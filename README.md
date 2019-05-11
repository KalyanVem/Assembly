# Assembly Language
There are many programming languages that can convert human-readable instructions to machine language i.e, binary. Then why do we need an assembly language? What is an assembly language?

Assembly language is a low-level programming language, which gives access to many details. This is the language that both CPU and human can understand. Different processors have different assembly language like x86. It is the 32bit version of the language that I am writing about. Let us see What are Registers and their purpose, Function calls, Functions in x86 assembly language.

## Registers
Processor's main task is to process the data. In order to achieve this, the processor has to store the data in memory and it is processed from the memory. This brings loads of stress to the processor. So, in order to avoid this, the processor comes with the pre-installed type of storage called Registers. The registers are capable to store data in them. But, there are a limited set of registers in a processor as they are very expensive. Registers are broadly three types. General purpose, Control registers, Segment registers.

###### Control Registers
Control registers are CR0, CR1, CR2, CR3, CR4. Control registers helps CPU in performing certain calculations.

###### Segment Registers
Segment are the places in the programme that contains data, code, stack. There are three main segments.

###### Code segment
Contains all the instructions that are to be executed.
```
section .text
   <or>
segment .text
```
###### Data Segment
It contains data, constants and work area.
```
section .data
   ;or
segment .data
   ;and
section .bss
   ;or
segment .bss
```
data segment is represented by .data and .bss. .data contains the variables that are predeclared and cannot be altered throughout the execution. in small, it is static. Whereas .bss is also static, but the data can be declared later in the programme.

###### Stack Segment
It contains data and return addresses of functions and local variables.

## General Purpose Registers
Intel assembly has 8 general purpose 32-bit registers. These are generally used for various calculations that happens inside the CPU.

```
EAX is a general purpose register. EAX is used to store operands and data of results.

EBX is a base register. It is used to store the pointers to the data.

ECX is generally known as counter register. It is used as a function parameter or a loop counter.

EDX is a data register that is used as an Input/Output pointer.

ESI is a Source Index and EDI is a Destination Index are also data pointer registers. They are also used for various memory operations. more generally used for string operations.

ESP points to the top of the Stack.

EBP is a base pointer. it is used to reference all the function parameters and local variables.

EIP holds the address of the next address that is to be executed.

EFLAGS are used to infer about the various executions are happening. For example, a zero flag is set if the execution of instruction results in zero. If two numbers are added, the zero flags (ZF) is set. there are many flags. Few of the flags are,

OverFlow Flag(OF): This flag is set if the result of arithmetical operation causes the overflow of the Most Significant Bit.

ZeroFlag (ZF): This flag is set if the result of an arithmetical operation results in zero.

Sign Flag (SF): This flag is set if the result of an arithmetical operation is Negative.

Carry Flag (CF): This flag is set if when the value is to be carried out during arithmetical operations like addition and division.

Parity Flag (PF): This flag is set if the result of an Arithmetical operation contains the Odd number of ‘1’-bits. It is set to 0 if the result contains even number of ‘1’-bits.
```
### STACK
A stack is an abstract data type. It grows from higher addresses to lower memory addresses. Arguments that are passed to the function are stored in a stack. We can also store local variables are stored in the stack. A stack of one programme is unique that it cannot be used by other functions. The stack contains two main operations PUSH and POP. Push inserts an element to the top of the stack whereas pop eliminates the element that is on the top of the stack. This is depicted as LAST IN FIRST OUT. Yes, the last element that enters the stack by using push operation is the one which gets eliminated by the pop operation. This can be easily understood from the below Image.


### Functions
By the time of execution, functions are frequently set up with a stack frame. When a function is called, it creates a stack frame. And if another function is called, a new stack frame corresponding to the second function is created at the current esp location over the first function's stack. the stack frames of both the functions must not overlap. It must be made sure that no other stacks manipulate the content of the other functions. The stack is deallocated before the function returns.

### Function Prologue
Function prologue is a few lines of code that appears at the beginning of the function. it is responsible for prepare a stack frame and registers for use within the function. Usually, prologue pushes base pointer on to the stack. and we assign the value of stack pointer. This creates a new stack frame on top of the old one.
```
push ebp
mov ebp, esp
```
### Function Epilogue
Function epilogue appears by the end of the programme. it is responsible to set stack and registers to the previous state i.e, the state before the function is called. It reverts the stack pointer to the current base pointer freeing the space reserved to the prologue and local variables. We pop the base pointer at the end so as to restore the stack pointer to the place where it is before the prologue.
```
mov esp, ebp
pop ebp
```
this can be simplified by giving the following.
```
leave               ;mov and pop
ret                 ;exits the function.
```
