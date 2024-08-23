# 6T-SRAM-
6T-SRAM cell and 8x8 memory array - silicon design (Cadence)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
6T-SRAM unit - 1 bit memory cell that has 3 modes (HOLD/WRITE/READ):

Schematic and physical design of a memory cell using 4 NMOS and 2 PMOS transistors. 2 NMOSs and PMOSs are used to apply two NOT gates that connected each output to the other's input so that any value (logic HIGH/LOW) will be helded as long as the HOLD mode is on (description below) ofcorse we need to state which net is considered to be the bit value "Q", and which is the complementary one "QB". The other two transistors are NMOSs used as switches between the NOT gates and the Bit Lines (BL to the Q net, BLB to QB net).

HOLD mode: 
ON- means that the switches between the Bit Lines and the NOT gates are closed so that the logic value in the cell is preserved. 
OFF- means that the switches between the Bit Lines and the NOT gates are open so now the cell is in a READ or WRITE mode.

WRITE mode:
Before writing a value we need to load the BL with the wanted value (HIGH/LOW) and the BLB with the opposite value. After loading, we need to open the switches (means that HOLD mode is off) so that the Q and QB nets will get the loaded value.

READ mode:
Before reading the value from the cell, we need to set the BL and BLB with HIGH values. After loading, we need to open the switches (means that HOLD mode is off). The BIT line that is connected to a LOW valued net will have a charge leakage through the NMOS transistor of the feeding NOT gate, while the other BIT line will be remained with full charge. The two BIT lines are connected to a sensitive Comperator which can recognize which Bit Line has the charge leakage. The value observed from the Comperator will be the Q value. (BL is connected to the "+" input of the Comperator, and vise versa to BLB)

**IN THIS PROJECT, COMPERATOR IS NOT INCLUDED.**
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

8X8 6T-SRAM Array:
The 6T-SRAM units are ordered in an 8X8 2-D array in a way that each row gets it's WL Line which controlls ALL of the cell's switches of the line (8 cells- 16 switches). Each column gets a BL,BLB lines. 

If we want to HOLD the array values, all we need to do is to reset (LOW) all the lines (WL,BL,BLB)- **THIS IS THE DEFAULT OF THE ARRAY**. 

If we want to WRITE to a specific cell, we will choose the column of our wanted cell, set its (**and only its**) BL,BLB according to our demand. After that we will set (HIGH) **only** the WL Line of the cell's line. That way we are implementing the WRITE operation on our specific cell. 

If we want to READ to a specific cell, we will choose the column of our wanted cell, set its (**and only its**) BL,BLB to HIGH. After that we will set (HIGH) **only** the WL Line of the cell's line. Each column has its own Comperator. That way we are implementing the READ operation on our specific wantes cell. 

**EXAMPLE (GOTO: 8X8 SRAM Array- Test Bench.png)** : In this example we can see that we are set to WRITE or READ from cell (4,6). The 4th WL gets the electrical voltage "WL4". The 6th BL, BLB gets the electrical voltage of BL6, BLB6 respectively. All the rest of the lines are in logic LOW voltage (DGND). 

