# DAY-1: LAB work for RISC-V software toolchain
# Task 1

## Write a C program to compute sum from 1 to n
![Screenshot from 2023-08-19 11-20-30](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3ee921a8-140c-4353-aac7-104b2f6c5168)

### The result for the above after gcc compilation 
![Screenshot from 2023-08-19 11-20-59](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/d89ef2d4-9315-4643-957c-63d027004a1b)

### commands used 
```
gcc sum1ton.c
./a.out
```

## GCC compile And Disassemble 

![Screenshot from 2023-08-21 00-52-48](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/0033f39e-f64d-439c-965b-2c9185d6bdc3)
![Screenshot from 2023-08-21 00-45-38](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6b067ff8-dada-4462-b6ec-2647c6690a94)


### Commands used to compile and get the outout
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o | less

riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o | less
```
![Screenshot from 2023-08-21 00-56-27](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/0a321df3-eb8e-4eda-be6d-2d651332630a)


## Spike Simulation And Debug

### commands to run the risc-v compiler and spike debugger 
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
spike pk sum1ton.o
spike -d pk sum1ton.o
```

### The outputs after running the above commands are:

![Screenshot from 2023-08-21 01-03-17](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/08502c60-1b52-43d1-b24f-06bed6d8a44f)


![Screenshot from 2023-08-21 01-07-25](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6ab2a91e-47d9-4a3d-984a-82a3c50bb404)




# Task 2

## Write a C program for Signed And Unsigned Numbers 

![Screenshot from 2023-08-21 01-19-18](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/0b1c01e9-04df-4c78-97ba-6675715996ba)

## After running the compiler

![Screenshot from 2023-08-21 01-20-43](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/ba0825a6-1319-4d7a-a3ec-95b8ebdd2168)

### The commands for above porcess are:
```
vim unsignedHighest.c
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c
spike pk unsignedHighest.o
```
