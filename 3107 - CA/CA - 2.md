---
course: "CSE 3107 – Computer Architecture (CA)"
class: "CA - 2"
duration: "1:15:23"
---
# CA - 2 – Computer Architecture Foundations: ISA, Microarchitecture, Program Execution Lifecycle, and Transistor-Level Logic

## Overview
This lecture introduces the core scope of Computer Architecture by distinguishing **Instruction Set Architecture (ISA)** from **Microarchitecture**, and then traces the entire vertical stack of how a high-level program executes on physical hardware—spanning compilation, assembly, machine code encoding, the Von Neumann fetch-decode-execute cycle, logic gates, and semiconductor transistors (BJT, MOSFET, and CMOS). It serves as the conceptual roadmap ("gist") for the whole semester's course, bridging prior knowledge from Analog Electronics and Digital Logic Design to processor design.

## Topic Map
- **1. Components of Computer Architecture**
  - Instruction Set Architecture (ISA) — behavioral definition, register size & count, memory access, instruction size, addressing modes, ISA extensions
  - Microarchitecture — hardware-level implementation, generational & vendor differences, transistor scaling
  - Semiconductor Industry & Career Context
- **2. End-to-End Program Execution Lifecycle**
  - High-Level Language (`int a = 10; a = a + 5; return 0;`)
  - Compiler Phase — error checking, comment removal, parsing, target-dependent Assembly generation
  - Assembly Language Portability & Evolution (`8086` mother series vs. Core i9, ARM)
  - Assembler, Linker & Loader — memory dependency resolution, stack preservation, decomposing `MOV` into `XOR` + `ADD`
  - Machine Code Encoding — Opcode (Addressing Mode + Operator) & Operands in binary (shown in hex)
  - Von Neumann Execution Cycle — Process creation, RAM loading, Program Counter (PC), Control Unit (CU), ALU, MUX, buses, write-back/I/O
  - Abstraction Hierarchy (High-Level Code $\rightarrow$ Physics) & Turing Machine Note
- **3. Transistors, Logic Gates & CMOS**
  - Transistor Roles: Amplifier vs. Switch
  - BJT-Based Logic Gates — AND, OR, NOT, NOR, and practical voltage thresholds
  - Limitations of BJT — bipolar carriers, size (~300–400× larger), resistor heat/power dissipation
  - Field-Effect Transistors (FET / MOSFET) — NMOS vs. PMOS speed and operation
  - From NMOS-Only to CMOS — eliminating bulky, power-wasting resistors

## Detailed Notes

### 1. Components of Computer Architecture

Computer Architecture is defined by two distinct layers:

#### Instruction Set Architecture (ISA)
- **Definition**: Defines the *behavior* of the computer—how the system behaves and what capabilities it exposes.
- **What ISA specifies**:
  - **Register size**: Data width processed or transferred in a single instruction / single clock cycle (e.g., a **32-bit architecture** operates on 32-bit data via ALU or communicates 32 bits over parallel buses in one cycle).
  - **Number of registers**: How many registers exist of that size (e.g., 16 registers of 32 bits each, such as `AX`, `BX`, `CX`, `DX`, `EX`, `SI`, `DI`, etc.). *Size* of a register and *count* of registers are two separate ISA parameters.
  - **Memory access**: How the CPU communicates with and accesses memory.
  - **Instruction (machine code) size**: Bit width of each machine instruction.
  - **Addressing modes**: Which modes are supported and how they are encoded (e.g., Direct, Indirect, Base, Immediate). Supporting $8$ addressing modes requires $3$ bits because $2^3 = 8$.
- **ISA Extensions**: Existing ISAs can be extended for specific data types or specialized operations. For example, in `8086` assembly, general addition is `ADD`, while an extended instruction like `ADDI` handles immediate addition (and similar extensions exist across architectures like ARM).
- **Teacher's Analogy**: ISA is like a country's **constitution** (*সংবিধান / মূলনীতি*, e.g., the 1972 constitution)—it sets the fixed foundational rules.

#### Microarchitecture
- **Definition**: How the ISA is *implemented at the hardware level*.
- **Design choices**:
  - Whether a 16-bit operation is executed on a native 16-bit hardware unit, or broken down into 4-bit slices or two 8-bit operations ($8 + 8 = 16$).
  - Specific transistor/register technology used, circuit organization, and power consumption ratings.
- **Same ISA, Different Microarchitecture**:
  - **Across vendors**: Intel, AMD, and ARM all have 32-bit ISAs, yet their microarchitectures differ.
  - **Across eras**: A 32-bit processor from 1990 or 2000 vs. 2026 shares the 32-bit ISA concept, yet has a radically different microarchitecture.
  - **Transistor scaling**: The `8086` had roughly a few thousand transistors *(teacher uncertainly recalled ~4,000 / 4,096 / 32,000; note: the Intel 8086 had ~29,000 transistors)*, whereas modern chips pack over **4 billion** transistors. As transistor technology advances, microarchitecture updates continuously while keeping the ISA compatible.
