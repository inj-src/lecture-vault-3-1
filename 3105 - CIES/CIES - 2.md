---
course: "CSE 3105 – Computer Interfacing and Embedded Systems (CIES)"
class: "CIES - 2"
duration: "39:07"
---
# CIES - 2 – Embedded System Scenarios, Security, Constraints, and Design Process

## Overview
This lecture continues the introductory module of CSE 3105 after covering embedded system characteristics and applications in the previous class. It begins with a recap of why general-purpose processors are favored over task-specific chips, distinguishes between IoT and Cyber-Physical Systems (CPS), and explains edge computing, data security (cryptography), and real-time deadline constraints. The bulk of the lecture walks through the five-step embedded system design process using a Smart Plant Watering System as a worked example, concluding with functional versus non-functional requirements.

## Topic Map
- **Recap: General-Purpose vs. Specific-Purpose Processors**
  - Performance trade-off (average across tasks vs. single-task optimal)
  - Design/manufacturing cost and flexibility
- **Embedded System Use Scenarios: IoT vs. Cyber-Physical Systems (CPS)**
  - Internet of Things (IoT): low-power household end devices
  - Cyber-Physical Systems (CPS): high-capability automated systems (airplanes, autonomous vehicles)
- **Edge Computing & Security in Embedded Systems**
  - Why time-critical tasks require local (edge) computation
  - Security risks in embedded devices (e.g., autonomous vehicles)
  - Cryptography basics: Plaintext, Ciphertext, Key, Encryption/Decryption, Caesar Cipher
  - Symmetric-key (AES) vs. Asymmetric-key (RSA) cryptography
- **Design Constraints & Optimization Challenges**
  - Desktop speed goal vs. Embedded **Deadlines** (e.g., ABS braking)
  - Hardware limitation (Desktop $3\text{–}5\text{ GHz}$ vs. STM32F103 $72\text{ MHz}$)
  - Dual optimization: Hardware selection + Algorithm efficiency
- **Embedded System Design Process (5 Steps) — Smart Plant Watering System**
  1. Requirement Analysis (Customer needs, Requirement Form: Inputs, Functionality, Outputs)
  2. Specification (Ordered technical steps, periodic sensing for energy efficiency)
  3. Architecture (System blueprint, splitting into Hardware & Software flows)
  4. Designing Hardware & Software Components
  5. System Integration
- **Functional vs. Non-Functional Requirements**
  - Core system behavior vs. constraints (cost, weight/size, performance, delivery deadline)

## Detailed Notes

### 1. Recap: General-Purpose vs. Specific-Purpose Processors
- **Core question from previous class**: Why do we usually use general-purpose processors instead of designing a custom processor strictly for one specific task?
- **Trade-off**:
  - A **specific-purpose** processor is excellent for its single target task, but performs poorly or cannot be used for any other task.
  - A **general-purpose** processor performs better on average across a wide range of tasks.
- **Two main reasons general-purpose processors are used**:
  1. **Lower design and manufacturing cost**: Designing and fabricating a separate custom chip for every individual operation is expensive. General-purpose chips are already available on the market and can simply be picked up and used.
  2. **Flexibility**: If requirements change later (for instance, launching a next-generation model of a product such as a bike), a task-specific chip would require redesigning the entire hardware chip, whereas a general-purpose processor accommodates changes flexibly.

### 2. Embedded System Use Scenarios: IoT vs. Cyber-Physical Systems (CPS)
The teacher introduces two primary deployment scenarios for embedded systems:

1. **Internet of Things (IoT)**
   - Household/everyday single-purpose devices (e.g., smart lights, refrigerators, ovens) containing small embedded chips that are centrally connected to a server or network so a user can control them.
   - The **end devices** themselves are lightweight household items and require **very little computing power**.

