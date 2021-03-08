# VSD-IAT_Workshop_VLSI-SOC_PHYSICAL_DESIGN_using_open_source_eda_tools

![image](https://user-images.githubusercontent.com/79994584/110278790-f2afe800-7ffd-11eb-96f0-c4f980cf6ca5.png)

*3 MARCH 2021 - 7 MARCH 2021*

The main focus of this 5 day workshop was to learn the installation procedures of open source EDA tools required for IC design and simulation and get the hands on practice with each tool focussing on the Physical Design basics at a beginner level.

# Day 1

**Study and Review various components of RISC-V based picoSoC**
--------------------------------------------------------------

* IC design components terminologies
* Let's talk to computers
* Get familiar to open-source EDA tools

1. ***IC design component terminologies***

QFN-48 Package - A Chip sits in the centre of the package. It helps a chip in getting integrated to a larger system. QFN stands for Quad Flat No leads and 48 is the number of ports of the chip. Its dimensions are 7nm * 7nm.

Chip - Various components are integrated onto a single chip.

Pads - Through them signals can be sent to and from the chip. 

Core - Area where all the digital logic (AND gate,OR Gate, MUX etc.) is placed.

Die - Size of the entire chip, which gets manufactured on the silicon wafer.

IP - Called as Intellectual Property , Eg: PLL, ADC, DAC, SRAM are foundry IPs.

Foundry - A Big factory which manufactures the chips. A VLSI engineer has to continously communicate with the foundaries with some interface. Interface is nothing but some files which are provided by the foundary.

2. ***Let's Talk to computers***

**Introduction to RISC-V - Instruction Set Architecture(ISA)**
Basic idea---> If a C program is to be run on a hardware layout i.e. chip , so the information is first compiled in the RISC-V assembly language program, which gets converted to binary language (Os and 1s) and finally the bits get executed into the layput and we receive the required output.
Another interface to be present between RISC-V Architecture and the layout is the HDL (Hardware Description Language). Hence we create RISC-V specifications using RTL. Example: picorv32 cpu core - implements the specifications and then performs PNR to GDS flow.

RISC-V Architecture ===> Implementation (picorv32 cpu core) ===> Layout (qflow)

**From Software Applications to Hardware**
The complete flow of how the software applications run on hardware.

3. ***Get familiar to open-source EDA tools***

**Step 1 : Logic Synthesis** - RTL netlist has all the functionalities defined which has to be converted to a synthesized netlist comprising of logic gates. 
Open source EDA Tool for Logic syntesis - **Yosys Open Synthesis Suite** : it takes the RTL information , timing .libs  and converts it into a logical netlist which is a combination of gates and flip flops. 

**Step 2 : Floorplanning**  - It is the arrangement of blocksin a chip. Open source EDA Tool **Graywolf**

**Step 3 : Placement** - Open source EDA Tool **Graywolf**

**Step 4 : CTS (Clock Tree Synthesis)** - Route the clock in a way speciified by the designer. Open source EDA Tool **Graywolf**

**Step 5 : Routing** - Routes all the components placed in the placement stage. Open source EDA Tool for Routing - **QRouter**

Common step which is performed at each step is the STA( Static Timing Analysis ) - Open source EDA Tool for STA - **Opentimer** : Open Source high performance timing analysis Tool.

Layout Viewer - **Magic - Layout Viewr**

Pre-layout and Post-layout spice simulations - **Ngspice**

Schematic Editor - **eSim** : Complex circuit design , SPICE Simulations and Analysis and PCB Design.

**Qflow** - Is a tool chain for performing complete RTL2GDS.

***Virtual Box is needed to install Linux OS on Windows so that you can install all these necessary Open Source EDA tools***


*Day1- Hands On*
----------------
Open the Terminal in Linux OS.

-> Type "which sta" and what path do you see the sta tool to be linked to?

![image](https://user-images.githubusercontent.com/79994584/110287876-35c58780-800d-11eb-9a0a-7c2b64b691a9.png)

-> Type the command from current working directory : `git clone https://github.com/kunalg123/vsdflow.git` What is the last line you see ?

![image](https://user-images.githubusercontent.com/79994584/110288261-bdab9180-800d-11eb-8c03-136345edc1b6.png)

-> Type below commands:

`cd vsdflow`

`./vsdflow spi_slave_design_details.csv`

![image](https://user-images.githubusercontent.com/79994584/110289473-7c1be600-800f-11eb-8b03-53fb96cb6495.png)

![image](https://user-images.githubusercontent.com/79994584/110289554-981f8780-800f-11eb-937a-b29891ad108d.png)

![image](https://user-images.githubusercontent.com/79994584/110289579-a1a8ef80-800f-11eb-8316-8b0bcedef254.png)

![image](https://user-images.githubusercontent.com/79994584/110289597-aa99c100-800f-11eb-8b14-1da27cb213bd.png)

![image](https://user-images.githubusercontent.com/79994584/110289621-b2596580-800f-11eb-8195-4da397ac9dbd.png)

![image](https://user-images.githubusercontent.com/79994584/110289673-c4d39f00-800f-11eb-990c-b93e5d08407b.png)

Now, `ls -ltr outdir_spi_slave/`

![image](https://user-images.githubusercontent.com/79994584/110289800-f482a700-800f-11eb-99a8-c7c0f2b65e1a.png)

Here you will see lot of files created.

Now type below command

`ls -ltr outdir_spi_slave | wc`

![image](https://user-images.githubusercontent.com/79994584/110289927-1da33780-8010-11eb-9c39-c4d994c6615b.png)

This will give you 3 numbers in one row, where 1st number represents number of files.
What are the number of files you see?

Hint - The keyword "total 320 which is the first line you see when you type "ls -ltr outdir_spi_slave" is NOT a file.

-> Type below commands:

`cd outdir_spi_slave`

`qflow display spi_slave`

![image](https://user-images.githubusercontent.com/79994584/110290251-91dddb00-8010-11eb-9a9b-6976a3fef789.png)

It will open 2 windows "layout1" and "tkcon".

![image](https://user-images.githubusercontent.com/79994584/110290290-9efaca00-8010-11eb-9fea-b3786f6d8a13.png)

On "tkcon" window, type "box"

![image](https://user-images.githubusercontent.com/79994584/110290342-b2a63080-8010-11eb-8ce2-72f7513dc219.png)

It gives the output area in Microns . Which comes out to be 15420.24 microns.

-> Type below command

`cd`

`cd vsdflow`

`mkdir my_picorv32`

`cd my_picorv32`

`mkdir source synthesis layout`

`cp ~/vsdflow/Verilog/picorv32.v source/.`

`qflow gui &`

![image](https://user-images.githubusercontent.com/79994584/110290890-4aa41a00-8011-11eb-9870-b241b0035f4a.png)

![image](https://user-images.githubusercontent.com/79994584/110290918-5263be80-8011-11eb-979c-7d71fa98a33f.png)

![image](https://user-images.githubusercontent.com/79994584/110290937-57c10900-8011-11eb-85fd-d6b2a0b71975.png)

![image](https://user-images.githubusercontent.com/79994584/110290977-63accb00-8011-11eb-900a-740905768207.png)

Select below options in gui

![image](https://user-images.githubusercontent.com/79994584/110291030-732c1400-8011-11eb-9011-373d601e8fe8.png)

![image](https://user-images.githubusercontent.com/79994584/110291068-7de6a900-8011-11eb-9b75-bb4d2173b672.png)

Click on Set Stop

What is the % ratio of flipflop/total logic ?

![image](https://user-images.githubusercontent.com/79994584/110291156-9c4ca480-8011-11eb-9154-3f8772fadc80.png)

Click on Run to run the synthesis.

![image](https://user-images.githubusercontent.com/79994584/110291202-a7073980-8011-11eb-9a0e-f96f985ad072.png)

Again click on run and then click on Okay in Synthesis

![image](https://user-images.githubusercontent.com/79994584/110291254-ba1a0980-8011-11eb-9a11-11e39637877a.png)

You will see the log file

![image](https://user-images.githubusercontent.com/79994584/110291285-c43c0800-8011-11eb-867b-1489b69866cd.png)

The number of flip flops here are 1613 and the total no. of cells are 13197

So, 1613/13197 = 0.1222 * 100 = 12.222 %

Hence, 12.222% of the entire combinational logic is flip flops. 


# Day 2

**Chip planning strategies and introduction to foundry library cells**
---------------------------------------------------------------------

**1. Ultilization factor and aspect ratio**

The first step in physical design is to define the height and width of the core and die.

**Die** - It encapsulates the core and it is where the fundamental circuit gets fabricated.

**Core** - It lies inside the die wherein the fundamental logic of design is placed.

Inorder to maximize the throughput we have multiple dies on a single wafer.

***When Netlist occupies 100% of the core area, it means that the utilization of chip is 100%***

**Utilization factor - Area occupied by the Netlist / Total area of the core**

Ideally we do not aim at 100% utilization instead 60-70% utilization is what we look at so that there is room for optimization at later stages.

**Aspect Ratio = Height / Width**

***When the Aspect ratio is 1, it means that the chip is square shaped. While values of aspect ratio other than 1 represent that the chip is rectangular in shape.***

**2. Preplaced Cells**

These are cells which have user defined locations and therefore are already present in the chip before automated placement and routing. Automated placement and routing tools places the remaining logical cells in the design onto chip. Few examples of Pre-placed cells are memories, muxes, etc. They are placed in the core according to the design scenario. For example if the pre-placed cells have more number of inputs then they are placed close to the input side and if they have more number of outputs then they are placed close to the output side.

Arrangement of these IPs in a chip is referred to as Floorplanning.

**3. De-Coupling capacitors** 

When the logic 1 or 0 is not exactly 1 or 0 due to the drop in supply voltage , due to its physical location (far away). Hence if the input and output is within the Noise Margin then the situation is still finebut if it is not then it a huge problem so to fix this we use de - coupling capacitors which store alot of charge and are connected close to the logic circuit physically so that they provide the circuit full supply required and hence de - couples the logic circuit from the supply V, Vdd. When the logic is from 1 to 0, the de-coupling capacitor gets discharged through the Vdd. 
***Therefore de-coupling capacitors are placed close to the input cells.***

The de-coupling capacitors take care of local communication but for global communication **power planning** is used. 


**4. Power Planning** 

***The initial problem was that each circuitry demanded supply at the same time by the de-coupling capacitor.***

Hence all the de - coupling capacitors which where charged to V Volts will have to discharge to 0 through single Gnd, causing a bump in the ground tap point. This problem is known as **Ground Bounce**.

When the de -coupling Capacitors which were at 0 Volts are to be charged to V Volts through a single Vdd, causing lowering of Vdd tap point. This problem is known as **Voltage Droop**.


***So the solution to the above two problems is to use multiple Vdd and Vss***. 

This is called the **Mesh**, and is how the power planning will be done.


**5. Pin Placement**

A netlist gives the connectivity information between gates which is written in the HDL. The pin placement is the used space between die and core. 
The Frontend engineer defines the netlist connections while the backend engineer defines the pin placement. The clock ports are usually bigger in size in comparison to other data pins because the clock is continously drives all the flip flops in the design and to get minimum resistance as R is inversly proportional to A.

***Logical cell placement Block*** - It is placed in the core before the automated placement an routing tools place the other blocks.

**6. Cell Design Flow**

It comprises of three things.

1. Inputs - They include **PDK (Process Design Kit**) *which comes from the foundry* and consists of DRC and LVS rules, SPICE Models, library and user defined specs.
2. Circuit Design Steps -*Cell height* is decided by the distance betwee the power and ground rails, supply voltage, metal layers, pin locations, drawn gate length. 
3. Outputs


***Day2- Hands On***


![image](https://user-images.githubusercontent.com/79994584/110300777-4e3d9e00-801d-11eb-8b99-b82399c51254.png)


![image](https://user-images.githubusercontent.com/79994584/110300793-54337f00-801d-11eb-8a60-ed4147ff46d7.png)


Set the technology node 180nm and the Verilog module as picorv32

And click on set stop

Then Run 

![image](https://user-images.githubusercontent.com/79994584/110300836-68777c00-801d-11eb-8116-908b0a4a1651.png)


Then run the synthesis

![image](https://user-images.githubusercontent.com/79994584/110300873-73321100-801d-11eb-9c14-4a52dd57e6a0.png)


Then check again by clicking on Okay

![image](https://user-images.githubusercontent.com/79994584/110300903-7deca600-801d-11eb-8dd7-e8fe009c873f.png)


Checked for the gate count as 13197 and the FF count as 1613

Then close it

Now the Initial density is the Utilization factor so we will keep it as 70% i.e. 0.7

Aspect ratio wil be kept as 1.0 as we want a square chip

![image](https://user-images.githubusercontent.com/79994584/110300971-9361d000-801d-11eb-8ae0-b1a75e68b146.png)


Then click on Arrange Pins

![image](https://user-images.githubusercontent.com/79994584/110301022-9e1c6500-801d-11eb-9143-e936976cccaf.png)


Then click on Auto group

![image](https://user-images.githubusercontent.com/79994584/110301071-aa082700-801d-11eb-9b84-849b4c874c45.png)


And Apply

This will save the existing grouping 

And now click on arrange pins again

We have to group clk and reset so first we will create a new group

![image](https://user-images.githubusercontent.com/79994584/110301134-bc826080-801d-11eb-8051-fe9e5550c3a4.png)


Drag and drop clk and rset to the newly created group

![image](https://user-images.githubusercontent.com/79994584/110301174-c60bc880-801d-11eb-9c78-60ba8f45ca44.png)


Uncheck the top , Right , Left and then check fixed for clk and reset and then apply

![image](https://user-images.githubusercontent.com/79994584/110301213-d15ef400-801d-11eb-81a4-feef73166071.png)


![image](https://user-images.githubusercontent.com/79994584/110301230-d623a800-801d-11eb-8f40-37f78dd8c73c.png)


Check for the Placement run 

![image](https://user-images.githubusercontent.com/79994584/110301284-e63b8780-801d-11eb-9d6a-24407278b0b6.png)

After 30-35 mins your placement runs will finish by then,

-> Type below command

`cd`

`cd vsdflow/my_picorv32`

`qflow display picorv32 &`

![image](https://user-images.githubusercontent.com/79994584/110301737-6f52be80-801e-11eb-8eaa-755f2259e1f6.png)

This will open layout and tkcon window In the layout window, select whole chip using below steps

![image](https://user-images.githubusercontent.com/79994584/110301760-7974bd00-801e-11eb-9576-4731689bf70d.png)

![image](https://user-images.githubusercontent.com/79994584/110301658-577b3a80-801e-11eb-9505-d95f61979559.png)

This will select the whole layout Now in tkcon window, type below command

`box`

![image](https://user-images.githubusercontent.com/79994584/110301807-8a253300-801e-11eb-96de-09de62e06728.png)

What is the area of your chip in microns?


# Day 3

**Design & Characterization of a library cell using Magic tool & Ngspice**
--------------------------------------------------------------------------

**1. Spice Deck**

It comprises of the connectivity information of components i.e. Netlist. 

**2. Component values**

The width and length of PMOS and NMOS are defined.

M1: PMOS -> W/L -> 0.375u / 0.25u
M2: NMOS -> W/L -> 0.375u / 0.25u

***Generally the gate Voltage is similar to channel length i.e. if we have channel length L= 0.25u , then the gate voltage = 2.5 V***

**3. Identify 'nodes'** 

A node is required to specify the spice netlist. 

**4. Name nodes**

Every node is represented as a positive number starting from 0 to n. In an increasing order. Nodes can either be represented as gnd, out, in etc.



*** MODEL DESCRIPTION ***

*** NETLIST DESCRIPTION ***

`M1 out in Vdd Vdd pmos W=0.375u L=0.25u`

In the above spice statement a transistor M1 which is a pmos is specified with the order : drain , gate , source, substrate .

`M2 out in 0 0 nmos W=0.375u L=0.25u`

In the above spice statement a transistor M2 which is a nmos is specified with the order : drain , gate , source, substrate .

`cload out 0 10f`

In the above spice statement a load capacitor connected between the out and 0 node having a value of 10fF is specified.

`Vdd vdd 0 2.5`

In the above spice statement a the power supply Vdd is connected between the vdd and 0 nodes and has value 2.5V 

`Vin in 0 2.5`

**Spice Simulation Lab for CMOS Inverter**

*** SIMULATION COMMANDS ***

`.op`

`.dc Vin 0 2.5 0.05`

The above Spice command is to sweep the input voltage 'Vin' from 0 to 2.5V at steps of 0.05 and get the ouput voltage.


There are two cases for pmos and nmos in which there is SPICE Waveform variation :

1. When, Wn = Wp = 0.375u and Ln,p = 0.25u - The (W/L)n = (W/L)p = 1.5 : The VTC Curve is shifted towards the left and the **switching threshold Vm = 0.98 V**
2. When, Wn = 0.375u, Wp= 0.9375 ( observe that Wp = 2.5 * Wn ) : The VTC Curve is exactly at the middle , and the  **switching threshold Vm = 1.2 V**

Hence we observe a difference in transfer characteristics.


**Switching Threshold**

It defines the robustness of CMOS. It is represented as Vm and it lies at the point where Vin = Vout.


**Layout**

Art of layout using Euler's path + Stick diagram

***Layout using stick diagram only***

In this case the conjestion of many metal layers causes alot of DRC rules to come up. However the output remains the same as that in euler's path. 

The improved stick diagram is the combination of Euler's path + Stick diagram.  Stick diagram acts as an interface between final layout and circuit.

After drawing the stick diagram , a rough layout and the dimensions to the metal lines and diffusion layers is specified in accordance with the DRC rules.

***Remember n diffusion contact and p diffusion contact are different.***


**Cell Characterization**

1. Derive actual dimensions for the function
2. Script to create layout in Magic
3. Final layout and input output labelling 
4. Pre-layout and post-layout simulation

***# Day 3 Hands On***

-> Type below commands in terminal

`cd`

`git clone https://github.com/kunalg123/ngspice_labs.git`

`cd ngspice_labs`

`cat inv.spice`

![image](https://user-images.githubusercontent.com/79994584/110316383-a9c55700-8030-11eb-9c6c-7f0031538b92.png)


What is the width of PMOS transistor?

-> Type below commands

`cd`

`cd ngspice_labs`

`cat inv.spice`

![image](https://user-images.githubusercontent.com/79994584/110316538-e1cc9a00-8030-11eb-993f-da23ecc4052a.png)


What is the width of NMOS transistor?

-> Type below commands in terminal

`cd`

`cd ngspice_labs`

`cat inv.spice`

What is Wp/Wn ratio?

-> Type below commands in terminal 

`cd`

`cd ngspice_labs`

`ngspice inv.spice`

There will be terminal like below

`ngspice 1 ->`

On the above ngspice terminal, type below commands

`run`

`setplot dc1`

`plot out in`

![image](https://user-images.githubusercontent.com/79994584/110316957-7800c000-8031-11eb-9a8f-abc6098b241e.png)


This will open a plot with CMOS VTC and Blue 45 degree line

![image](https://user-images.githubusercontent.com/79994584/110316985-851daf00-8031-11eb-8430-efba1a8bf7f3.png)


Click on the intersection of Blue line and CMOS VTC.- Called the Switching Threshold

Go to terminal

What does "x0" value lies between?

![image](https://user-images.githubusercontent.com/79994584/110317062-9b2b6f80-8031-11eb-8b8b-e58fb5552e78.png)


-> Type below command in terminal

`leafpad inv.spice`

![image](https://user-images.githubusercontent.com/79994584/110317157-bc8c5b80-8031-11eb-98b2-aa5302e0fbb4.png)


![image](https://user-images.githubusercontent.com/79994584/110317181-c4e49680-8031-11eb-89f2-a3ccdf51499c.png)

Edit the width of PMOS to 0.75u

Press Ctrl+s to save the file and exit the file

![image](https://user-images.githubusercontent.com/79994584/110317228-dc238400-8031-11eb-8e38-6ab1cb5ce4f2.png)


![image](https://user-images.githubusercontent.com/79994584/110317244-e2b1fb80-8031-11eb-8401-f30da2f38f99.png)


![image](https://user-images.githubusercontent.com/79994584/110317273-ec3b6380-8031-11eb-939a-1037f2510f78.png)


![image](https://user-images.githubusercontent.com/79994584/110317298-f52c3500-8031-11eb-8ca3-ea212745c1af.png)

Where does the switching threshold lies between?


-> In the terminal Open file called "inv_tran.spice" using below command

`leafpad inv_tran.spice`

![image](https://user-images.githubusercontent.com/79994584/110317462-302e6880-8032-11eb-93ac-6f34ab30f20b.png)


![image](https://user-images.githubusercontent.com/79994584/110317487-36bce000-8032-11eb-83c2-93dc2e381b87.png)


Change PMOS width to 0.75u, Save and Close

![image](https://user-images.githubusercontent.com/79994584/110317620-68ce4200-8032-11eb-868d-79849f3a42a8.png)


Type below commands for transient simulations

`ngspice inv_tran.spice`

`ngspice 1 -> run`

`ngspice 1 -> setplot tran1`

`ngspice 1 -> plot out in`


![image](https://user-images.githubusercontent.com/79994584/110317649-72f04080-8032-11eb-9b2b-a2a9ea3d57b2.png)


![image](https://user-images.githubusercontent.com/79994584/110317666-78e62180-8032-11eb-84a0-dd672ad226a4.png)


What is the rise delay? 


![image](https://user-images.githubusercontent.com/79994584/110317800-a03cee80-8032-11eb-8b80-1356fce4ff00.png)


![image](https://user-images.githubusercontent.com/79994584/110317869-bcd92680-8032-11eb-9771-8364576f419c.png)


-> On terminal type below commands

`cd`

`cd ngspice_labs`

`ngspice fn_prelayout.spice`

`ngspice 1 -> run`

`ngspice 1 -> setplot tran1`

`ngspice 1 -> plot out 1.25`

![image](https://user-images.githubusercontent.com/79994584/110318033-ff9afe80-8032-11eb-8ddf-9cc3d7db9822.png)


![image](https://user-images.githubusercontent.com/79994584/110318077-0b86c080-8033-11eb-97a8-2ebb800037b3.png)

What is the value of X0 at the intersection of horizontal blue line and middle rising waveform?


![image](https://user-images.githubusercontent.com/79994584/110318090-10e40b00-8033-11eb-86be-e70308b40705.png)


![image](https://user-images.githubusercontent.com/79994584/110318110-16d9ec00-8033-11eb-8186-b5e62f2f9ce9.png)


-> Repeat the above steps and find what is the value of X0 at intersection of horizontal blue line and middle falling waveform ?

![image](https://user-images.githubusercontent.com/79994584/110318299-530d4c80-8033-11eb-9d2a-8b41f40264cc.png)


-> Pulsewidth is defined by the X0 value obtained in above two lab steps, What is the pulsewidth ?

   **2.25234   -   1.57944 = 0.6729 ~ Around 650ps**
   
-> Open terminal, type below commands

`cd`

`cd ngspice_labs`

`magic –T min2.tech`

![image](https://user-images.githubusercontent.com/79994584/110318701-d4fd7580-8033-11eb-989f-9fc8bb1fad3b.png)


This will open magic layout window and tkcon window

Go to tkcon window and type below command

`source draw_fn.tcl`

![image](https://user-images.githubusercontent.com/79994584/110318835-05451400-8034-11eb-812f-ec38c573486a.png)


In layout window, how many nsubstratecontact and how many polysilicon strips you observe?

![image](https://user-images.githubusercontent.com/79994584/110318867-0fffa900-8034-11eb-8757-acba1092b41d.png)


**8 nsubstratecontact and 6 polysilicon strips**


-> Open terminal, type below command

`cd`

`cd ngspice_labs`

`magic –T  min2.tech fn_postlayout.mag &`

![image](https://user-images.githubusercontent.com/79994584/110319134-74bb0380-8034-11eb-8d07-640fe81e1a9c.png)


![image](https://user-images.githubusercontent.com/79994584/110319151-7a184e00-8034-11eb-9937-cc6ea52753d6.png)


![image](https://user-images.githubusercontent.com/79994584/110319172-83091f80-8034-11eb-9d07-8c92b281b1dd.png)


![image](https://user-images.githubusercontent.com/79994584/110319196-8ac8c400-8034-11eb-935c-25c60c18b81a.png)

What is the area of this design?

![image](https://user-images.githubusercontent.com/79994584/110319215-92886880-8034-11eb-970a-187f83f89062.png)


# Day 4

**Pre-Layout timing analysis and importance of good clock tree**
----------------------------------------------------------------

**1. Delay Tables**

A Delay Table is used for representing delay of a particular block while varying the output load and input slew. Every clock with different sizes has a different Delay table and delay tables varies from block to block.

**2. Setup Timing Analysis**

It is the finite time required *before the clock edge* wherein the data stability is maintained. 

**3. Hold Timing Analysis**

It is the finite time required *after the clock edge* wherein data stability is maintained.

**4. Clock Jitter**

It is the temporary variation in clock period, it is modelled by using a single pararmeter **Uncertainity** .


***# Day 4 Hands On***

-> Open terminal and Type below commands

`cd`

`git clone https://github.com/kunalg123/ngspice_labs`

`cd ngspice_labs`

`cat inv_tran.spice`

What is the input rise slew and fall slew ?

![image](https://user-images.githubusercontent.com/79994584/110329219-51975080-8042-11eb-860e-fabf70a0a75b.png)


-> Open terminal and Type below commands

`cd`

`cd ngspice_labs`

`cat inv_tran.spice`

`ngspice inv_tran.spice`

![image](https://user-images.githubusercontent.com/79994584/110329918-35e07a00-8043-11eb-8b34-7b4e06392a9e.png)

What is the output load and rise delay ?

-> Modify to output load to 20fF in inv_tran.spice Run ngspice 

What is the rise delay that you see now?

![image](https://user-images.githubusercontent.com/79994584/110330881-59f08b00-8044-11eb-8c87-dd2bc88509c7.png)


![image](https://user-images.githubusercontent.com/79994584/110330904-62e15c80-8044-11eb-9e3d-87841bcb844b.png)


![image](https://user-images.githubusercontent.com/79994584/110330928-6b399780-8044-11eb-9299-a07b65aef3c6.png)


![image](https://user-images.githubusercontent.com/79994584/110330953-742a6900-8044-11eb-9db1-a4661ee90bfe.png)


Rise time delay = rise time of output (II)  - Fall time of input (I) = 1.23364 – 1.01869 = 0.21495ns

-> Open below file using "leafpad" or "less" or "vim" 

`/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib`

![image](https://user-images.githubusercontent.com/79994584/110331616-5ad5ec80-8045-11eb-96e6-b58e0b6c1cc5.png)

Look between line numbers 21 to 24 What is the value of "slew_upper_threshold_pct_fall" ?

![image](https://user-images.githubusercontent.com/79994584/110331686-6fb28000-8045-11eb-9a84-06787aa0b856.png)

-> Open below file using "leafpad" or "less" or "vim"

`/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib`

Look for lines between 25 to 28

What is the value of output_threshold_pct_rise ?


![image](https://user-images.githubusercontent.com/79994584/110331871-a7212c80-8045-11eb-9088-bd16fba0e06b.png)


-> Open below file using "leafpad" or "less" or "vim"

`/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib`

Look for line number 43

What are the 2 variables of "delay_template_5x5"?

![image](https://user-images.githubusercontent.com/79994584/110332325-33335400-8046-11eb-8518-be925878479f.png)

-> Open below file using "leafpad" or "less" or "vim"

`/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib`

Look for line number 2943

The delay table below line number 2943 is for which cell ?

![image](https://user-images.githubusercontent.com/79994584/110332443-56f69a00-8046-11eb-8479-6dfe02a73661.png)

-> Which delay template is used for INVX1?

Look for line number 2983

![image](https://user-images.githubusercontent.com/79994584/110333037-1f3c2200-8047-11eb-83be-002128db6a4b.png)


# Day 5

**Final steps for RTL2GDS**
--------------------------

**1. Maze Routing - Lee's Algorithm**

It is a very popular algorithm in physical design - Routing stage. It starts by creating a routing grid. So, according to this algorithm we have a Source "S" and a target "T" and we need to find a path from S to T which is shortest and has the least number of bends. So starting from the cell wherein we have our S , the adjacent cells ( except the diagonal one's) are numbered in an increasing order to reach the T cell.

![image](https://user-images.githubusercontent.com/79994584/110338870-85c43e80-804d-11eb-93d4-70c862e9a6bf.png)


**2. DRC - Design Rule Checks**

It comprises of various design constraints that have to be adhered to inorder to avoid DRC failure. 

* Wire Width - Width of the Wire
* Wire pitch - Spacing between the centres of two wires
* Wire Spacing - Spacing between two wires
* Via Width
* Via Spacing

An example of a DRC violation is *Signal Short* and to the easiest and the cheapest way to prevent this from occuring is to use change metal layers.


***# Day 5 Hands On***

![image](https://user-images.githubusercontent.com/79994584/110333308-7641f700-8047-11eb-873c-544ffc5e0ef6.png)


![image](https://user-images.githubusercontent.com/79994584/110333373-8954c700-8047-11eb-908f-8d3f8d347661.png)


![image](https://user-images.githubusercontent.com/79994584/110333406-8fe33e80-8047-11eb-81ca-e6707c333ff2.png)


![image](https://user-images.githubusercontent.com/79994584/110333446-97a2e300-8047-11eb-8f8f-e8796f7b321a.png)


What is the pre-layout frequency?

Hint - Search for case-sensitive keyword "MHz"

-> If you have completed above step, then open the below file

`log/post_sta.log`

What is post-layout frequency?

![image](https://user-images.githubusercontent.com/79994584/110333606-c7ea8180-8047-11eb-80d5-70f1c2e790c3.png)


What is the post-layout to pre-layout drop in frequency ?

**314-294= 20Mhz** 

*The drop in frequency from post-layout to pre-layout is due to **parasitics**.*


--------------------------------------------------------------------------------------------------------------------------------------------------

# Acknowledgement

**Kunal Ghosh** , *Co-founder (VSD Corp. Pvt. Ltd).*











































