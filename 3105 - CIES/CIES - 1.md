---
course: "CSE 3105 – Computer Interfacing and Embedded Systems (CIES)"
class: "CIES - 1"
duration: "32:25"
---
# CIES - 1 – Introduction to Computer Interfacing and Embedded Systems

## Overview
This introductory lecture establishes the core concepts of **Computer Interfacing** and **Embedded Systems**, explaining how embedded microcontrollers differ from general-purpose computers. It also introduces the hardware and software stack for the course—moving from familiar 8-bit Arduino concepts to a 32-bit **STM32** microcontroller—and outlines the three defining characteristics of embedded systems along with a brief comparison against microprocessors and FPGAs.

## Topic Map
- Course Scope & Logistics
  - Co-teaching structure and microcontroller focus
- Computer Interfacing
  - Von Neumann components (CPU, RAM, I/O devices)
  - Peripherals vs. core components
  - Interface examples (USB, legacy mouse port, audio jack, NIC)
  - Human-Computer Interface (HCI)
- How a Computer Works (Review)
  - Instruction storage and loading (Secondary storage $\rightarrow$ RAM $\rightarrow$ CPU)
  - Fetch–Decode–Execute cycle (8086 recap)
- Embedded Systems
  - Everyday examples (microwave oven, washing machine, smartwatch, rice cooker)
  - User interaction vs. manufacturer pre-programming
  - Sensors vs. processing units
- Microcontrollers & Course Hardware
  - Arduino as a complete suite vs. a standalone board
  - Word size and bit width (8-bit vs. 16-bit vs. 64-bit)
  - STM32 introduction (32-bit, 48 pins, GPIO Ports A/B/C, bare-metal register configuration)
  - Lab transition: programming STM32 via Arduino IDE using middleware
- Real-World Embedded System Case Study (Motorcycle)
  - Disc brake vs. Anti-lock Braking System (ABS)
  - Fuel level indicator
  - Multi-chip architecture and coordination
  - Clock speed and thermal limits
- Three Characteristics of Embedded Systems
  - Sophisticated functionality
  - Real-time output (vs. "faster" output)
  - Cost and power constraints
- Microprocessors vs. Microcontrollers vs. FPGAs
  - General-purpose (CPU) vs. special-purpose (GPU, FPGA)
  - Open question for next class

## Detailed Notes

### 1. Course Scope & Expectations
- Students expect to work with **microcontrollers** and **Embedded C / C++**.
- The course uses a microchip/microcontroller platform to teach how a designer/manufacturer programs and sets up an embedded system from the ground up.

### 2. What is Computer Interfacing?
- **Interface (intuitive idea):** A communication bridge.
- Recall from **Von Neumann architecture** that a computer has three main parts: **CPU**, **RAM**, and **I/O devices**.
  - **CPU** and **RAM** are mandatory ("must") for a computer.
  - Everything else outside CPU and RAM is a **peripheral**.
- **Definition of Interface:** The medium or mechanism through which peripherals connect to and communicate with the computer's CPU and RAM.
- **Examples:**
  - **USB port**
  - **Legacy mouse port** (referred to in class as a "PSA port"; *note: the teacher likely meant the legacy PS/2 port*)
  - **Audio / earphone jack** (sound card port)
  - **LAN card / Network Interface Card (NIC)** (has "Interface" directly in its name)
- **Human-Computer Interface (HCI):**
  - Users never interact directly with a PC's CPU; every interaction goes through an interface.
  - **HCI** is a broad category for user-facing interfaces, and **keyboard** and **mouse** are two devices within it.

### 3. How a Computer Works (8086 Recap)
- Literally in Bangla, a computer is a *gananajantra* ("গণনযন্ত্র" — calculating machine), but technically it is a **device capable of executing instructions**.
- **Instruction flow:**
  1. Instructions are stored in **permanent (secondary) storage**.
  2. They are loaded into **main memory (RAM)** as a program (a set of instructions).
  3. The **CPU** brings instructions from RAM and executes them.
- **Processor Instruction Cycle (from 8086):**
  - Any device that performs the three-step cycle below is a microprocessor/CPU:
    1. **Fetch** (retrieves the instruction/data from memory)
    2. **Decode** (interprets what the instruction means)
    3. **Execute** (carries out the operation)

### 4. What is an Embedded System?
- **Everyday examples:** Microwave oven, washing machine, smartwatch, rice cooker.
  - **Microwave oven:** You press a few buttons, it heats food for a set time, and automatically turns off.
  - **Rice cooker:** You put rice in and start it without specifying when to stop; it automatically turns off once the rice is cooked.
    - While a **heat sensor** detects the temperature/state, a sensor can *only sense*—it has no processing power. Inside the appliance, a **processing unit** reads the sensor and decides when to switch off.
