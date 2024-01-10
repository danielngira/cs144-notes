## Registers
- %rdi
- %rsi
- %rdx
There's 16 general purpose registers

rax is the return value register

## Implementing if...else in assembly
`if (x>y)return x;`
`else return y;`

<!--x in %rdi, y in %rsi-->

`movq %rsi, %rax` <!--y -> %rax-->
`cmpq %rsi, %rdi` <!--compare x and y-->
`jle .L2`  <!--jump when x is less or equal to y-->
`movq %rdi, %rax` <!--x -> rax we are returning x-->
`.L2:`
    `ret` <!--return the value in rax which is y in this case-->`

In machine level, values are stored in a binary manner. 
There's no signed or unsigned.
11001000 when interpreted as two's complement is -56 which is 
-2^7 + 2^6 + 2^3 = -56. <!--Review lecture 0-->

## Compare two signed integers on bit level
Do a signed x-y and save the result in t
If the leading bit is 0 it is positive, if it's 1 it's negative

## Arithmetic instructions
subq, addq, andq, salq, incq...The result of this is recorded in these four flags:
- SF
- OF
- ZF
- CF
cmpq b, a computes a - b

|setl | (SF^OF)| Less(Signed)|
|----| ---- | ----|

`long less (long x, long y){`
    `return x < y;`
`}`

`cmpq %rsim %rdi` #compare x:y
`setl %al  #set` when <
`movzbq %al, %rax` #zero rest of %rax
`ret #ret val` in %rax

x = 2, y = 3
SF = 1, OF = 0

jl #Jump if less