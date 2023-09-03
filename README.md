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



# Lab Classes 

# Week 1

<details>
  <summary> Day 1 - Introduction to RISCV ISA and GNU Compiler Toolchain </summary>
  <br>

  # DAY-1: LAB work for RISC-V software toolchain
  ## Task 1
  
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
  
  
  
  ## Task 2
  
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
  <summary> Day 2 - Introduction to ABI and Basic Verification Flow </summary>
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

# Week 2

<details>
  <summary> Day 1 - Introduction to Verilog RTL design and Synthesis</summary>
  <br>

  ## Installation of vsdflow 

  ```
  sudo apt-get install git
    git clone https://github.com/kunalg123/vsdflow.git
    cd vsdflow
    chmod 777 opensource_eda_tool_install.sh
    ./opensource_eda_tool_install.sh 

    **NOTE for freshers:** This has been tested on a fresh Ubuntu installation.
    **NOTE for experienced UNIX users:** It has a lot of `sudo apt-get` and `sudo remove` commands, so you might want to 
      review before running.

    ./vsdflow spi_slave_design_details.csv
    ./vsdflow picorv32_design_details.csv
  ```

  ### Steps to test 'vsdflow' on Ubuntu

  ```
    cd outdir_spi_slave
    qflow display spi_slave
  ```

  ## Task 1


  ## Installing sky130RTLDesignAndSynthesis
  ```
    sudo -i
    sudo apt-get install git
    cd /home
    ls  
    cd shashank
    mkdir VLSI
    git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git    
  ```
  ![Screenshot from 2023-08-27 14-40-07](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/9acda0e5-e202-460e-8383-56832879a9cc)

  ### After installation the VLSI dir should have these files in order 
  ![Screenshot from 2023-08-27 15-15-44](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/07e2eecd-db77-415f-8c2a-ff78687382fb)


  ## Introduction iverilog gtkwave part1
  ```
    sudo -i
    cd /home
    ls
    cd shashank
    cd VLSI
    cd sky130RTLDesignAndSynthesisWorkshop
    cd verilog_files
    ls
  ```

  ### In this current dir all the verilog files are present with their testbench
  ### Load a mux and it's testbench into iverilog 
  
  ![Screenshot from 2023-08-27 16-17-07](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/b871819e-aa6d-489f-ba5c-911d0398f801)

![Screenshot from 2023-08-27 16-17-41](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/0490ef3d-7f7b-4b1b-9b65-0f06b657e42c)

  ### After the output is generated then execute the .vcd file in the simulator

  ```
  gtkwave tb_good_mux.vcd
  ```

![Screenshot from 2023-08-27 16-19-54](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3c87a8d7-83f8-494a-a182-d1488f312531)

![Screenshot from 2023-08-27 16-20-09](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/68209088-0179-4e87-aa21-7e704ecbd3b2)

![Screenshot from 2023-08-27 16-29-42](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/f182a6ab-efcf-4dca-84c3-92a3d2dfc366)
  
  ```
  vim tb_good_mux.v -o good_mux.v 
  ```
  
  ## Task 2

  ## Labs using Yosys and Sky130 PDKs

  ### Content of good_mux.v and tb_good_mux.v
  
  ![Screenshot from 2023-08-28 13-44-27](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6a65eed9-0161-4107-b913-8d4427e057ca)



## Invoke yosys
![Screenshot from 2023-08-28 13-48-48](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/429395be-d38c-4629-ba7c-b83d5ecfdc3c)

give the commands as mentioned below
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![Screenshot from 2023-08-28 13-52-02](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/9b68f04e-7936-4e3a-89da-f010f7005fa2)

![Screenshot from 2023-08-28 13-52-45](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/a393c247-a38c-47e9-939c-3cadf4e6dcf2)

![Screenshot from 2023-08-28 13-53-47](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/9de8304b-a43d-4cb3-a17e-ea344581b7d2)

![Screenshot from 2023-08-28 13-56-31](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/fbea9c3b-6359-4eac-a1a7-22189bd5b418)

![Screenshot from 2023-08-28 13-57-32](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/452f42b0-ac12-40db-a6f2-d52d371898fb)