- **Definition:** An embedded system is a small processing unit/system integrated (**embedded**) inside a larger system as a component of that larger system.
- **Key Difference from a General-Purpose Computer:**
  - **Personal Computer (PC):** Through interfaces, a user can directly interact with the CPU, modify its behavior, and write/run arbitrary code on it.
  - **Embedded System:** End-users cannot write or run arbitrary programs on the internal CPU. The **manufacturer/designer** pre-programs a fixed set of instructions into the chip, and the user only triggers those predefined behaviors through simple interfaces (e.g., pressing oven buttons or closing the rice cooker lid and flipping a switch).
- **Perspective in this course:** We will study and build embedded systems from the **manufacturer/designer's perspective**—learning how to program and configure the embedded chip itself.

### 5. Microcontrollers, Word Size, and Course Hardware (STM32)
- **Arduino vs. Microcontroller:**
  - People often call the board "Arduino," but Arduino is actually a **complete suite/package** containing:
    - Hardware boards/chips (e.g., Arduino Uno)
    - **Arduino IDE**
    - Programming language / libraries
    - Compiler
- **Word Size & Bit Width:**
  - **Word size** corresponds to the general-purpose register width a processor handles natively.
  - **8086** was a **16-bit** CPU $\rightarrow$ word size = $2\text{ bytes}$ ($16\text{ bits}$).
  - Standard **Arduino** (e.g., Uno) is an **8-bit** microcontroller (very low power).
  - Modern PCs use **64-bit** processors.
  - **Effect of larger bit width:** Allows handling larger numbers natively, supports larger instruction sets, and enables packing more data/operations into a single instruction, increasing computational capability and complexity.
- **Course Chip — STM32:**
  - Instead of Arduino boards, this course uses an **STM32** board/chip.
  - Naming breakdown: **ST / STM** = **STMicroelectronics**, **32** = **32-bit processor**, followed by the series number.
  - **Bare-metal programming:** Unlike Arduino (where you simply call high-level library functions), STM32 natively works at the **bare-metal** level—nothing is abstracted away, and everything must be configured from the ground up.
  - **Pin & Port Structure (preview):**
    - The chip has **48 pins** divided into categories.
    - One category is **GPIO** (**General Purpose Input/Output**), organized into three ports: **Port A**, **Port B**, and **Port C**.
    - As explained in class, each port has **16 pins** (*note: while STM32 GPIO port registers are 16-bit wide, on a 48-pin package such as STM32F103C8, Port C exposes fewer external physical pins*).
    - Pins can be configured individually (16 separate purposes in a port) or grouped so an entire 16-pin port serves one purpose.
    - **How configuration works:** Every port has built-in **registers**. Manipulating and writing values into those registers configures the port's behavior (to be covered in detail later in the course).
- **Lab Transition Strategy (Arduino IDE + Middleware):**
  - Rather than jumping straight into bare-metal register manipulation on day one, initial labs will use the **Arduino interface (Arduino IDE)** with C/C++.
  - **Why middleware is required:** Arduino and STM32 have different processor architectures and therefore **different machine code**. Code compiled natively for Arduino cannot run directly on STM32.
  - **Virtual Machine / Emulator analogy:** Just as running Linux inside Windows requires a translation layer converting instructions from one environment to another, programming STM32 from Arduino IDE requires a **middleware / translation layer** that compiles Arduino C/C++ code into **STM32 machine code**.

### 6. Case Study: Motorcycle as an Embedded System
A motorcycle is a large embedded system composed of many smaller embedded subsystems working together.

- **Braking System & ABS (Anti-lock Braking System):**
  - **Traditional Disc Brake:** Pressing the brake lever clamps rubber pads onto the wheel's steel disc, locking the wheel instantaneously. Because the vehicle still has forward momentum, the locked wheel **skids/slides** ("গাড়ি পিছলে চাকা আটকিয়ে যায়").
  - **ABS (Embedded System Solution):**
    - A **sensor** on the front wheel continuously tracks wheel rotation speed.
    - The moment the brake is pressed, the ABS subsystem activates, reads the wheel speed, and modulates brake pressure gradually/dynamically instead of locking the wheel all at once.
    - This produces a **smooth stop** without wheel lockup. The exact pressure control logic is pre-programmed by the manufacturer.
- **Fuel Level Indicator:**
  - A sensor in the fuel tank tracks the fuel level. Since a sensor cannot process data on its own, it sends readings to a processor, which triggers a low-fuel indicator light/beep when fuel drops below a threshold.
