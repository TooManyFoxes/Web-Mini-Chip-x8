There are 6 Registers (0 - 5) , 2 flags, 256 Bytes of ROM and Memory, and 112 bytes of
video memory.

Each byte is 8 pixels in video memory. The top left of the screen is byte 1, and the
bottom right of the screen is byte 112. These bytes are read horizontally, meaning
"01101100" at byte 0,  "10000001" at byte 4, and "01111110" at byte 8 would display as

⬛⬜️⬜️⬛⬜️⬜️⬛⬛
⬜️⬛⬛⬛⬛⬛⬛⬜️
⬛⬜️⬜️⬜️⬜️⬜️⬜️⬛

The CPU runs 28 instructions per second. 28 instructions = 28 cycles.

28 cycles = 1 second.

The CPU accepts 16 different user inputs. 0-9 and q,w,e,a,s, and d.

CPU Order of Operations per cycle: -----

Updates Inputs.
Run operation.
Render screen.

The compiler compiles the inputs as follows:

0 - 9 : binary equvilent
q: 00001010
w: 00001011
e: 00001100
a: 00001101
s: 00001110
d: 00001111

Operations are case-sensitive and must be written in lowercase.

Comments must be started with a "//". There are no multi-line comments.

When writing code, only numbers and binary are used. For example, a binary number written would be
b10101010, but you could write it as 170. These value formats are the only formats allowed. However, this rule does
not apply to operations so dont write the actual byte for the operation code!

-----

OF - Set to 1 if the last math operation resulted in an overflow.
VC - Set to 1 if the last render operation resulted in a pixel being overwritten.
ZR - Set to 1 if the last math operation resulted in a zero.

-----


00000000:
Null - NUL
1 Byte

Do nothing.

-----

11110000:
Jump - JMP
2 Bytes

Jumps to the location in read-only memory determined by the
second byte.

-----

11110001:
Jump if Register Equals - JRE
4 Bytes

Jumps to the location in read-only memory determined by the
second byte if the contents of the register dictated by the 3rd byte is exactly
the contents of the register dictated by the fourth byte.

-----

11110010:
Jump if Carry- JCC
2 Bytes

Jumps to the location in read-only memory determined by the
second byte if the Overflow flag is 1.

-----

11110011:
Jump if Zero- JCZ
2 Bytes

Jumps to the location in read-only memory determined by the
second byte if the Zero flag is 1.

-----

11110100:
Jump if Input- JCI
3 Bytes

Jumps to the location in read-only memory determined by the
second byte if the input determined by the third byte is active. To
check for any input, set the third byte to 11111111.

-----

11111111:
Halt - HLT
1 Byte

Stops the program.

-----

00000001:
Write Byte - WBM
3 Bytes

Writes the second byte to the memory location determined by the
third byte.

-----

00000010:
Read Byte - RBR
3 Bytes

Reads the byte stored in the memory location determined by the second byte and writes it to the register determined by the third byte.

-----

00000011:
Move Byte - MMB
3 Bytes

Moves the byte at the location in memory determined by the second byte to the location in memory determined by the third byte.

-----

00000100:
Swap Byte - SMB
3 Bytes

Swaps the byte at the location in memory determined by the second byte with the location in memory determined by the third byte.

-----

00000101:
Check Register - IFR
4 Bytes

Reads the byte in the register determined by the second byte, if the byte is
exactly the third byte, the program counter will be set to the fourth byte.

-----

00000110:
Bitwise AND - BWA
4 Bytes

Does a bitwise AND operation with the second and third byte, then stores the result in the register location determined by the fourth byte.

-----

00000111:
Bitwise OR - BWO
4 Bytes

Does a bitwise OR operation with the second and third byte, then stores the result in the register location determined by the fourth byte.

-----

00001000:
Bitwise XOR - BWX
4 Bytes

Does a bitwise XOR operation with the second and third byte, then stores the result in the register location determined by the fourth byte.

-----

00001001:
Bitwise NOT - BWN
3 Bytes

Does a bitwise NOT operation with the second byte, then stores the result in the register location determined by the third byte.

-----

00001010:
Bit shift Left - BSL
4 Bytes

Shifts the bits in the second byte left the amount determined by the third byte, then stores the result in the memory location determined by the fourth byte.

-----

00001011:
Bit shift Right - BSR
4 Bytes

Shifts the bits in the second byte right the amount determined by the third byte, then stores the result in the memory location determined by the fourth byte.