### Write a netlist for the verilog code 
![Screenshot from 2023-08-28 14-06-54](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/dab4c2ac-4d54-4599-95d4-5c3a84be51e2)

![Screenshot from 2023-08-28 14-08-01](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/ef532e18-84e9-4f0a-bc95-663819259efd)

![Screenshot from 2023-08-28 14-09-37](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/d7ea4dc6-4433-4caa-8a1b-ca9aba881a7b)

![Screenshot from 2023-08-28 14-09-47](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/2bb5b2ba-e035-4758-aff3-a98ab5020710)

</details>

<details>
  <summary> Day 2 - Timing libs, hierarchical vs flat synthesis and efficient flop coding styles </summary>
  <br>

  ## Introduction to .lib

## Task 1
### Command to invoke sky130_fd_sc_hd__tt_025C_1v80.lib file 

```
 vim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![Screenshot from 2023-08-28 14-13-38](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/346d173e-0be2-4ccb-99f5-1db98cdcb35c)

![Screenshot from 2023-08-28 14-15-59](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/4614462b-c8f6-4a7e-9bba-8d78f114f3cc)

![Screenshot from 2023-08-28 14-16-09](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/85c5d97a-c92b-4772-8c97-765c3c4ba4a1)

![Screenshot from 2023-08-28 14-18-04](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/96232c45-5a0a-496d-9d4c-c8dccfbda9b0)

## Task 2
## Hier synthesis flat synthesis 

### In this section we will be using the multiple_modules.v
### The commands used are :
```
vim multiple_modules.v
yosys
read_liberty -lib ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
```
![Screenshot from 2023-08-28 14-20-26](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3ce00e90-0d99-4fac-a458-533f3e7a53de)

![Screenshot from 2023-08-28 16-51-43](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/b89671b4-5066-40a3-8278-cdd6dbd7b544)

![Screenshot from 2023-08-28 16-52-28](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6f8da149-1f00-49be-a35d-e4f4bcc5d71e)

![Screenshot from 2023-08-28 16-52-40](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3dede933-5b7c-4d13-b5c8-964ca1994087)

![Screenshot from 2023-08-28 16-53-18](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6457e149-8118-4204-b6dd-d580b3c2f1ce)

```
write_verilog multiple_modules_hier.v
!vim multiple_modules_hier.v 
```
![Screenshot from 2023-08-28 17-54-14](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/41fad2d2-310f-43d1-a8e0-ac6c8848a2d4)

![Screenshot from 2023-08-28 17-55-32](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/a23db2a1-b896-4bb6-a39b-7111a2e5e0cb)


![Screenshot from 2023-08-28 17-55-41](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/94a217d3-4e5b-4523-b36c-615c816f985e)

```
write_verilog -noattr multiple_modules_hier.v
!vim multiple_modules_hier.v 
```

![Screenshot from 2023-08-28 17-56-51](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/d70420b9-a04b-4965-a3b9-79bf6bfbfcad)


![Screenshot from 2023-08-28 17-57-01](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/b10ee0a6-b6b1-4feb-b05a-a692b5962210)


## Task 3

## Various Flop Coding Styles and optimization

### For asynchronous reset

```
ls
ls *dff*
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd 
```

![Screenshot from 2023-08-28 19-42-00](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/20c1df08-e42a-4ffc-ab44-322b16e15c9c)

![Screenshot from 2023-08-28 19-42-21](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/ea55aa6a-0d11-425f-9830-e557f29ae744)


### For asynchronous set

```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

![image](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/7c2f104e-7808-4a2d-82c6-35de7d76b8e4)


### For synchronous reset

```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd 
```

![Screenshot from 2023-08-28 19-53-29](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/8c85eb64-bbdf-4fb8-b8c1-32ed3bfecfe8)



## Task 4

### Now to synthesize all the 3 codes as mentioned above we use yosys
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-08-28 19-58-30](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/13a263c8-d9ad-4300-aae7-c551c7449588)

![Screenshot from 2023-08-28 19-58-39](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6ef9bfbd-cc97-4161-ae42-6e745a084291)


