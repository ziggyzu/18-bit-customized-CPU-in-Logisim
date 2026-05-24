# 18-bit-customized-CPU-in-Logisim
18-Bit Microprogrammed Mini Computer

Introduction:
This project presents the design and simulation of a custom 18-bit CPU using a digital logic simulator. The purpose of the project was to understand the basic working principles of a processor, including arithmetic operations, memory access, instruction execution, and control signal generation. The processor follows an accumulator-based architecture where most operations are performed using a main working register called the accumulator. The complete system includes memory units, registers, an arithmetic and logic section, and a control section that manages the execution of instructions.

Project Objectives:
The main goals were:
To design a functional 18-bit processor.
To implement arithmetic and logical operations.
To connect memory and registers into a complete system.
To execute instructions through a step-by-step control mechanism.
System Overview:
The CPU was designed with an 18-bit data path and a 14-bit address system. The architecture allows data transfer between memory, registers, and the arithmetic unit. The system mainly consists of:
Program Counter
Instruction Register
Memory Address Register
Memory Buffer Register
Accumulator
RAM (Main Memory)
Arithmetic and Logic Unit (ALU)
Control Unit (Featuring an internal Control Store ROM)
The Program Counter stores the address of the next instruction. The Instruction Register stores the current instruction being executed. The Memory Address Register holds memory locations, while the Memory Buffer Register temporarily stores data being transferred. The accumulator acts as the main working register for calculations.
CPU Architecture:
The processor uses an accumulator-based architecture. Data moves through a shared bus system between memory and registers.
The processor contains:
Component
Size
Function
Program Counter
14-bit
Stores next instruction address
Instruction Register
4-bit
Stores operation code and address
Memory Address Register
14-bit
Stores memory addresses
Memory Buffer Register
18-bit
Transfers data to/from memory
Accumulator
18-bit
Main calculation register
CPU(RAM)
16,384 locations
Stores data
Control Unit(ROM)
64 locations
Stores control instructions


The data path width is 18 bits, meaning all operations are performed using 18-bit binary values.
Arithmetic and Logic Operations:
The ALU performs all arithmetic and logical calculations of the processor. Supported operations are:
AND
OR
ADD
SUBTRACT
Note: The CPU also supports Increment and Decrement instructions. Instead of dedicated ALU hardware , these are executed by routing the Accumulator and a hardwired constant value of 00001 into the ALU, and applying the standard ADD or SUB operation.
The ALU receives two input values and produces one output result. It also generates status flags. Status Flags are:

Flag
Purpose
Zero
Activated when result becomes zero
Negative
Activated when result is negative
Carry
Activated when when carry occurs
Overflow
Activated during arithmetic overflow


Memory System:
The processor uses two types of memory.
1. RAM: RAM is used for storing data.
Address Width: 14 bits
Data Width: 18 bits
Total Capacity: 16,384 memory locations
 
2. ROM: ROM stores the control instructions required for processor operations.
The ROM controls the execution steps of each instruction.

Registers:
Instruction Register: Stores the current instruction opcode and address.
Memory Address Register: Stores the memory address for read/write operations.
Memory Buffer Register: Temporarily stores data transferred between memory and processor.
Accumulator: Stores arithmetic and logical operation results.
Control Unit:
The Control Unit controls the overall operation of the CPU.
Its responsibilities include:
Fetching instructions
Decoding instructions
Generating control signals
Managing memory operations
Controlling ALU operations
Instruction Execution Process:
Because the CPU is a Synchronous design, all register updates are strictly tied to a global clock edge. This prevents data corruption as information moves through the datapath. The CPU executes each instruction using a multi-cycle sequence: 
Fetch:The instruction is fetched from RAM into the Instruction Register (IR). 
Decode:The 4-bit opcode from the IR is passed to the Control Unit to determine the required execution path. 
Execute:The Control Unit outputs the necessary signals to route data through the multiplexers and ALU. The final result is processed and immediately latched into the destination (either the Accumulator or RAM) on the concluding clock cycle of this phase.
 Control Unit and Control Signal Generation:
The Control Unit is responsible for the overall orchestration of the CPU. Rather than using hardwired logic gates, it utilizes a Microprogrammed Control Unit design.
Instead of drawing from main memory, the Control Unit has its own internal Control Store(ROM). A sequence counter steps through this internal ROM, which outputs a control word. The word is fed into a decoder that activates specific control wires at the exact right clock cycle to manage multiplexers, registers and ALU operations.
Instruction Format:
Each instruction is 18 bits wide.
Field
Size
Functions
Opcode
4 bits
Determines the operation to be performed .
Operand/Address
14 bits
Contains the memory address the instruction acts upon.


The opcode determines the operation type, while the operand field contains data or memory addresses.
Supported Instructions:
The processor supports several operations:
Opcode(Dec)
Instruction
Description
0
AND
Logical AND
1
ADD
Add values
2
STO
Store data into memory
3
OR
Logical OR
4
SUB
Subtract values
5
BUN
Branch unconditionally
6
LDA
Load data from memory
7
HLT
Terminates the program
8
INC
Increment value 
9
DEC
Decrement value


Technical Specifications:

Feature
Specification
Word Size
18 bits
Address Width
14 bits
Data Memory
16,384 X 18-bit
Instruction Width
18 bits
ALU Operations
6
Clock Type
Synchronous            (the entire control unit and datapath are synchronized to a single global clock edge )


CONCLUSION:
This project successfully demonstrates the design and simulation of a functional 18-bit CPU within a digital logic environment. The processor accurately performs arithmetic operations, logical operations, memory access, and instruction execution. By building this architecture from the ground up, the project provided a strong, practical understanding of crucial computer architecture concepts such as register-transfer level (RTL) design, memory management, and microprogrammed control signal generation. 

