# custom-assembler
This repository provides an assembler written in Python for a simulated CPU in Logisim, enabling the conversion of custom assembly code into machine code.

## Getting started
### Clone:
`git clone https://github.com/Kenoalpe/custom-assembler.git`

### Change directory:
`cd asm-compiler-excercise`

### Get required packages (Linux):
1. Create a virtual environment:
   1. [venv in pycharm](https://www.jetbrains.com/help/pycharm/creating-virtual-environment.html)
2. Move into **venv**:
   1. `source venv/bin/activate`
3. Install requirements:
    1. `python3 -m pip install -r requirements.txt`

### Run:
`python3 -m app`

# How to use
It is important to notice that the output this Assembler only works for a special CPU made for this Projekt.

## Writing an Assembler File
To use the Assembler you'd have to write an Assembler File names `asm.txt` containing your Instructions for your CPU Programm.

This perticular Assembler supports the following Instructions:
| Instruction     | Definition      |
| ------------- | ------------- |
| NOP           | No Operation; does Nothing and moves on to the next Instruction after one CPU Cycle|
| INPUT    | Reads data from the external Input Field ans writes into register A|
| Output | Copies content from register A to the output bus, where its displayed in hex format |
| JMP `<adress>` | Jumps to <address> adress in  RAM  |
| LOAD A,#<value> | Loads a constant <value> value in register A |
| LOAD A,<adress> | Loads a value from `<adress>` address of the RAM in register A |
| INC A | Increments register A by 1 |
| INC B | Incrementes register B by 1 |
| MOV B,A | Copies contents of register A into register B |
| ADD A,B | Calculates the **sum** of contens of register A and register B and writes the result in register A | 
| SUB A,B | Calculates the **difference** of register A and register B and writes the result in register A |
| AND A,B | Does a bitwise **and** of contents of register A and register B and writes the result in register A |
| OR A,B | Doas a bitwise **or** of contents of register A and register B and writes the result in register A |
| ISEQUAL | Checks if content of register An and register B is the equal and writes the result in register A (0h if equal, else not equal) |
| JMPEQ <address> | Jumps to `<address>` adress in RAM if contents of regsiter A and register B are the same |
| STORE <address> | Stores the content of register A at `<address>` adress in the RAM
| DB <value> | Definies a byte in  RAM |
| EQU <value> | Defines a constant |
| RESB <number> | Reserves number of `<number>` of bytes in RAM |

You can also place comments. They beginn with a `;` and end at the end of the line
```asm
; This is a comment
INPUT ; this is a comment too 
MOV B,A ;this is also a comment 
```

Additionally you can use `Labels` to acess your values and constants and define jump markers, like this
```asm
myByteAdress: DB 45h ; Places a 0x45 at the position of this labeln in the RAM; can be used for instruction with a address parameter
myConstant: EQU 34h ; Definies a constant 34h at the position of this labeln in the RAM; can be used for instructions with a value paramter
revervedBytes: RESB 5 ; Definies 5 bytes; can be used for instruction with a address parameter, points to the first byte 
```

Now you can generate the machine code via `python 3 -m app`
This generates an output `machine-code.txt` file.
You can now copy the contents of this file and paste them into your RAM of your Logisim CPU.
