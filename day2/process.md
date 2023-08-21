# Day 2: Introduction to ABI and basic verification flow

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