2. **Cyber-Physical Systems (CPS)**
   - Complex physical systems integrated with powerful, dedicated embedded computation.
   - **Example — Airplane**: An airplane contains a very powerful computer. It has numerous parameters and mechanisms (flaps, radar/rudder *(note: likely referring to flight control surfaces like rudder alongside flaps)*, pitch, yaw, etc.) that cannot all be controlled manually by a pilot simultaneously—if the pilot had to manage them manually, the plane could not fly. Most of these are automated: the pilot moves the steering control, and the onboard computer automatically calculates and adjusts which flaps move and by how much.
   - Despite being a powerful computer, it is still an **embedded system**, not a general-purpose PC: you cannot use it to play games or watch movies; it is built specifically to fly the plane.
   - **Example — Vehicles**: Modern cars and automated/autonomous vehicles (e.g., Tesla).

### 3. Edge Computing & Data Security (Cryptography)
- **Need for On-Site (Edge) Computing Power**:
  - End devices in embedded systems are often called **edge devices**.
  - Many operations on edge devices are **time-critical**. For example, an airplane in flight must continuously compute altitude and speed. Sending raw sensor data to a remote server for calculation and waiting for the result would be far too slow and could cause the plane to crash.
  - Therefore, edge devices must be **powerful enough** locally to perform their intended computation within required time limits (they do not need to be as powerful as a desktop PC, just sufficient to achieve their purpose).
- **Need for Security**:
  - Because computation happens locally on edge devices using sensitive operational data, that data must be secured.
  - **Example**: An autonomous car (e.g., Tesla) has many embedded chips. If a hacker compromises those chips, steering one way could cause the car to turn the other way.
  - Consequently, an embedded system design must ensure the device is sophisticated, performs real-time computation, meets timing constraints, and keeps its data secure.
