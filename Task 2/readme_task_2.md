**RISC-V Program Simulation with Spike**</b>
This guide covers how to compile, run, and debug a RISC-V program using the spike simulator.</b>

Steps </b>
1. Compile the Program:To compile your C program, use the following command,</b>
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c </b>
```
2. Run the Program with Spike</b>
To run the compiled program with the Spike simulator:</b>
```
spike pk sum1ton.o
```
3. Debug the Program : To open the debugger,
```
spike -d pk sum1ton.o
```
4. Run Until a Specific Address :To run the program until a specific address</b>
```
until pc 100b0
```
5. Check Register Values : To check the contents of a specific register,</b>
```
reg 0 a0
```
Press Enter after each step to continue executing the program line-by-line.
