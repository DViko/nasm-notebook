# 🖥️ Computer Architecture

> **Computer architecture** is the organization, structure, and behavior of a computer system, including the interaction between hardware and software.

### 🔹 CPU

> The **CPU (Central Processing Unit)** executes program instructions, processes data, and coordinates the operation of system components.

- **Key CPU components:**
  - **Control Unit (CU):** controls the operation of the processor.
  - **Arithmetic Logic Unit (ALU):** performs arithmetic and logical operations.
  - **Registers:** small and extremely fast memory cells inside the processor used for immediate data access. They store operands, memory addresses, stack pointers, and computation results.

### 🔹 Memory

> Memory is typically divided into two main types.

- **Primary Memory (RAM):**
  - Temporarily stores currently used data and programs.
  - Provides fast access (slower than registers but faster than storage devices).
  - Volatile memory: data is lost when power is turned off.

- **Secondary Memory (Storage):**
  - Stores data for long-term use.
  - Provides slower access.
  - Non-volatile memory: data is preserved when power is turned off.

### 🔹 Bus

> A **bus** is a communication system that transfers data between components inside or outside the computer.

- **Main bus types:**
  - **Address Bus:** transfers the memory or device address being accessed.
  - **Control Bus:** transfers control signals such as read or write operations.
  - **Data Bus:** transfers the actual data being read or written.


- **How the bus works (memory read example):**
  - **Address Bus:**
    - The processor places the target memory address on the address bus.
  - **Control Bus:**
    - The processor places a control signal on the control bus indicating whether it wants to perform a read or write operation.
      - **Read:** the processor activates the read signal, after which memory places data onto the data bus.
      - **Write:** the processor activates the write signal, after which data from the data bus is written into memory.
  - **Data Bus:**
    - Contains the actual data being transferred.
      - **Read:** the value from the target memory address is placed onto the data bus and then read by the processor.
      - **Write:** the value to be written is placed onto the data bus.

---

## ⚙️ Memory Hierarchy

> The **memory hierarchy** consists of different levels of memory in a computer system, each with different speed and storage capacity.

- **Register:**
  - Stores operands, addresses, and stack pointers. Provides the fastest possible access to data required for arithmetic operations, logical operations, control flow, and data processing.
  - **Location:** inside the processor.
  - **Speed:** the fastest type of memory.
  - **Size:** very small (typically tens of bytes).
- **Cache Memory:**
  - Stores frequently used data and instructions, reducing access time to main memory.
  - **Organization:**
    - **L1 Cache:** the smallest and fastest cache.
    - **L2 Cache:** larger and slightly slower than L1.
    - **L3 Cache:** even larger and slower, shared between processor cores.
  - **Location:** usually located on the processor die.
  - **Speed:** very fast.
  - **Size:** relatively small, from several KiB to several MiB.
- **Main Memory (RAM):**
  - Stores currently used data and instructions.
  - **Location:** outside the processor (on the motherboard).
  - **Speed:** fast.
  - **Size:** several GiB.
- **Secondary Storage:**
  - Used for permanent data storage.
  - **Location:** outside the processor.
  - **Speed:** slow.
  - **Size:** from hundreds of GiB to several TiB.
- **Tertiary Storage:**
  - Used for backups and data archiving.
  - **Location:** external storage systems.
  - **Speed:** the slowest type of storage.
  - **Size:** can be very large.

---

## ⚙️ Endianness

> **Endianness** is the order in which bytes are stored or transmitted in memory. It is important for understanding how data is represented in assembly language and how the processor accesses multi-byte data types.

**Two main byte orders:**

- **Big-Endian:**
  - The **Most Significant Byte (MSB)** is stored at the lower memory address.
  - The **Least Significant Byte (LSB)** is stored at the higher memory address.
  - Example: the 32-bit integer ` 0x12345678 ` is stored in memory as:
  ```text
    | Address | Value |
    | :------ | :---- |
    | 0x00    | 0x12  |
    | 0x01    | 0x34  |
    | 0x02    | 0x56  |
    | 0x03    | 0x78  |
  ```

