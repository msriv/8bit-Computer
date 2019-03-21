

# 8bit Computer

Developed by Hatim Nomani(@hatimmnomani) and Mihir Srivastava(@msriv)

Our project for the course Computer Architecture, the following is the working and specification of this 8-bit Computer. 

The CPU is shown below. It consists of all the necessary components required by any CPU. This simulation is done on Logisim.

![CPU](/home/msrivastava/Documents/SEMESTER4/Computer_Architecture/Git_Repo/CPU.png)



We will cover the necessary component specification below. 



1. **Arithmetic Logic Unit**


The unit that controls all the logical and arithmetic operations. 

![ALU](new.png)



The codes written along the ALU are the inputs in the `MUX_Con` . 



| MUX_Con Address | Description |
| :-------------: | :---------: |
|      0000       |  A Buffer   |
|      0001       |  B Buffer   |
|      0010       |   A AND B   |
|      0011       |   A OR B    |
|      0100       |     A-B     |
|      0101       |     A++     |
|      0110       |     B--     |
|      0111       |     A+B     |
|      1000       |     !A      |
|      1001       |     !B      |



2. **Register Bank**

![Register Bank](/home/msrivastava/Documents/SEMESTER4/Computer_Architecture/Git_Repo/regbank.png)



This is 8-bit x 16 register, Register Bank. It consists of 16 Registers which store values whenever the clock is triggered. The `WRITE_MODE` trigger is to switch write mode on and off, so we don't have the problem of erasing the data already existing in the register bank. `WRITE_IN_ADDRESS` is the address of the register where data needs to be written. `OUT_ADDRESS 1` and`OUT_ADDRESS 2` are the addresses of the two operands we will require from the register bank.  



3. **Control Unit**

![](/home/msrivastava/Documents/SEMESTER4/Computer_Architecture/Git_Repo/CU.png)



The Control Unit just uses the opcode to determine which flags to turn on or off and the `WRITE_SOURCE` control line as visible in the diagram above. The `REG_WRITE` controls the `WRITE_MODE` in the Register Bank. The `JMP` controls the instruction to which we need to jump. The `PWR` flag controls the Program Counter and stops the increment cycle so that no more instructions can be read.

The instruction is a group of 16-bit binary which is segmented into the following format, 

![](/home/msrivastava/Documents/SEMESTER4/Computer_Architecture/Git_Repo/Instruction.png)

|   OPCODE    |                         Description                          |
| :---------: | :----------------------------------------------------------: |
|    0000     |                       OReg &larr; IMM                        |
|    0001     |                      OReg &larr; REG_B                       |
|    0010     |                 OReg &larr; REG_B AND REG_A                  |
| 0011 - 1001 | Same as 0010 for different ALU operations as mentioned above. |
|    1010     |                   LOAD OReg &larr; MEM[A]                    |
|    1011     |                   STORE OMEM &larr; REG_A                    |
|    1100     |                      PC &larr; JUMP_DES                      |
|    1111     |                             HALT                             |

When the Opcode is 0000, the least significant 8-bits act as an immediate value in the instruction which is written inside a register in the register bank. For all the Opcode other than 0000, the least significant 8-bit are divided into 4-bit pair in which they store the values of addresses of Register B and Register A respectively. 
