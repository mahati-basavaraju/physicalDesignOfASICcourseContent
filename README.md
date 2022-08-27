# physicalDesignOfASICcourseContent
Repo with info related to the physical design of asic 

## Inception of open-source EDA, OpenLANE and SKy130PDK
### How to talk to computers
### Introduction to QFN- 48 package, chip, pads, core, die and IPs

A core of the chip is located at the centre of the package. The pins are connected to the chip with a wire bound. 
Core is area where the digital logic is.
Example of a package: QFN-48 (QFN stands for Quad Flat No leads)

A package has various components. 
Pads are one such component which helps in transmission of signals from pins to the core of the chip.
Die is another component.

A typical core consists of SoC, SRAM, PLL, ADC, DAC , etc. All these parts of the core chip are known as Foundry IPs.

Foundry is a factory where chips get manufactured.
IP standsd for intellectual property.

### Introduction to RISC - V

#### RISC - V Instruction Set Architecture (ISA)

Let us consider an example to understand this concept.

To execute a C program on a particular hardware layout, it first needs to compiled, converted to assembly language and then to machine language such that the hardware understans. Also an interface is required to implement the C code on the hardware i.e., an RTL.
Example of RTL: picorv32 cpu core

### From Software applications to hardware

System software converts the software/ applications so that it could be understood by the hardware. The major components of System Software are the operating system (OS), the compiler and the assembler.

The OS handles IO operations, memory allocation and other interfacing task. Also, the OS converts the software applciations into assembly language and finally into binary language so that the hardware can understand.

The output of the OS are small snippets of C/C++/ Java which are compiled using their respective compilers and are converted into instructions. The syntax of these instructions depends on the type of hardware used. This is done by the compiler. 

The Assembler then converts the instructions to machine language i.e., binary. 

The hardware then performs the functions accordingly.


The instruction set acts as an abstract interface between the C code and the hardware. This is known as instruction set architecture or architecture of a computer.

As the hardware understands only binary, the instructions have to be converted to binary that could be understood by hardware. An  RTL is required to implement these instructions. RTL gets synthesised as a netlist. 

## SoC Design and OpenLANE

### Introduction to all components of open-source digital asic design

Designing ASIC requires elements such as the RTL IPs, EDA tools and PDKs.

#### PDK

Process Design Kit or the PDK is the interface between the FAB and the designers. It is a collection of files used to model a fabrication process for the EDA Tools used to design an IC. The PDK contains information such as Process Design Rules, Digital Standard cell libraries, I/O Libraries.

### Simplified RTL2GDS flow

The major steps in RTL to Layout include
- Synthesis
- Floor/ Power planning
- Placement
- Clock Tree Synthesis
- Routing
- Sign off

In synthesis, the design is converted into circuits made from standard cell libraries. The standard cells have regular layout. Each cell has different views/models.

In floor/ power planning, silicon area is planned and robust power distribution to circuits is ensured.

- Chip Floor-Planning: The chip die partitioned between different cgip components.
- Macro Floor - Planning: We define macro dimensions and pin locations. Also, the rows of routing tracks are defined.
- Power Planning- The power network is constructed. Chip is powered by multiple Vdd and ground pins. The power pins are connected through rails - horizantal and vertical metal straps. Such parallel structures are meant to reduce the resistance and to address the electro migration problem.

In placement, the macros will place the gate level netlist cells on the vertical rows. To reduce the interconnect delay and enable routing, the cells must be placed closer to each other. Typically, cell placemtn is done in two steps: Global and Detailed.

Global placement is done to find optimal position for all cells. Such positions are not always legal and hence some cells may overlap or go off rows.
In Detailed placement, the positions obatined from global placements are minimally altered to be legal.

After placement, and before routing, the clock must be routed.

Hence the next step is clock tree synthesis,. In this a clock distribution network is created to deliver the clock to all the clock cells (example, flip-flops) with minimum skew and minimum latency and in good shape. The clock network looks like a tree with the clock source as the roots and the clock elementts as the end leaves. 

Clock skew means the arrival of the clock at different components at different times.

After routing the clock, comes signal routing. Given placement and fixed number of metal layers, it is required to find a valid pattern of horizantal and vertical wires to implement the nets that connects the cells together. The router uses the available metal layers as defined by the PDK. For each metal layer, the PDK defines the thickness, the pitch that defines the tracks and the minimum width. Also defines the ways that can be used to connect the wire segments on the different metal layer together.


The skywater130 pdk defines 