- **Teacher's Analogy**: If ISA is the constitution, Microarchitecture is how successive governments actually run the country—maintaining, upgrading, or adapting within/around that framework.

#### Semiconductor Industry Context
- Major semiconductor/processor companies highlighted: **Intel, Nvidia, ARM, Qualcomm, AMD, Microchip, Samsung** (noting Samsung also designs/fabricates processors).
- The teacher noted that CSE students often focus only on software engineering, competitive programming, BCS, or higher studies abroad, leaving VLSI and chip design roles (e.g., at Intel) mostly to EEE/ECE graduates.

---

### 2. End-to-End Program Execution Lifecycle

To understand the whole course, the lecture walks through how a high-level C snippet runs on hardware:

```c
int a = 10;
a = a + 5;
return 0;
```

```
High-Level C Code
       │
       ▼  [Compiler] (checks compile-time errors, strips comments, target ISA-aware)
Assembly Language (e.g., MOV AX, 10)
       │
       ▼  [Assembler + Linker + Loader] (decomposes MOV -> XOR+ADD, resolves memory)
Machine Code (Binary, shown as Hex)
       │
       ▼  [Loaded into RAM as a Process]
Von Neumann Cycle (PC -> Fetch -> CU Decode -> ALU/MUX Execute -> Register/RAM/IO)
```

#### Step 1: Compiler
- Checks **compile-time errors** (distinct from runtime errors like division by zero):
  - Syntax errors (e.g., missing `;`, missing `return` expression).
  - Type errors (e.g., declaring an `int` variable and assigning a `float`).
- Ignores **comments**—commented lines never produce machine instructions and therefore never execute.
- Tokenizes identifiers, builds parse/syntax trees, and emits **Assembly Language** tailored to the installed processor's ISA (a compiler inspects the host processor architecture upon installation).
- **Assembly is Processor-Dependent**:
  - `8086` is Intel's "mother series" (`x86`), so all subsequent Intel processors (Core i5, i7, i9) share the same core assembly family, though newer chips have many *additional* instructions (e.g., dedicated hardware circuits for unsigned multiplication that older chips lacked and had to emulate with repeated additions).
  - ARM assembly shares similar concepts (`ADD` vs. `ADDI`), but has different syntax.
- For `int a = 10;`, the compiler maps variable `a` to a register (e.g., `AX` or `RAX`) and generates an immediate move instruction like `MOV AX, 10` (slide showed `dword` for double word).

#### Step 2: Assembler, Linker & Loader
- **Why Assembly cannot run directly**:
  - Assembly itself may contain comments or errors that must be stripped/checked.
  - **Memory dependencies**: Jump targets and physical RAM addresses are unknown at compile time; the Assembler, Linker, and Loader resolve these using a memory lookup/symbol table when loading the program.
- **Hardware Decomposition of `MOV`**:
  - Unlike addition (which has an adder circuit), there is **no dedicated hardware circuit** for moving an immediate constant directly into a register.
  - The assembler decomposes `MOV AX, 5` into two primitive hardware operations:
    1. **Clear/flush the register**: `XOR AX, AX` (Exclusive-ORing a register with itself zeroes all bits).
       - *Context preservation*: If another active process was previously using `AX`, its value must first be **pushed onto the Stack** before the routine begins and **popped back** afterward so the prior process does not lose its data.
    2. **Add the immediate constant**: `ADD AX, 5` (since $0 + 5 = 5$).
- **Binary Machine Code Encoding (Worked Example)**:
  - Each instruction splits into **Opcode** and **Operands**.
  - **Opcode** = `Addressing Mode` + `Operator`:
    - Addressing Mode (e.g., 2 bits): `00` = Direct Register mode, `10` = Immediate mode.
    - Operator (e.g., 4 bits): `0010` = `XOR`, `0000` = `ADD`.
  - **Operands**:
    - Register addresses need $\lceil \log_2 N \rceil$ bits (e.g., 16 registers $\rightarrow 4$ bits since $2^4 = 16$; 32 registers $\rightarrow 5$ bits). In the board illustration, the teacher used 2-bit register IDs with `AX` = `00` for simplicity:
    - `XOR AX, AX` $\rightarrow$ `00` (Direct) `0010` (`XOR`) `00` (`AX`) `00` (`AX`)
    - `ADD AX, 5` $\rightarrow$ `10` (Immediate) `0000` (`ADD`) `00` (`AX`) `0101` ($5$ in binary)
  - *2-Address vs. 3-Address Formats*:
    - 3-address: `ADD AX, AX, CX` (1st operand is destination, 2nd & 3rd are sources).
    - 2-address: `ADD AX, CX` (`AX` acts as both destination and first source).
  - *Hexadecimal display*: Textbooks show machine code in **hexadecimal** (4 binary bits per hex digit) purely for readability; the hardware stores and executes pure **binary**.