-----

00001100:
Write to Register - WBR
3 Bytes

Writes the second byte to the register determined by the third byte.

-----

00001101
Read from register to memory - RFR
3 Bytes

Writes the contents of the register determined by the second byte to the location in memory determined by the third byte.

-----

00001110:
Add Immediate - ADI
4 Bytes

Adds the second and third byte together, storing the result in the register
determined by the fourth byte. If the addition resulted in an overflow, the overflow flag will be set to 1.

-----

00001111:
Subtract Immediate - SBI
4 Bytes

Finds the difference between the second byte and the third byte, storing the result in the register
determined by the fourth byte. If the subtraction resulted in an overflow, the overflow flag will be set to 1.

i.e: result = byte2 - byte3.

-----

00010000:
Multiply Immediate - MUI
4 Bytes

Multiplies the second byte and the third byte, storing the result in the register
determined by the fourth byte. If the multiplication resulted in an overflow, the overflow flag will be set to 1.

-----

00010001:
Divide Immediate - DVI
5 Bytes

Divides the second byte by the third byte, storing the result in the register
determined by the fourth byte. Note that this operation will set the overflow flag to 0 regardless of the result.

To store the ceiling of the result, the fifth byte must be 1, to store the floor of the result, the fifth byte must be 0.

i.e: result = byte2 / byte3.

-----

00010010:
Add Registers - ADR
4 Bytes

Adds the contents of the register determined by the second byte with the contents of the register determined by the third byte. Then store the result in the register determined by the fourth byte. If the addition resulted in an overflow, the overflow flag will be set to 1.

-----

00010011:
Subtract Registers - SBR
4 Bytes

Finds the difference between the contents of the register determined by the second byte and the contents of the register determined by the third byte , storing the result in the register determined by the fourth byte. If the subtraction resulted in an overflow, the overflow flag will be set to 1.

i.e: result = byte2 - byte3.

-----

00010100:
Multiply Registers - MUR
4 Bytes

Multiplies the contents of the register determined by the second byte and the contents of the register determined by the third byte , storing the result in the register determined by the fourth byte. If the multiplication resulted in an overflow, the overflow flag will be set to 1.

-----

00010101:
Divide Registers - DVR
5 Bytes

Divides the contents of the register determined by the second byte by the contents of the register determined by the third byte , storing the result in the register determined by the fourth byte. Note that this operation will set the overflow flag to 0 regardless of the result.

To store the ceiling of the result, the fifth byte must be 1, to store the floor of the result, the fifth byte must be 0.

i.e: result = byte2 / byte3.

-----

00010110:
Write Register Clone - WRC
3 Bytes

Write the contents of the register determined by byte 2 to the contents of the register 
determined by byte 3. 


-----

00010111:
Write Register Dictated - WRD
3 Bytes

Write the contents of the register determined by byte 2 to the memory address determined by the contents of the register determined by byte 3.

-----

00011000:
Write Memory Influenced - WMI
3 Bytes

Write to a register dictated by byte 2 with the contents of the memory
address dictated by byte 3.

-----

00011001:
Random Number - RAN
2 Bytes

Write a random number between 0 - 255 to the register dictated by byte 2.

-----

00011010:
Load Counter from Register - LCR
2 Bytes

Overwrite the program counter with the contents of the register dictated by
the second byte.

-----

00011011:
Write Counter to Register - WCR
2 Bytes

Write the current program counter to the register dictated by the second byte.


-----

00011100:
Read from Video Memory to Memory - RVM
3 Bytes

Read video memory byte determined by byte 2 to memory address determined
by byte 3.

-----

00011101:
Write to Video Memory Immediate - WVI
3 Bytes

Write a byte to video memory address dictated by byte 3.

-----

00011110:
Write to Video Memory Register - WVR
3 Bytes

Write the contents of a register dictated by byte 2 to the video memory address
determined by byte 3.

-----

00011111:
Pause Program for register Cycles - PPC
2 Bytes

Pause the program for the amount of cycles determined by the second byte's register address contents.

-----

00100000:
Pause program Until Input - PUI
2 Bytes

Pause the program until input from the keyboard is received, then store the input in the register determined by the second byte.

-----

00100001:
Sound for Register Cycles - SRC
2 Bytes

Play a low tone sound for the amount of cycles stored in a register dictated
by byte two.

-----

00100010:
Clear Video Memory - CVM
1 Byte

Clear the contents of video memory.
