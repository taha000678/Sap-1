# Sap-1
SAP-1 (Simple-As-Possible Computer) is a Logisim-based implementation of the classic 8-bit educational computer architecture proposed by Ben Eater. This project demonstrates the fundamental concepts of computer organization, including the fetch-decode-execute cycle, ALU operations, registers, memory, control logic, and instruction execution. It serves as a learning resource for understanding how a basic CPU works from the hardware level. 
# Block Diagram
<img width="1028" height="755" alt="image" src="https://github.com/user-attachments/assets/07afb332-5601-400e-8501-79fb006b77b3" />


## Steps to Implement SAP-1 in Logisim

1. **Create the Project**

   * Create a new Logisim project.
   * Set the clock and organize the workspace into datapath and control sections.

2. **Build the Registers**

   * Program Counter (PC)
   * Memory Address Register (MAR)
   * Instruction Register (IR)
   * A Register (Accumulator)
   * B Register
   * Output Register

3. **Design the Bus**

   * Implement an 8-bit shared data bus.
   * Connect all registers using tri-state buffers or multiplexers to avoid bus conflicts.

4. **Implement Memory**

   * Add a 16 × 8 RAM.
   * Connect the MAR to the RAM address input.
   * Load the program using a `.hex` file.

5. **Build the ALU**

   * Design an 8-bit adder/subtractor.
   * Connect inputs from the A and B registers.
   * Enable the ALU output onto the bus when required.

6. **Create the Program Counter Logic**

   * Implement increment functionality.
   * Add load and reset controls.
   * Connect the PC output to the bus.

7. **Design the Control Unit**

   * Implement the instruction decoder.
   * Generate control signals for each T-state (T0–T5).
   * Control register loading, bus output enables, memory read, ALU operations, and PC increment.

8. **Implement the Fetch Cycle**

   * **T0:** PC → MAR
   * **T1:** RAM → IR, PC++
   * **T2:** Decode instruction

9. **Implement the Execute Cycle**

   * Implement control sequences for each instruction:

     * **LDA** – Load accumulator
     * **ADD** – Add memory value to accumulator
     * **SUB** – Subtract memory value from accumulator
     * **OUT** – Transfer accumulator to output register
     * **HLT** – Stop clock

10. **Connect the Output Display**

    * Connect the Output Register to LEDs or a Hex Display.
    * Verify that results appear correctly.

11. **Load a Test Program**

    * Create a `.hex` program.
    * Load it into RAM.
    * Run the clock step-by-step and observe register values.

12. **Verify the System**

    * Test each instruction individually.
    * Check the fetch–decode–execute cycle.
    * Debug bus conflicts and incorrect control signals.
    * Finally, test complete programs (e.g., addition, subtraction, counting, continuous loop).

These steps result in a fully functional **SAP-1 processor** capable of executing simple 8-bit programs in Logisim.

# Program Counter 
The Program Counter (PC) is a 4-bit register that stores the address of the next instruction to be fetched from memory. It automatically increments after each instruction fetch or can be loaded with a new address when required, ensuring sequential execution of the program.
<img width="937" height="451" alt="image" src="https://github.com/user-attachments/assets/f97479ec-eb4a-4c50-baae-4a3615f770a3" />

# Register A 
Register A (Accumulator) is an 8-bit register that stores operands and intermediate results during arithmetic and logic operations. It receives data from the system bus and works with the ALU to perform calculations, holding the final result until it is transferred to another register or the output.
<img width="939" height="453" alt="image" src="https://github.com/user-attachments/assets/7467ecf9-ced7-4206-bbd0-17c3c3cedb26" />

# Memory Address Register (MAR)
The Memory Address Register (MAR) is a 4-bit register that stores the address of the memory location to be accessed. It receives addresses from the Program Counter or the instruction register and provides them to the RAM during instruction fetch and data access operations.
<img width="964" height="388" alt="image" src="https://github.com/user-attachments/assets/92984934-17f4-4293-9f4e-17f92f674d4e" />

# Arithemetic Logic Unit (ALU)
The Arithmetic Logic Unit (ALU) is an 8-bit combinational circuit that performs arithmetic operations such as addition and subtraction. It takes inputs from Register A and Register B, processes them using an adder/subtractor circuit, and places the result on the system bus for storage or output.
<img width="893" height="303" alt="image" src="https://github.com/user-attachments/assets/a3bc4867-0445-4a70-966f-947ef83375d3" />

# Register B 
Register B is an 8-bit register that temporarily stores the second operand for arithmetic operations. It receives data from the system bus and provides it to the ALU, where it is used along with Register A to perform addition or subtraction.
<img width="711" height="380" alt="image" src="https://github.com/user-attachments/assets/3db8b710-163e-4b90-b698-7cf275bcf76c" />

# Random Access Memory (RAM)
RAM is a 16 × 8-bit memory module that stores both program instructions and data. It receives memory addresses from the Memory Address Register (MAR) and outputs the corresponding instruction or data onto the system bus during the fetch and execute.
<img width="791" height="344" alt="image" src="https://github.com/user-attachments/assets/dcddd706-4b54-4a17-874e-1d2c0d39719c" />

# Instruction Register 
The Instruction Register (IR) is an 8-bit register that stores the current instruction fetched from memory. It separates the opcode and operand, allowing the control unit to decode the instruction and generate the appropriate control signals for execution.
<img width="858" height="334" alt="image" src="https://github.com/user-attachments/assets/99037a49-8da8-4a4e-b4cf-4f85a421bea7" />

# Ring Counter 
The Ring Counter is a sequential circuit that generates the timing signals (T0–T5) required for the SAP-1 instruction cycle. It advances one state on each clock pulse, synchronizing the fetch, decode, and execute operations by activating the appropriate control signals at each step.
<img width="1020" height="501" alt="image" src="https://github.com/user-attachments/assets/b368361f-c8f6-4861-9d0a-c9adef9ab802" />

# Output Register and Hex Display 
The Output Register is an 8-bit register that stores the final result produced by the ALU or accumulator. It receives data from the system bus and holds it until it is displayed. The Hex Display is connected to the Output Register and converts the stored 8-bit binary value into a hexadecimal representation, allowing the processor's output to be easily monitored and verified.
<img width="849" height="494" alt="image" src="https://github.com/user-attachments/assets/fd84f279-6ce0-4c70-8507-60557e532aa4" />

# Control Unit (Decoder)
The Control Unit (Instruction Decoder) decodes the opcode stored in the Instruction Register (IR) and generates the control signals required to execute each instruction. Working together with the Ring Counter, it activates the appropriate control lines during each timing state (T0–T5), coordinating data transfers between registers, memory, the ALU, and the system bus to complete the fetch–decode–execute cycle.
<img width="1012" height="859" alt="image" src="https://github.com/user-attachments/assets/f0a9e544-c71a-4efc-87b5-d664e12f8680" />

# Main Circuit 
The Main Circuit integrates all the major components of the SAP-1 computer, including the Program Counter (PC), Memory Address Register (MAR), RAM, Instruction Register (IR), Register A, Register B, ALU, Control Unit, Ring Counter, Output Register, and the shared 8-bit system bus. It coordinates the interaction between these components to perform the fetch–decode–execute cycle, enabling the processor to execute instructions and display the final output correctly.
<img width="775" height="863" alt="image" src="https://github.com/user-attachments/assets/4b379c8c-ceed-4819-bbf1-eae4067406de" />