#### Step 3: Execution Cycle (Von Neumann Architecture)
- This course uses the **Von Neumann Architecture** (contrasted with **Harvard Architecture**, studied later in Microprocessors):
  - **Units**: Input, Output, **Memory Unit** (stores both data and instructions), and CPU consisting of **Control Unit (CU)** + **Arithmetic Logic Unit (ALU)**.
- **Lifecycle**:
  1. The binary executable sits on secondary storage (hard disk). Launching it creates an OS **Process** with a unique Process ID (PID) and a memory block tracked by the OS (Process Control Block), loading the binary lines into **RAM**. (Note: 1,000 lines of C may expand to ~1,200 lines of machine code after decomposition).
  2. The **Program Counter (PC)** register holds the RAM address of the *next instruction to be executed* (initialized to the starting address of the process in RAM, e.g., `0001`).
  3. **Fetch**: The computer fetches the binary instruction from RAM at the PC address and delivers it to the **Control Unit**.
  4. **Decode**: The CU reads the addressing mode and operator bits, deciding what operation to run and where the operands live (register, immediate field, or memory).
  5. **Execute**: Data from the selected registers (or immediate value) travels over parallel **buses** (one bus per operand so both arrive simultaneously) into the **ALU**. Inside the ALU, all functional circuits (OR, ADD, XOR, etc.) compute in parallel in a single clock cycle, and a **Multiplexer (MUX)** selects only the output of the requested operation (e.g., `XOR`).
  6. **Write-back / Output**: The CU routes the ALU result back to the destination register, writes it to RAM, or sends it to a peripheral output device.

#### Abstraction Hierarchy & Turing Machine Note
- **Full Vertical Stack**:
  $$\text{High-Level Language} \rightarrow \text{Assembly} \rightarrow \text{Machine Code} \rightarrow \text{ISA} \rightarrow \text{CU/ALU/Registers} \rightarrow \text{Digital Logic Gates} \rightarrow \text{Analog Electronics} \rightarrow \text{Laws of Physics}$$
- **Turing Machine** (Alan Turing; **Turing Award** is the Nobel Prize of Computer Science): A purely theoretical model of computation. Any problem solvable by a Turing Machine can be solved by a real computer; any problem unsolvable by a Turing Machine cannot be solved by any computer.

---

### 3. Transistors, Logic Gates & CMOS

#### Transistor Roles
- **As an Amplifier**: Used in analog / Data Communication circuits (amplifying weak signals or attenuating strong ones via collector resistors).
- **As a Switch**: Used in Digital / Computer Architecture circuits (`ON` / `OFF`).

#### BJT (Bipolar Junction Transistor) Logic Gates
- Terminals: **Base (B)**, **Collector (C)**, **Emitter (E)**.
- Switching behavior:
  - Input = `0` (below saturation/threshold voltage) $\rightarrow$ **Open switch (OFF)**; no conductive path.
  - Input = `1` (above threshold) $\rightarrow$ **Closed switch (ON)**; conductive path forms and electrons flow from **Ground toward $V_{CC}$** (opposite to conventional current).
- **Gate Constructions** (with $V_{CC} = 5\text{ V}$ and resistor $R_2$):
  - **AND Gate**: Two BJTs in **series**, output taken across $R_2$ (between lower transistor and Ground). Both $A=1$ and $B=1$ must close the path for current to flow through $R_2$ and create a voltage drop ($V_{out} = 1$).
  - **OR Gate**: Two BJTs in **parallel**, output taken across $R_2$. Either $A=1$ or $B=1$ (or both) completes the path ($V_{out} = 1$).
  - **NOT Gate (Inverter)**: Single BJT with output taken *above* the transistor (between upper resistor and Collector).
    - Input `0` $\rightarrow$ switch open $\rightarrow$ no current $\rightarrow$ $V_{out} \approx V_{CC}$ (`1`).
    - Input `1` $\rightarrow$ switch closed $\rightarrow$ output shorted to Ground $\rightarrow$ $V_{out} \approx 0$ (`0`).
  - **NOR Gate**: Two BJTs in **parallel** with output taken *above* both transistors. Only $A=0, B=0$ leaves both open ($V_{out} = 1$); any `1` shorts output to Ground ($V_{out} = 0$).
