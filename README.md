# Custom CPU V2

This project is a continuation of my [custom CPU](https://github.com/KingstumusPrime/Custom-CPU-V1/). It was a bit of a "CPU Jam," with me making the CPU in three days, the PPU in three more, and spending one or two days wrapping things up. Instead of following a tutorial, I wrote this one completely from scratch with no outside resources. It taught me a lot more about CPU architecture, and I was finally able to sync everything to the clock, something I had a lot of trouble with on the first CPU. I also learned a lot more about staying organized and tried naming my components and tying debug output to most of the registers. This one also had a PPU, which I had a ton of fun making.

## Specs

[CPU specs]() | [PPU specs]()

### CPU

The CPU can be found in CPUV3; this is the most functional out of all of them and includes some basic 16-bit functionality (though it is rather forced to the point where I would not recommend it).

#### Features
* Two Registers: A & X
* 8-bit RAM (technically 4 to help with lag)
* Carry, Zero, and Negative flags
* 16-bit program ROM
* 16-bit jumps



#### Instructions<br/>

X   : ILLEGAL OPCODE<br/>
@   : MEM WRTE<br/>
$   : CONSTANT<br/>
" " : Mem Value<br/>

=========== A<br/>
LDA $  0x04<br/>
LDA    0x06<br/>
ADC $  0x05<br/>
ADC    0x07<br/>
SBC $  0x0D (value plus 1)<br/>
SBC    0x0F (value plus 1)<br/>
ADC @$ 0x01 X (stores result at P1)<br/>
SBC @$ 0x09 X (stores result at P1)<br/>
STA @  0x03<br/>
NOT $  0x0C<br/>
NOT    0x0D<br/>
NOP    0x02<br/>
=========== 8 bit jump<br/>
JMP $  0x10<br/>
BCA $  0x11<br/>
BZE $  0x12<br/>
BNE $  0x13<br/>
NOP $  0x14<br/>
BNC $  0x15 (Branch not carry)<br/>
BNZ $  0x16 (BRANCH not zero)<br/>
BPO $  0x17 (Branch if positive)<br/>
CLC    0x19<br/>
SEC    0x1D<br/>
CLZ    0x1A<br/>
SEZ    0x1E<br/>
CLN    0x1B<br/>
SEN    0x1F<br/>
=========== X<br/>
LDX $  0x24<br/>
LDX    0x26<br/>
ADX $  0x25<br/>
ADX    0x27<br/>
SBX $  0x2D<br/>
SBX    0x2F<br/>
ADX @$ 0x21 X (stores result at P1)<br/>
SBX @$ 0x29 X (stores result at P1)<br/>
STX @  0x23<br/>
TAX @  0x2C (two bytes long P1 ignored)<br/>
=========== 16 bit jump<br/>
JMP $  0x30<br/>
BCA $  0x31<br/>
BZE $  0x32<br/>
BNE $  0x33<br/>
NOP $  0x34<br/>
BNC $  0x35 (Branch not carry)<br/>
BNZ $  0x36 (BRANCH not zero)<br/>
BPO $  0x37 (Branch if positive)<br/>

#### bit-by-bit

Bit 1: send selected register to ALU
Bit 2: send the second value to ALU (0 Param1, 1 Ram)
Bit 3: write location (0 RAM, 1 A)
bit 4: invert selected register
bit 5: jump instructions (see below)
bit 6: register select (0 A, 1 X)

#### Jump instructions (when bit 5 is set):
Bits 1-2: flag select (0 unconditional, 1 carry, 2 zero, 3 negative)
Bit  3: invert condition
Bit  4: Set the selected flag to the value in bit 3.

### PPU

The PPU can be found in the circuit titled "ppu". You can see an example of it connected to a CPU in the full build. 

> NOTE: this CPU in full build has some huge bugs given the speed of the CPU and lack of an emulator it is recomended to ignore this PPU as a programmer

To communicate with the PPU, use the upper three bits of the RAM address, then write the value. You can write to the PPU just like you would write to RAM. The PPU is capable of drawing simple glyphs to the screen, with the first 26 containing the alphabet, the next 10 being numbers, and the rest being blank.

### Explanation

V: the value being written to the PPUs RAM.
W: basic write flag
A: the address in video memory you want to write to (3 bits wide)