- **Little-Endian:**
  - The **Least Significant Byte (LSB)** is stored at the lower memory address.
  - The **Most Significant Byte (MSB)** is stored at the higher memory address.
  - Example: the 32-bit integer ` 0x12345678 ` is stored in memory as:
  ```text
    | memory address | value stored at the address |
    | :------------- | :-------------------------- |
    | 0x00           | 0x78                        |
    | 0x01           | 0x56                        |
    | 0x02           | 0x34                        |
    | 0x03           | 0x12                        |
  ```

### 🔹 Data Interpretation

- **Data interpretation:**
  - Byte order affects how data is interpreted when read from memory.
  - A program reading data using one byte order may incorrectly interpret data written using another byte order.
- **Network protocols:**
  - Many network protocols use the **big-endian** format, also known as **Network Byte Order**, to ensure consistency between systems.
  - Systems often need to convert their native byte order into **big-endian** format before transmitting data over a network.
- **Cross-platform compatibility:**
  - Byte order may cause issues in cross-platform software development.
  - If one system uses **little-endian** and another uses **big-endian**, data structures must be converted appropriately when shared between systems.

> ⚠️ Note: x86/x86-64 architectures use **little-endian**.
---

## ⚙️ Instruction Set Architecture (ISA)

> **ISA (Instruction Set Architecture)** is the interface between hardware and software that defines the set of instructions a processor can execute.

### 🔹 Key ISA Components

- **Instruction Set:**
  - The complete set of instructions the processor can execute, including arithmetic operations, logical operations, control flow, data movement, and more.
  - Instructions are commonly divided into the following categories:
    - **Data Movement Instructions:** move data between registers, memory, and I/O devices (` MOV, PUSH, POP `, etc.).
    - **Arithmetic Instructions:** perform mathematical operations (` ADD, SUB, MUL, DIV `).
    - **Logical Instructions:** perform bitwise operations (` AND, OR, NOT, XOR `).
    - **Control Flow Instructions:** change the execution flow (` JMP, CALL, RET `).
    - **Input/Output Instructions:** transfer data to and from peripheral devices (` IN, OUT `).

- **Addressing Modes:**
  - Methods used to specify instruction operands.
  - Common addressing modes:
    - **Register:** operand is stored in a register: ` mov eax, ebx `
    - **Indirect:** address is stored in a register: ` mov eax, [ebx] `
    - **Immediate:** operand is a constant embedded directly in the instruction: ` mov eax, 5 `
    - **Direct (Memory):** memory address is explicitly specified: ` mov eax, [0x1234] `
    - **Indexed:** uses a base address, index, and offset: ` mov eax, [ebx + ecx*4] `
- **Registers:**
  - Small, high-speed memory locations inside the CPU used for temporary data storage during instruction execution.
  - **Main register types:**
    - **General-Purpose Registers:** used for general data operations (` RAX, RBX, RCX, RDX `, etc.).
    - **Special-Purpose Registers:** used for specific functions (` RSP, RBP `, etc.).
- **Instruction Formats:**
  - An instruction usually contains the following fields:
    - **Opcode:** specifies the operation to perform.
    - **Operands:** specify the data being processed, such as registers, immediate values, or memory addresses.
    - **Addressing Mode:** specifies how operands should be interpreted.
- **Control Signals:**
  - Signals generated by the CPU control unit to manage instruction execution, including memory read/write operations, ALU activation, and control flow management.


### 🔹 Types of Instruction Set Architectures

- **CISC (Complex Instruction Set Architecture)**
  - Contains a large number of instructions, including complex instructions capable of performing multiple operations in a single instruction.
  - ` x86 architecture (Intel, AMD) `
- **RISC (Reduced Instruction Set Architecture)**
  - Contains fewer instructions.
  - Instructions are generally simpler and more uniform in execution time.
  - Emphasizes a load/store architecture where memory access is restricted to dedicated LOAD/STORE instructions.
  - ` ARM, MIPS architecture `
- **VLIW (Very Long Instruction Word)**
  - Uses long instructions that combine multiple operations into a single instruction block.
  - The compiler is responsible for scheduling instructions to execute in parallel.
  - ` Itanium architecture `