- **Practical Voltage Thresholds**: Real transistors have small internal resistance even when ON, so outputs are never an ideal $5\text{ V}$ or $0\text{ V}$. Practical logic levels typically treat $< 2.7\text{ V}$ (or $2.8\text{ V}$) as `0`, $> 3.8\text{ V}$ as `1`, with an intermediate transition/saturation zone.

#### Why BJT Is Not Used in Modern CPUs
Two dominant constraints in processor design are **Space** and **Power Dissipation (Heat)**:
1. **Bipolar vs. Unipolar**: BJTs use *both* electrons and holes ("bipolar"), whereas FETs are **unipolar** (only holes in P-type, only electrons in N-type).
2. **Area/Size**: A BJT is roughly **300–400× larger** than a Field-Effect Transistor (FET), severely limiting how many gates fit on a die.
3. **Heat / Power Dissipation**: BJT logic gates rely heavily on **resistors** for voltage drops. Resistors oppose current and dissipate energy as heat ("like baking bread on the CPU").

#### FET / MOSFET, NMOS vs. PMOS, and CMOS
- **MOSFET (Metal-Oxide-Semiconductor FET)** terminals: **Source (S)**, **Gate (G)**, **Drain (D)**.
- **NMOS vs. PMOS Speed**:
  - **NMOS** conducts via free **electrons**, which move rapidly once a potential path exists.
  - **PMOS** conducts via **holes** (empty octet slots in silicon requiring electrons to hop from atom to atom), which is slower.
  - Therefore, **NMOS is faster than PMOS**.
- **Switching Conditions**:
  - **NMOS** (no bubble on gate symbol): Turns **ON** when forward-biased ($V_{GS} > 0$); **OFF** when $V_{GS} \le 0$.
  - **PMOS** (bubble/circle on gate symbol): Turns **ON** when reverse/negatively biased ($V_{GS} < 0$); otherwise **OFF**.
- **Why CMOS instead of NMOS-only?**
  - An NMOS-only inverter still requires a **resistor**. A single resistor occupies **at least ~300× more chip area** than a transistor and wastes power as heat.
  - **PMOS** exhibits high impedance and can serve as the pull-up/load impedance in place of a physical resistor.
  - Pairing **PMOS + NMOS** together eliminates all physical resistors—forming **CMOS (Complementary MOS)**, which drastically saves area and minimizes static power dissipation/heat.

## Exam / Important Points
- **ISA Definition (Viva & Written Exam Favorite)**: The teacher explicitly warned that **Instruction Set Architecture (ISA)** is repeatedly asked in vivas and exams, yet many students still fail to explain it clearly—memorize what ISA covers (register size & count, memory access, instruction size, addressing modes) vs. Microarchitecture (hardware implementation).
- **Distinguish Register Size vs. Register Count**: e.g., "32-bit architecture" = 32-bit register/data width per cycle; number of registers = e.g., 16 such registers.
- **Addressing Modes & Bit Width**: Remember $n$ bits encode $2^n$ items (e.g., 3 bits for 8 addressing modes; 4 bits for 16 registers).
- **Hardware Reality of `MOV`**: `MOV` has no dedicated circuit; it is decomposed into `XOR AX, AX` (flush) + `ADD AX, val`, and prior register contents must be saved to the stack before overwriting.
- **Practical Lab Measurements**: Never expect exact $5\text{ V}$ or $0\text{ V}$ on real BJT/transistor gates due to internal resistance (recognize the ~2.7–2.8 V low threshold and ~3.8 V high threshold).
- **Why CMOS Wins**: Know the two key chip-design criteria (**Space** and **Power Dissipation/Heat**), why BJT fails both (size + resistors), why NMOS beats PMOS in speed (electrons vs. holes), and why CMOS pairs PMOS + NMOS to remove resistors completely.

## Announcements & Logistics
None mentioned.

## Open Questions / Unclear Parts
- `00:00`: The recording begins mid-sentence ("...architecture. One is Instruction Set Architecture, another is called Microarchitecture."), so the initial few opening words are cut off.
- `16:35–16:50`: The teacher briefly hesitated on the exact transistor count of the Intel 8086 ("around 4,000, or 4,096, or 32,000"); the actual historical figure for the 8086 is ~29,000 transistors.
- `19:15–19:30`: Brief side exchange / interruption in the classroom (inaudible distant voice, teacher replies briefly about doing something within the day).
- `48:55–50:55`: Short classroom break discussion with overlapping student voices about taking a break vs. continuing.
- `1:14:00–1:15:23`: Loud student chatter at the end as the class wraps up; exact final remark of the teacher around `1:15:20` is partially drowned out by classroom noise.
