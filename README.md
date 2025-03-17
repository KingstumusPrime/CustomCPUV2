# Custom CPU V2

This project is a continuation to my [custom CPU](https://github.com/KingstumusPrime/Custom-CPU-V1/). Instead of following a tutorial I wrote this one completly from scratch like no google for the week from scratch. That being said I took a lot of inspiration from the 6502 and NES for the CPU/PPU.

## Specs

### CPU

The CPU can be found in CPUV3 this is the most functional out of all of them and includes some basic 16 bit functionality (though it is rather forced to the point where I would not recomend it).

#### Features
* Two Registers A & X
* 8 Bit ram (technically 4 to help with lag)
* Carry, Zero, and Negitive flags
* 16 bit program rom
* 16 bit jumps

#### Instructions

X   : ILLEGAL OPCODE
@   : MEM WRTE
#   : CONSTANT
" " : Mem Value

=========== A
LDA #  0x04
LDA    0x06
ADC #  0x05
ADC    0x07
SBC #  0x0D (value plus 1)
SBC    0x0F (value plus 1)
ADC @# 0x01 X (stores result at P1)
SBC @# 0x09 X (stores result at P1)
STA @  0x03 
NOT #  0x0C
NOT    0x0D
NOP    0x02
=========== 8 bit jump
JMP #  0x10
BCA #  0x11
BZE #  0x12
BNE #  0x13
NOP #  0x14
BNC #  0x15 (Branch not carry)
BNZ #  0x16 (BRANCH not zero)
BPO #  0x17 (Branch if positive)
CLC    0x19
SEC    0x1D
CLZ    0x1A
SEZ    0x1E
CLN    0x1B
SEN    0x1F
=========== X
LDX #  0x24
LDX    0x26
ADX #  0x25
ADX    0x27
SBX #  0x2D
SBX    0x2F
ADX @# 0x21 X (stores result at P1)
SBX @# 0x29 X (stores result at P1)
STX @  0x23 
TAX @  0x2C (two bytes long P1 ignored)
=========== 16 bit jump
JMP #  0x30
BCA #  0x31
BZE #  0x32
BNE #  0x33
NOP #  0x34
BNC #  0x35 (Branch not carry)
BNZ #  0x36 (BRANCH not zero)
BPO #  0x37 (Branch if positive)

#### bit-by-bit

Bit 1: send selected register to ALU
Bit 2: send second value to ALU (0 Param1, 1 Ram)
Bit 3: write location (0 ram, 1 A)
bit 4: invert selected register
bit 5: jump instructions (see below)
bit 6: register select (0 A, 1 X)

#### Jump instructions (when bit 5 is set):

Bits 1-2: flag select (0 unconditional, 1 carry, 2 zero, 3 negitive)
Bit  3: invert condition
Bit  4: Set selected flag to value in bit 3