- **EPIC (Explicitly Parallel Instruction Computing)**
  - An extension of ` VLIW `.
  - Designed to exploit instruction-level parallelism by explicitly specifying parallel operations in the instruction set.
  - The compiler is responsible for scheduling instructions for parallel execution.
  - ` Intel Itanium `


### 🔹 Importance of ISA

- **Compatibility:** determines software compatibility. Programs written for one ISA may not run on another ISA without recompilation or emulation.
- **Performance:** affects CPU and overall system performance characteristics.
- **Programming:** influences compiler design and programming language implementation by defining how high-level instructions are translated into machine code.

---

## ⚙️ Interrupts

> **Interrupts and exceptions** are mechanisms used by the processor to handle events that disrupt the normal execution flow of a program. Both allow the CPU to respond to hardware signals, software requests, and error conditions, but they differ in their causes and handling methods.

### 🔹 Types of Interrupts

- **Hardware Interrupts:**
  - Generated by external devices such as keyboards, mice, or network cards.
  - For example, pressing a key on a keyboard generates an interrupt that allows the processor to handle the event.
  - Common use cases:
    - I/O operations, timers, system events.
- **Software Interrupts:**
  - Triggered by executing a special instruction in a program, often for system calls or privileged operations.
  - Example: requesting operating system services such as file reading or writing.

### 🔹 Interrupt Handling Process

When an interrupt occurs, the processor typically performs the following steps:

- **Save the current process state:**
  - Registers and the instruction pointer of the current task are saved.
- **Handle the interrupt (ISR):**
  - Control is transferred to the interrupt service routine.
- **Process the event:**
  - Example: reading data from an I/O device or handling a timer event.
- **Restore the state:**
  - The processor restores the saved state and resumes execution of the interrupted task.


### 🔹 Interrupt Characteristics

  - **Asynchronous:** interrupts may occur at any moment during program execution.
  - **External or software-triggered:** interrupts originate from external devices or special software instructions.
  - **Prioritized:** interrupts may have different priority levels.


## ⚙️ Exceptions

> **Exceptions** are events generated during instruction execution, often caused by errors or special conditions that must be handled by the processor or operating system.

### 🔹 Types of Exceptions

- **Trap:**
  - Intentionally generated by software, usually through a system call or special instruction.
  - A program may use a trap to request operating system services such as memory allocation or file processing.
- **Fault:**
  - Caused by instruction execution errors such as invalid memory access (segmentation fault).
  - The operating system or exception handler may attempt to correct the problem. If successful, the program may continue execution; otherwise, the program is terminated.
- **Abort:**
  - Caused by severe hardware or system errors such as memory parity failures or hardware malfunctions.
  - Usually unrecoverable and often leads to program termination or a system crash.

### 🔹 Exception Handling Process

When an exception occurs, the processor usually performs the following steps:

- **Save the current state:**
  - The processor saves the program state (registers and instruction pointer).
- **Transfer control to the exception handler:**
  - The processor invokes the handler responsible for the specific exception.
- **Handle the exception:**
  - The handler may attempt to resolve the issue.
- **Resume or terminate execution:**
  - Depending on the exception type, the program may continue or terminate.


### 🔹 Exception Characteristics

- **Synchronous:** exceptions occur during instruction execution.
- **Instruction-related:** exceptions are associated with a specific instruction or processor state.

## ⚙️ Key Differences Between Interrupts and Exceptions

```text 
    | Characteristic | Interrupt                               | Exception                                         |
    | :------------- | :-------------------------------------- | :------------------------------------------------ |
    | Source         | External device or software instruction | Internal CPU event                                |
    | Timing         | Asynchronous (can occur at any time)    | Synchronous (during instruction execution)        |
    | Cause          | I/O events, hardware signals            | Instruction errors, system calls                  |
    | Handling       | Uses interrupt service routines (ISR)   | Uses exception handlers                           |
    | Priority       | Often prioritized                       | Usually requires immediate handling               |
    | Recovery       | Program execution can usually continue  | Some exceptions are recoverable, others terminate |
```
---