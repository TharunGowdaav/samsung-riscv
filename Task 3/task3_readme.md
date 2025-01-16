*RISC-V Main Function Analysis*<br>
The code used for this compilation is give below which is a combination of finding factorial,Sum of natural numbers and fibonacci series
```
#include <stdio.h>
void factorial(int n) {
    long long fact = 1;
    printf("Factorial of %d: ", n);
    for (int i = 1; i <= n; i++) {
        fact *= i;
    }
    printf("%lld\n", fact);
}
void sum_of_natural_numbers(int n) {
    int sum = n * (n + 1) / 2;
    printf("Sum of first %d natural numbers: %d\n", n, sum);
}
void fibonacci(int n) {
    int a = 0, b = 1, temp;
    printf("Fibonacci Series: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", a);
        temp = a + b;
        a = b;
        b = temp;
    }
    printf("\n");
}
int main() {
    int n;
    printf("Enter a number: ");
    scanf("%d", &n);
    
    if (n < 0) {
        printf("Invalid input. Please enter a non-negative number.\n");
    } else {
        factorial(n);
        sum_of_natural_numbers(n);
        fibonacci(n);
    }
    
    return 0;
}
```
An in-depth analysis of RISC-V instructions from the main function of a program, including their binary encoding and functionality.
Main Function Instructions Overview

1. lui (Load Upper Immediate)
```lui     a0,0x2b
Binary: 0002b537
Breakdown:
- Immediate[31:12]: 0000000000000101011
- rd (a0 = x10): 01010
- Opcode: 0110111
```
Loads the upper 20 bits of register a0 with the immediate value 0x2b.

2. addi (Add Immediate)
```
addi    sp,sp,-32
Binary: fe010113
Breakdown:
- Immediate[11:0]: 111111100000
- rs1 (sp = x2): 00010
- funct3: 000
- rd (sp = x2): 00010
- Opcode: 0010011
```
Adds immediate value -32 to the stack pointer.

3. sd (Store Double)
```
sd      ra,24(sp)
Binary: 00113c23
Breakdown:
- Immediate[11:5]: 0000011
- rs2 (ra = x1): 00001
- rs1 (sp = x2): 00010
- funct3: 011
- Immediate[4:0]: 10000
- Opcode: 0100011
```
Stores the return address register to memory at sp+24.

4. jal (Jump and Link)
```
jal     ra,105bc
Binary: 4f8000ef
Breakdown:
- Immediate[20|10:1|11|19:12]: 010011111000
- rd (ra = x1): 00001
- Opcode: 1101111
```
Jumps to printf function and stores return address.

5. lw (Load Word)
```
lw      a0,12(sp)
Binary: 00c12503
Breakdown:
- Immediate[11:0]: 000000001100
- rs1 (sp = x2): 00010
- funct3: 010
- rd (a0 = x10): 01010
- Opcode: 0000011
```
Loads a word from memory at sp+12 into a0.

6. bltz (Branch Less Than Zero)
```
bltz    a0,1012c
Binary: 04054863
Breakdown:
- Immediate[12|10:5]: 000001
- rs1 (a0 = x10): 01010
- funct3: 100
- Immediate[4:1|11]: 01100
- Opcode: 1100011
```
Branches if a0 is less than zero.

7. mv (Move)
```
mv      a0,s0
Binary: 00040513
Breakdown:
- Immediate[11:0]: 000000000000
- rs1 (s0 = x8): 01000
- funct3: 000
- rd (a0 = x10): 01010
- Opcode: 0010011
```
Moves value from s0 to a0 (pseudo-instruction for addi).

8. ret (Return)
```
ret
Binary: 00008067
Breakdown:
- Immediate[11:0]: 000000000000
- rs1 (ra = x1): 00001
- funct3: 000
- rd (x0): 00000
- Opcode: 1100111
```
Returns from function (pseudo-instruction for jalr x0,ra,0)<br>
**Instruction Format Types in Main**<br>

###R-type: Register-to-register arithmetic instructions<br>
###I-type: Immediate arithmetic and loads<br>
###S-type: Store instructions<br>
###B-type: Branch instructions<br>
###U-type: Upper immediate instructions<br>
###J-type: Jump instructions<br>