```
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib//sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-08-28 20-03-35](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/57a85d0c-12da-4bba-bd34-67dbba42566f)

![Screenshot from 2023-08-28 20-04-15](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6bbe419d-7f0f-4b29-a22c-ed2fa0050b9b)


```
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-08-28 20-07-42](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/10b51a53-df18-457e-9849-6ba0a21425bf)

![Screenshot from 2023-08-28 20-07-36](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/7159396b-e347-4a92-8530-d2d2cd08f57e)

## Interesting optimisations part1
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-08-29 19-21-21](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6bbb1f7e-af4b-4104-9695-c126fa5f976e)

![Screenshot from 2023-08-29 19-25-20](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/3dde5354-f6cd-40db-af54-9fb390c594cf)

## Interesting optimisations part2

```
write_verilog -noattr mul2_net.v
show
```
![Screenshot from 2023-08-29 19-51-02](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/b7ecb74c-cfb7-4755-81d9-9feb11e72a69)

![Screenshot from 2023-08-29 19-53-28](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/fd70e96a-d1fe-4515-a90a-74b4c4855667)


```
read_verilog mult_8.v
synth -top mul8
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult8_net.v
show
```

![Screenshot from 2023-08-29 19-56-10](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/1f390b9d-9789-45cf-aa9c-fa1398da723b)

![Screenshot from 2023-08-29 19-59-20](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/2314a63e-3107-474a-9da3-0616976ac978)

![Screenshot from 2023-08-29 19-59-33](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/1cae9df1-dbcd-4596-b207-0d94e5c9da38)

</details>


<details>
  <summary> Day 3 - Combinational and sequential optmizations </summary>
  <br>
  
  ## Task 1  Combinational logic optimizations

  ![Screenshot from 2023-08-29 20-29-18](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6ecec5d4-0aa5-46f2-a098-e2f8e1fe6ec5)

  ### Commands
  
  ```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog opt_check.v
  synth -top opt_check 
  opt_clean -purge
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
  read_verilog opt_check2.v
  synth -top opt_check2
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  show
  ```
  
  ![Screenshot from 2023-09-03 10-02-01](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/df68275d-3089-4d88-9bd6-aed2753fd9fa)
  
  ![Screenshot from 2023-09-03 10-03-58](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/79c8fdcf-1973-4546-aa62-2eef7be2b1be)


  ### Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
read_verilog opt_check4.v
synth -top opt_check4
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```


![Screenshot from 2023-09-03 10-10-02](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/f9df9b6c-23e0-483d-85e3-5229fbd26024)

![Screenshot from 2023-09-03 10-11-19](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/790b9f99-b57d-4d08-9676-3bdfc916fd61)


## Task 2  Sequential logic optimizations


![Screenshot from 2023-09-03 10-30-00](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/a4e9e107-4843-4efa-8164-0c9e3d81237c)


![Screenshot from 2023-09-03 10-31-07](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/e70925ad-d766-4a99-95dd-23e9bf0fcbd7)

### Synthesis

```
vim dff_const1.v -o dff_const2.v
iverilog dff_const1.v  tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
iverilog dff_const2.v  tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd 
```


![Screenshot from 2023-09-03 10-33-52](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/f2a54282-a82b-45ab-a2cd-0a61c02ff67a)

![Screenshot from 2023-09-03 10-35-01](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/6685cbcc-6b9b-4358-a51b-fe77e9f39091)

### Synthesis

```
yosys

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-09-03 10-40-09](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/34ee59d9-e558-439b-ba3d-37079b3218d8)

### Synthesis

```
read_verilog dff_const2.v
synth -top dff_const2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-09-03 10-43-56](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/9b0519e7-bc23-463a-a51e-396eb5c09d4a)


### Gtkwave

```
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd 
```

![Screenshot from 2023-09-03 10-46-37](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/a0aac26d-5510-4011-9113-f2ac2e4c9f12)

### Synthesis

```
yosys
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-09-03 11-35-22](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/9607832e-15c1-415c-aba3-66eb3924972f)


# Task 3  Sequential logic optimizations for unused outputs 

### synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog  counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2023-09-03 11-42-25](https://github.com/Shashanksharma280201/PESU-ASIC/assets/79470436/46334447-a8d2-4378-b66f-de71c351e279)





</details>
