# PES_ASIC_CLASS
This Repository Guides you to complete ASIC flow from scratch (FACULTY : Mahesh Awati, GUIDE : Kunal Ghosh)

## The COURSE files are present under those respective day folders 

### Solutions to frequenty occuring errors are in Error_solution.md

## Install the Prerequisites(for ubuntu)

```
sudo apt update
sudo apt upgrade
chmod +x run_ubuntu.sh
./run_ubuntu.sh
```
The installed contents will be available at ~/riscv_toolchain

# Introduction
### Flow : HLL -> ALP -> Binary -> (HDL) -> GDS
#### 1. HLL -> High level language (c , c++) 
- A high-level programming language is a type of programming language that is designed to be more human-readable and user-friendly compared to low-level languages like assembly or machine code.

#### 2. ALP -> Assembly level program
- Assembly language is a low-level programming language that is closely related to the architecture of a specific computer's central processing unit (CPU). Assembly language programs are written using mnemonic codes that represent specific machine instructions which the machine can understand.

#### 3. HDL -> Hardware Description Language
- It is a specialized programming language used for designing and describing digital hardware circuits. HDLs allow engineers to model and simulate complex digital systems before physical implementation, aiding in the design and verification of integrated circuits and FPGA configurations.
- Verilog, System Verilog, VHDL

#### 4. GDS -> Graphic Data System (layout)
- Format used in the semiconductor industry to represent the layout and design of integrated circuits at a highly detailed level. GDSII files contain information about the geometric shapes, layers, masks, and other essential details that make up the physical layout of a chip.
- Tools : Klayout, Magic

##### The Hardware needs to understand what the Application software is saying it to do.This relation can be eshtablished by System Software

____System Software____
- OS : Operating System : Handles IO, memory allocation, Low level system function
- Compiler : Convert the input to hardware dependent instruction
- Assembler : Convert the instructions provided by compiler to Binary format
- HDL : A program that understands the Binary pattern and map it to a netlist
- GDS : Layout

# lab classes 
<details>
  <summary> Week 1 </summary>
  <br>
  <details>
    <summary> DAY 1: Introduction to RISCV ISA and GNU Compiler Toolchain </summary>
    <br>
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
  
  ## For the signed number 
  
  ![Screenshot from 2023-08-21 01-28-57](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/2efbf598-7a24-4f71-a3ba-6a7bc3d41d35)
  
  ## After running the compiler
  
  ![Screenshot from 2023-08-21 01-28-48](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/0c63fe28-1cc8-476e-adfd-9387bd020663)
  
  
  ### The commands for above porcess are:
  
  ```
  vim signedHighest.c
  riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signedHighest.o signedHighest.c
  spike pk signedHighest.o
  ```
  </details>

  <details>
  <summary> DAY 2 : Introduction to ABI and Basic Verification Flow </summary>
  <br>
  
  ## Lab work using ABI function calls
  
  ### Download the load.S , 1to9_count.c files from 
  https://github.com/kunalg123/riscv_workshop_collaterals/tree/master/labs
  
  
  ```
  cat 1to9_custom.c
  cat load.S
  ```
  
  ### The above commands are used to view the content of the files on terminal
  
  ![Screenshot from 2023-08-21 01-49-31](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/4ec9fd68-5f28-4043-9571-f610346eff63)
  
  
  ![Screenshot from 2023-08-21 09-11-11](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/674d5a42-c54d-4803-94a1-0e2276a6dd91)
  
  ![Screenshot from 2023-08-21 09-10-32](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3bd596ac-744e-4925-9f45-b27a44eab3b5)
  
  ### Command used :
  
  ```
  riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.S
  spike pk 1to9_custom.o
  riscv64-unknown-elf-objdump -d 1to9_custom.o | less
  ```
</details>
  
</details>

<details>
  <summary> Week 2 </summary>
  <br>
 <details>
    <summary> Day 1 - Introduction to Verilog RTL design and Synthesis </summary>
     # installation process
    ## For ubuntu
   
    ```
    sudo apt-get install git
    git clone https://github.com/kunalg123/vsdflow.git
    cd vsdflow
    chmod 777 opensource_eda_tool_install.sh
    ./opensource_eda_tool_install.sh 
    **NOTE for freshers : This has been tested on a fresh UBUNTU installtion
    **NOTE for experienced UNIX users : It has lot of sudo apt-get and sudo remove commands, so you might want to review           before running
    ./vsdflow spi_slave_design_details.csv
    ./vsdflow picorv32_design_details.csv
    ```
  </details>

  <details>
    <summary> Day 2 </summary>
  </details>
</details>