- **Cryptography Concepts (Brief Overview)**:
  - *Problem*: Device A sends a message to Device B. Data stored inside each device can be kept private, but transmission passes over a **public medium**. How do we prevent others from reading it?
  - **Key Terminology**:
    - **Plaintext**: The original, human-readable data/message.
    - **Encryption**: Scrambling plaintext using a **key** so it looks like meaningless garbage to outsiders.
    - **Ciphertext**: The scrambled, unreadable output produced by encryption.
    - **Decryption**: Reversing the ciphertext back into plaintext using a key.
  - **Worked Example — Caesar Cipher**:
    - Shifts every alphabet character forward by a fixed distance $k$ (the **key**).
    - With key $k = 2$: `A` $\to$ `C` (2 positions after A), `B` $\to$ `D`, etc.
  - **Two Categories of Encryption**:
    1. **Symmetric-Key Cryptography**:
       - Uses the **same key** for both encryption and decryption (like a physical padlock—the same key locks and unlocks it).
       - **Example — AES (Advanced Encryption Standard)**: Considered the gold standard of symmetric-key encryption; used almost everywhere (e.g., WhatsApp end-to-end encryption).
       - **Why AES is fast**: Its entire operation consists of end-to-end **matrix multiplications**, which can be heavily parallelized. Because AES is so widely used, modern CPUs (in both PCs and smartphones) include dedicated hardware circuits/instructions specifically for AES (analogous to how GPUs are specialized chips for matrix multiplication in machine learning). *(Note: at 15:10 the teacher briefly said "asymmetric" by a slip of the tongue while referring to AES, which he had just defined as symmetric.)*
    2. **Asymmetric-Key Cryptography**:
       - Uses **different keys** for encryption and decryption *(note: in response to a student saying "encrypt with the receiver's private key," the teacher noted this is asymmetric cryptography and deferred the full key-usage explanation to the future Network Security course; standard public-key encryption uses the receiver's public key to encrypt and private key to decrypt)*.
       - **Example — RSA**: Covered in Discrete Mathematics; relies on large modular exponentiation ("big-mod" / power modulus) operations of the form $P^e \bmod n$.
       - **Drawback**: Computationally slower due to heavy modular exponentiation arithmetic.

### 4. Design Constraints & Challenges: Deadlines and Hardware Limits
- **Desktop Programming Goal vs. Embedded System Goal**:
  - **Desktop / General-Purpose PC**: Programmers aim to minimize time complexity (Big-O notation) and run code as fast as possible ("the faster, the better").
  - **Embedded Systems**: The goal is not "as fast as possible," but meeting a **specific deadline**.
    - Missing the deadline makes **even a mathematically correct output invalid**.
    - **Example — ABS (Anti-lock Braking System)**: When a biker hits the brake, within a few milliseconds the system must measure wheel speed and apply just the right brake pressure—neither locking the wheel completely nor leaving pressure so low that the wheel keeps spinning at full speed. If the ABS produces the correct answer after 1 minute, it is useless.
  - Meeting the **deadline** is the very first requirement to consider before anything else when designing an embedded system.
- **Hardware Speed Gap**:
  - Embedded microchips have significantly lower processing capability than PCs:
    - Desktop PC clock rate: typically $3\text{–}5\text{ GHz}$.
    - **STM32 F103** (the microcontroller used in this course): clock rate is **$72\text{ MHz}$**.
  - Because the clock speed is much slower, code that runs quickly on a PC will execute noticeably slower on the STM32. Therefore, code cannot be written casually—it must be optimized.
- **Two Core Constraints to Balance**:
  1. **Hardware Constraint**: Pick the fastest/best chip feasible for the system.
  2. **Software / Algorithm Constraint**: Design an efficient algorithm so that execution finishes within the deadline on constrained hardware.

### 5. Embedded System Design Process (5 Steps) & Worked Example
The design workflow is divided into **five sequential steps**:
1. **Requirement Analysis**
2. **Specification**
3. **Architecture**
4. **Component Design (Hardware & Software Components)**
5. **System Integration**

The teacher illustrates all five steps using a **Smart Plant Watering System** example:

#### Step 1: Requirement Analysis
- Captures the **need for the system** from the customer in plain English—without specifying *how* to build it or listing hardware equipment.
- **Customer request**: *"Design a small device that keeps the soil of a potted plant moist—automatically water it when dry, without letting it overflow."*
- Additional customer requests may include:
  - A **User Interface (UI)** to check soil humidity percentage (specifically: a text display, two small buttons, and one status LED).
  - A **cost limit** (e.g., do not exceed a certain dollar/taka budget).
  - A **size / physical weight constraint** (must fit right beside the flower pot without needing a separate room or extra space).
- **Requirement Form**: The designer documents these into a structured Requirement Form. Every system—whether an embedded system, a C function (takes parameters, processes them, returns output), or RUET's education system (students enter as input, RUET processes them, graduates exit as output)—must define **3 mandatory items**:
  1. **Inputs**
  2. **Functionality** (operations performed)
  3. **Outputs**
  - Additional fields (cost, physical weight/size, UI, etc.) are added depending on the customer's requirements.

#### Step 2: Specification
- Translates the customer's plain-language requirements into **concrete, ordered technical steps** the designer must implement to satisfy them.
- **For the Smart Plant Watering System**:
  - Use a **soil sensor** to monitor soil humidity periodically (e.g., once every **1 minute** instead of continuously, because periodic activation consumes much less power—applying the **energy efficiency** design principle).
  - If soil humidity falls below a lower threshold, activate a **water pump** to water the soil.
  - Once soil humidity rises past an upper threshold, turn the pump **off** (preventing overflow).

#### Step 3: Architecture
- Creates a **system blueprint / flow diagram** showing all subsystems, how they connect, and the order of operations.
- **Two main parts**:
  1. **Plant/Sensor side**: Soil moisture sensor sitting in the pot, sampling periodically.
  2. **User Interface side**: Text display, two buttons (e.g., manual override button), and status LED (indicating whether the sensor/pump is active).
- **Overall Flow**:
  - Moisture sensor periodically samples soil humidity $\to$ sends readings to the **control logic** (inside the microcontroller, e.g., STM32) $\to$ control logic decides whether to turn on the pump and sends status updates to the display.
- **Separating Architecture into Hardware and Software Sides**:
  - **Hardware Architecture** (physical components and connections):
    - Soil moisture sensor
    - Buttons
    - Water pump & pump driver
    - Text display & status LED
    - Microcontroller / CPU (e.g., STM32) to execute control logic
  - **Software Architecture** (firmware/logic modules and data flow):
    - **Timer**: Triggers the sensor to take a reading every 1 minute.
    - **Button Listener**: Detects manual button presses; overrides automatic moisture checks so pressing the button always activates the pump.
    - **Control Logic**: Combines Timer/Sensor input and Button Listener override (if button pressed $\to$ activate pump; else, check periodic sensor reading against threshold $\to$ activate/deactivate pump).
    - **Pump Control**: Sends the activation signal to the hardware pump driver.
    - **Display Driver**: Updates the text display and status LED.

#### Step 4: Designing Hardware & Software Components
- Actually building/selecting each hardware piece (sensor, pump driver, microcontroller, UI) and implementing each software module (timer, button listener, control logic, pump control, display driver) identified in the architecture.

#### Step 5: System Integration
- Combining all developed hardware and software components into a single, complete, tested product ready for the customer.

### 6. Functional vs. Non-Functional Requirements
- **Functional Requirements**: Describe **what the system does**—its core operations and behavior (e.g., "a smart plant watering system that waters soil when dry").
- **Non-Functional Requirements**: Everything **outside** the core functionality—constraints and quality attributes imposed on the design or delivery, such as:
  - **Cost** (e.g., budget cap of 1,000 BDT—this money doesn't go *into* watering the plant, it constrains how you design it)
  - **Performance**
  - **Physical size / weight** (e.g., compact enough to sit beside the pot)
  - **Project delivery deadline** (e.g., customer requiring delivery within 10 days)

## Exam / Important Points
- **General-purpose vs. Specific-purpose**: Be able to explain both cost and flexibility reasons why general-purpose processors are preferred.
- **IoT vs. Cyber-Physical Systems (CPS)**: Understand the distinction in computing power and use cases (lightweight household IoT devices vs. high-power automated CPS like airplanes and autonomous cars).
- **Deadlines in Embedded Systems**: Remember that in embedded systems, **meeting the deadline comes first**—a correct result produced past the deadline is **invalid** (know the ABS braking example).
- **Clock Rate Comparison**: Desktop PCs ($3\text{–}5\text{ GHz}$) vs. **STM32F103** ($72\text{ MHz}$)—know why code optimization is mandatory for embedded targets.
- **Cryptography Basics**: Know the difference between **symmetric-key** (same key, e.g., **AES**, fast due to parallelizable matrix multiplication & dedicated CPU hardware support) and **asymmetric-key** (different keys, e.g., **RSA**, slower due to modular exponentiation $P^e \bmod n$).
- **Design Flow (5 Steps)**: Requirement Analysis $\to$ Specification $\to$ Architecture $\to$ Component Design $\to$ System Integration.
- **Requirement Analysis vs. Specification**: Requirement is the customer's plain-English need; Specification is the designer's technical breakdown/steps to fulfill it.
- **Mandatory Elements of Any System / Requirement Form**: Inputs, Functionality, and Outputs.
- **Functional vs. Non-Functional Requirements**: Know how to classify requirements (e.g., cost, weight/size, performance, and delivery deadlines like "deliver within 10 days" are **non-functional**).
- **Sample Questions Mentioned from the End of the Slide**:
  - What is an embedded computer?
  - Is your laptop an embedded computer?
  - Difference between an IoT system and a Cyber-Physical System (CPS).

## Announcements & Logistics
- Microcontroller to be studied later in the course: **STM32F103** ($72\text{ MHz}$).
- Network Security / Cryptography will be covered in detail in a dedicated future course.
- No class tests, assignments, or external deadlines announced.

## Open Questions / Unclear Parts
- **00:00 – 00:14**: Opening remarks during classroom settling were very quiet/muffled before the recap question began.
- **02:02 – 02:29**: Teacher referred to a slide that had been edited/removed ("slide 9" or missing slide content), not visible in the audio.
- **21:30 – 23:25, 28:40 – 29:45, 36:25 – 37:45**: Long silent pauses while students read the lecture slides (e.g., Specification table, Architecture diagram, and end-of-slide sample questions). The specific exact wording of some slide text (such as the full list of sample questions at the end) is only partially read aloud.
- **37:45 – 39:07**: Attendance roll call at the end of the recording; cuts off mid-roll call around roll 9.