- **Why Multiple Chips Instead of One?**
  - A complex system like a motorcycle can contain **100 to 1,000+ chips**, each dedicated to a different role.
  - Microcontroller chips run at much lower clock speeds than PCs—typically around **80 MHz** or **100 MHz** (compared to **3–5 GHz** on a desktop CPU)—and have no active cooling system.
  - Attempting to run every subsystem (ABS, fuel monitoring, etc.) on a single low-power chip would be too slow and could overheat/damage the chip.
  - Using multiple specialized chips requires **coordination** between them; without proper coordination, failures (such as a crash) can occur.

### 7. Three Core Characteristics of Embedded Systems
1. **Sophisticated Functionality:**
   - Although embedded chips are weaker than PC CPUs, they are not limited to trivial arithmetic (like $1+1=2$). They execute fairly complex control logic (e.g., real-time ABS braking algorithms).
   - At the same time, they are not built for massive general-purpose workloads (e.g., playing modern PC games on a microwave oven).
2. **Real-Time Output:**
   - Outputs must be produced at the **exact instant required**, not merely "fast."
   - **Real-time vs. Faster:**
     - *Printer* (needs to be **faster**): If a printer takes 5 minutes, it is annoying and wastes time, but causes no physical harm.
     - *ABS* (needs to be **real-time**): If the ABS sensor/processor took 2 minutes to react after pressing the brake, an accident would occur before the brake engages.
   - **Multi-chip synchronization:** When multiple chips cooperate in one system, their outputs must align in real time (an output arriving 1 minute early or 1 minute late breaks coordination).
3. **Constraints (Cost & Power):**
   - **Low Cost:** Manufacturers will not put an expensive high-end processor (e.g., an RTX 4090) inside a microwave oven; the embedded chip must add minimal manufacturing cost on top of expensive mechanical parts (like an engine).
   - **Low Power:** Must consume very little power while still meeting sophisticated functionality and real-time deadlines.

### 8. Microprocessors vs. Microcontrollers vs. FPGAs
- **General-Purpose Microprocessors (PC CPUs) vs. Microcontrollers:**
  - PC microprocessors are power-hungry, costly, and built for heavy general-purpose workloads; embedded systems use low-power, low-cost microcontrollers instead.
- **FPGA (Field Programmable Gate Array):**
  - *"Field Programmable"* means before deploying to the end-user ("the field"), the chip's hardware gates can be configured/programmed for a **specific purpose**.
- **General-Purpose vs. Special-Purpose Tradeoff (CPU vs. GPU Analogy):**
  - **CPU (General-purpose):** Optimized for complex logic, **branching (`if-else`)**, and **looping**.
  - **GPU (Special-purpose):** Optimized specifically for **matrix multiplication**; its compute units are much simpler, so it outperforms a CPU at matrix math but is much slower at complex branching.
  - Similarly, **FPGAs** excel at the specific task they are configured for, whereas general-purpose processors handle varied tasks.

## Exam / Important Points
- **Know the 3 Characteristics of Embedded Systems:** (1) Sophisticated functionality, (2) Real-time output, (3) Constraints (low cost & low power). Be clear on the distinction between **real-time** (ABS) and **faster** (printer).
- **Sensor vs. Processor:** A sensor only detects/senses; it has **no processing capability** of its own and must pass data to a processor/microcontroller.
- **Word Size:** Defined by a processor's general-purpose register size (e.g., 8086 is 16-bit / 2-byte word size; standard Arduino is 8-bit; STM32 is 32-bit).
- **Thought Question for Next Class:** Since embedded systems are built for specific tasks (e.g., ABS only monitoring wheel speed and modulating brake pressure), why do we use **general-purpose microcontrollers** (like STM32 or Arduino) instead of designing a custom **special-purpose chip** for each task? (To be discussed next class.)

## Announcements & Logistics
- **Course Split:** The teacher will conduct the first half of the course, and a co-instructor will conduct the second half. Lecture slides are primarily from the co-instructor, supplemented by the teacher.
- **Google Classroom & Lab Manual:** A lab manual has already been posted on Google Classroom by the co-instructor.
- **Before Next Lab:** Students should check the lab manual and install the **three required software components** for STM32 development:
  1. **Arduino IDE**
  2. **Device Driver**
  3. **Middleware / STM32 board support package**
  - Anyone who gets stuck during installation will be helped in the upcoming lab session.

## Open Questions / Unclear Parts
- `00:00–01:40`: Pre-class informal chatter and discussion about earlier courses (e.g., Database) — partially indistinct due to room noise.
- `19:00–19:35`: The teacher holds up the physical STM32 board in class; only "STM32" is stated clearly aloud (exact part/series suffix was shown visually rather than read out).
- `27:45–28:15`: Brief overlapping classroom chatter during the ABS delay example.
