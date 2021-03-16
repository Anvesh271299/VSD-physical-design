# VSD-physical-design
## Physical Design using Open-Source EDA Tools
### A 5 day course on physical designing using open source tools.
### CONTENTS:
#### DAY 1 Study and review various components of RISC-V based picoSoC
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
  * SKILL 1
    + Introduction to QFN-48 Package, chip,pads,core,die and IP's
  * SKILL 2
    + Introduction to RISC-V
    + From Software applications to hardware
  * SKILL 3
    + Pre-requisites and RISC-V, picorv32 and picoSoC review
    + Raven SoC 
  * SKILL 4
    + Installation of basic EDA tools
    
#### DAY 2 Chip planning strategies and introduction to foundry library cells
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
  * SKILL 1
    + utilization factor and aspect ration
    + concept of pre-placed cells
    + De-coupling capacitors
    + power planning
    + pin placement
    + pin arrangement
    + floorplanning
  * SKILL 2
    + netlist binding and initial place design
    + estimated wire length and capacitance
    + final placement optimization
    + libraries and characterization
  * SKILL 3
    + inouts for cell design
    + circuit design
    + layout design
    + characterization flow
  * SKILL 4
    + timing threshold
    + propagation delay and transition time

#### DAY 3 Design and characterize one library cell using Magic Layout tool and ngspice
  **1. Spice Deck**

  It comprises of the connectivity information of components i.e. Netlist. 

  **2. Component values**

  The width and length of PMOS and NMOS are defined.

  M1: PMOS -> W/L -> 0.375u / 0.25u
  M2: NMOS -> W/L -> 0.375u / 0.25u

  ***Generally the gate Voltage is similar to channel length i.e. if we have channel length L= 0.25u ,then the gate voltage = 2.5 V***

  **3. Identify 'nodes'** 

  A node is required to specify the spice netlist. 

  **4. Name nodes**

  Every node is represented as a positive number starting from 0 to n. In an increasing order. Nodes  can either be represented as gnd, out, in etc.



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
  * SKILL 1- Labs for CMOS inverter ngspice simulation
    + Spice deck creation for CMOS inverter
    + Spice simulation lab for CMOS INverter
    + Switching threshold Vm
    + Static and Dynamic simulation of CMOS
  * SKILL 2- Art of layout using Euler's path plus stick diagram
    + Pre layout simulation of test circuit
    + Layout using only stick diagram
    + Euler's path for Fn-input gate reordering
    + Improved stick diagram for new input gate reordering
    + Abstract layout from stick diagram
  * SKILL 3- Lab for Magic and post-layout ngspice simulations
    + Derive actual dimension for Fn
    + Script to create layout in magic
    + Final layout and input/output labelling
    + Post layout ngspice simulation
  * SKILL 4- Inception of layout CMOD fabrication process
    + Create active region
    + Formation of n-well and p-well
    + Formation of gate
    + LDD formation
    + Source-drain formation
    + Local interconnect formation
    + Higher level metal formation

#### DAY 4  Pre-layout timing analysis and importance of good clock tree**
  **1. Delay Tables**

  A Delay Table is used for representing delay of a particular block while varying the output load    and input slew. Every clock with different sizes has a different Delay table and delay tables varies from block to block.

  **2. Setup Timing Analysis**

  It is the finite time required *before the clock edge* wherein the data stability is maintained. 

  **3. Hold Timing Analysis**

  It is the finite time required *after the clock edge* wherein data stability is maintained.

  **4. Clock Jitter**

  It is the temporary variation in clock period, it is modelled by using a single pararmeter          **Uncertainity** .

  * SKILL 1- Timing modelling using delay table
    + Introduction to delay table
    + Delay table usage
  * SKILL 2- Timing analysis with ideal clock
    + Setup timing analysis and introduction to flip flop setup time
    + Introduction to clock jitter and uncertainity
  * SKILL 3- Clock tree synthesis and signal integrity
    + Clock tree routing and buffering using H-tree algorithm
    + crosstalk and net shielding
  * SKILL 4- Timing analysis with real clock
    + Setup timing analysing using real clock
    + Hold timing analysis using real clock

**DAY 5 Final steps for RTL2GDS**
  **1. Maze Routing - Lee's Algorithm**

  It is a very popular algorithm in physical design - Routing stage. It starts by creating a routing   grid. So, according to this algorithm we have a Source "S" and a target "T" and we need to find a     path from S to T which is shortest and has the least number of bends. So starting from the cell       wherein we have our S , the adjacent cells ( except the diagonal one's) are numbered in an increasing   order to reach the T cell.


  **2. DRC - Design Rule Checks**

  It comprises of various design constraints that have to be adhered to inorder to avoid DRC failure. 

* Wire Width - Width of the Wire
* Wire pitch - Spacing between the centres of two wires
* Wire Spacing - Spacing between two wires
* Via Width
* Via Spacing

An example of a DRC violation is *Signal Short* and to the easiest and the cheapest way to prevent this from occuring is to use change metal layers.
  * SKILL 1- Routing and design rule check(DRC)
    + Introduction to maze routing
    + Lee's algoritm conclusion
    + Design rule check
    + Introduction to IEEE-1481--1999 SPEF format
    + SPEF representation of NET
    + Distributed resistance and capacitance in SPEF
    + SPEF header descrition
  * SKILL 2- PNR interactive flow tutorial
    + Few tips on PIN placement and floor planning chip
    + Placement and pre-route STA
    + Routing and post route STA
### TOOLS USED
#### The open source tools that are involved in this workshop are as follows

1. Yosys – for Synthesis, 
2. Graywolf – for Placement, 
3. Qrouter – for Routing, 
4. Netgen – for LVS, 
5. Magic – for Layout and Floorplanning, 
6. Qflow – RTL2GDS integration, 
7. OpenSTA & Opentimer -Pre-layout and Post-layout Static timing analysis

## LABS

### DAY1

#### Installation of basic EDA tools

1.Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal. 2.Now type the command "yosys". What do you see next?
![image](https://user-images.githubusercontent.com/80052871/110253187-e94b5f00-7fae-11eb-929d-bb1fb697bba0.png)

#### sta

which sta
![image](https://user-images.githubusercontent.com/80052871/110253094-7fcb5080-7fae-11eb-9ed3-1b75f330c92e.png)

git clone https://github.com/kunalg123/vsdflow.git
![image](https://user-images.githubusercontent.com/80052871/110253199-fe27f280-7fae-11eb-851c-ec6b04cb2187.png)

*cd vsdflow
./vsdflow spi_slave_design_details.csv
ls -ltr outdir_spi_slave/*
![image](https://user-images.githubusercontent.com/80052871/110253315-accc3300-7faf-11eb-8c72-c6149d4766ab.png)

*cd outdir_spi_slave
qflow display spi_slave*
It will open 2 windows "layout1" and "tkcon"
![image](https://user-images.githubusercontent.com/80052871/110253341-d2593c80-7faf-11eb-9630-c390d2d4b2d2.png)

![image](https://user-images.githubusercontent.com/80052871/110253547-f406f380-7fb0-11eb-8622-13647c3d112d.png)

*cd
cd vsdflow
mkdir my_picorv32
cd my_picorv32
mkdir source synthesis layout
cp ~/vsdflow/verilog/picorv32.v source/.
qflow gui &*
![image](https://user-images.githubusercontent.com/80052871/110253380-06ccf880-7fb0-11eb-843d-cc9b3dec4f49.png)

Select below options in gui

Technology = osu018

Verilog source file : picorv32.v

Verilog module : picorv32

![image](https://user-images.githubusercontent.com/80052871/110253395-1e0be600-7fb0-11eb-9731-e4410e088001.png)

![image](https://user-images.githubusercontent.com/80052871/110253397-219f6d00-7fb0-11eb-9268-366e023fe173.png)

![image](https://user-images.githubusercontent.com/80052871/110253401-26642100-7fb0-11eb-8427-e96505a6157c.png)

![image](https://user-images.githubusercontent.com/80052871/110253412-31b74c80-7fb0-11eb-8088-9359189e7f21.png)

### DAY 2
#### Chip planning strategies and introduction to foundry library cells
![image](https://user-images.githubusercontent.com/80052871/110253632-55c75d80-7fb1-11eb-9664-5c160e72ccca.png)
![image](https://user-images.githubusercontent.com/80052871/110253635-595ae480-7fb1-11eb-942d-6fea51a386cc.png)
![image](https://user-images.githubusercontent.com/80052871/110253636-5bbd3e80-7fb1-11eb-8ad7-bd9cf63de461.png)

*cd
cd vsdflow/my_picorv32
qflow display picorv32 &*
This will open layout and tkcon window In the layout window, select whole chip using below steps
![image](https://user-images.githubusercontent.com/80052871/110253583-26b0ec00-7fb1-11eb-8061-259c41741687.png)

Take cursor to bottom left
Left mouse click
Take cursor to top right
Right mouse click
Press Shift+i
This will select the whole layout Now in tkcon window, type below command

box
![image](https://user-images.githubusercontent.com/80052871/110253596-36c8cb80-7fb1-11eb-946f-2964661d925a.png)


### DAY 3
####  Labs for CMOS inverter ngspice simulation
*cd
git clone https://github.com/kunalg123/ngspice_labs.git
cd ngspice_labs
cat inv.spice*
![image](https://user-images.githubusercontent.com/80052871/110253698-c53d4d00-7fb1-11eb-8721-5c2f23537d20.png)

*cd
cd ngspice_labs
ngspice inv.spice*
There will be terminal like below
![image](https://user-images.githubusercontent.com/80052871/110253779-2402c680-7fb2-11eb-91aa-862412ed0eb5.png)
ngspice 1 ->
On the above ngspice terminal, type below commands

*run
setplot dc1
plot out in*
![image](https://user-images.githubusercontent.com/80052871/110253791-2e24c500-7fb2-11eb-950e-0c9dc167b312.png)

![image](https://user-images.githubusercontent.com/80052871/110253800-35e46980-7fb2-11eb-9b76-e512c2ef800e.png)
"x0" value lies between 1.0v-1.1v


Go to labs, open terminal

Type below command

leafpad inv.spice

![image](https://user-images.githubusercontent.com/80052871/110253847-6fb57000-7fb2-11eb-9631-c64cd0f7da3e.png)

![image](https://user-images.githubusercontent.com/80052871/110253937-d63a8e00-7fb2-11eb-92e4-f23993310296.png)

leafpad in_tran.spice
![image](https://user-images.githubusercontent.com/80052871/110253960-ece0e500-7fb2-11eb-94f6-cb7e2fbbae87.png)

ngspice inv_tran.spice
ngspice 1 -> run
ngspice 1 -> setplot tran1
ngspice 1 -> plot out in
![image](https://user-images.githubusercontent.com/80052871/110253978-01bd7880-7fb3-11eb-9a85-750021c087aa.png)
Rise delay= 76ps

#### Art of layout using Euler's path plus stick diagram
Go to labs, type below commands

*cd
cd ngspice_labs
ngspice fn_prelayout.spice
ngspice 1 -> run
ngspice 1 -> setplot tran1
ngspice 1 -> plot out 1.25*

![image](https://user-images.githubusercontent.com/80052871/110254047-6ed10e00-7fb3-11eb-8b0a-7b66663ae18d.png)
Value of X0 at the intersection of horizontal blue line and middle rising waveform = Around 1.6e-09

![image](https://user-images.githubusercontent.com/80052871/110254082-9a53f880-7fb3-11eb-83ab-5ea7fca05601.png)
Value of X0 at the intersection of horizontal blue line and middle falling waveform = Around 2.2e-09

#### Lab for Magic and post-layout ngspice simulations

Go to labs, open terminal

Type below commands

*cd
cd ngspice_labs
magic -T min2.tech*
This will open magic layout window and tkcon window
![image](https://user-images.githubusercontent.com/80052871/110254178-11898c80-7fb4-11eb-9877-deb68bcf5fa8.png)
8 nsubstratecontact and 6 polysilicon strips

Go to tkcon window and type below command

source draw_fn.tcl
![image](https://user-images.githubusercontent.com/80052871/110254163-f9b20880-7fb3-11eb-8f08-1067ec64e3f8.png)

![image](https://user-images.githubusercontent.com/80052871/110254205-2fef8800-7fb4-11eb-8308-f6e7f4689849.png)
area of the above design = 4489 unit^2

Go to labs, open terminal

Type below command

*cd
cd ngspice_labs
magic -T min2.tech fn_postlayout.mag &*

![image](https://user-images.githubusercontent.com/80052871/110254238-5e6d6300-7fb4-11eb-9e84-37d86df7fe68.png)

### DAY 4
####  Timing modelling using delay table

*cd
git clone https://github.com/kunalg123/ngspice_labs
cd ngspice_labs
cat inv_tran.spice*
![image](https://user-images.githubusercontent.com/80052871/110254534-9cb75200-7fb5-11eb-80a3-167808b73d25.png)
 input rise slew and fall slew = 10ps, 10ps respectively

Go to Day 4 (When you start Day 4 labs, system will enable Day 2 labs for you. Click on Desktop icon)

Open terminal and Type below commands

*cd
cd ngspice_labs
cat inv_tran.spice
ngspice inv_tran.spice*
![image](https://user-images.githubusercontent.com/80052871/110254396-fb300080-7fb4-11eb-9625-fa418abd2f25.png)

![image](https://user-images.githubusercontent.com/80052871/110254432-2286cd80-7fb5-11eb-8fd2-1e74b7d0ba78.png)
load is 10fF and rise delay is ~126ps

![image](https://user-images.githubusercontent.com/80052871/110254422-16027500-7fb5-11eb-885f-9a18ebe66b86.png)

![image](https://user-images.githubusercontent.com/80052871/110254465-3fbb9c00-7fb5-11eb-9a7b-6dc505d60735.png)
Changing the load to 20f.
![image](https://user-images.githubusercontent.com/80052871/110254735-5d3d3580-7fb6-11eb-9bd1-f81ae14a9eab.png)
![image](https://user-images.githubusercontent.com/80052871/110254741-66c69d80-7fb6-11eb-8c5d-abcf6f64568e.png)


#### Timing analysis with ideal clock

Go to labs Open below file using "leafpad" or "less" or "vim" - whichever you are comfortable with)

/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib

![image](https://user-images.githubusercontent.com/80052871/110254798-ad1bfc80-7fb6-11eb-88f2-bfa05d32ccb8.png)
slew upper threshold pct fall = 80 
![image](https://user-images.githubusercontent.com/80052871/110254838-e0f72200-7fb6-11eb-853e-13c7568578ad.png)
o/p threshold pct rise = 50%
![image](https://user-images.githubusercontent.com/80052871/110254870-0a17b280-7fb7-11eb-9e6b-e18d6deb9634.png)
variable 1 and variable 2
![image](https://user-images.githubusercontent.com/80052871/110254892-2a477180-7fb7-11eb-9c54-43fc91e9cfe0.png)
INVX1
![image](https://user-images.githubusercontent.com/80052871/110254901-33d0d980-7fb7-11eb-81ea-0954c4849b01.png)
Delay template 5x5


Go to labs

Type below command

*cd
cd vsdflow/my_picorv32
leafpad picorv32.sdc*
Type below lines in the file picorv32.sdc file which you have just opened above

create_clock -name clk -period 2.5 -waveform {0 1.25} [get_ports clk]
![image](https://user-images.githubusercontent.com/80052871/110254928-4ea34e00-7fb7-11eb-90d2-4c0797821c35.png)

Save and close the above file

Now type below command

leafpad prelayout_sta.conf
Type below lines in prelayout_sta.conf file which you have just opened above

*read_liberty /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
read_verilog synthesis/picorv32.rtlnopwr.v
link_design picorv32
read_sdc picorv32.sdc
report_checks*
![image](https://user-images.githubusercontent.com/80052871/110254940-59f67980-7fb7-11eb-8a03-c9da867c87ec.png)


Now type below command

sta prelayout_sta.conf
![image](https://user-images.githubusercontent.com/80052871/110254954-68449580-7fb7-11eb-8304-423980aeda15.png)
SLACK value =-0.56
![image](https://user-images.githubusercontent.com/80052871/110254959-6d094980-7fb7-11eb-8f41-f1742248047f.png)
data arrival time =2.9ns
![image](https://user-images.githubusercontent.com/80052871/110254960-709cd080-7fb7-11eb-8dbd-32e0eff94137.png)
data required time =2.3389ns


#### Timing analysis with real clock
Perform all steps in D4SK2 - MCQ11

You are now at below "sta" terminal

%
Type below command in above terminal

*set_propagated_clock [all_clocks]
report_checks*

![image](https://user-images.githubusercontent.com/80052871/110255131-4ac3fb80-7fb8-11eb-9608-c3433047b4ef.png)
SLACK value after clock propagation = around -0.68ns

![image](https://user-images.githubusercontent.com/80052871/110255286-ece3e380-7fb8-11eb-980c-967127118044.png)
launch clock network delay

![image](https://user-images.githubusercontent.com/80052871/110255319-10a72980-7fb9-11eb-84e7-b81a7b908a61.png)
capture clock network delay=0.56

Perform all steps in D4SK4 - MCQ3

Type below command

report_checks -path_delay min -digits 4

![image](https://user-images.githubusercontent.com/80052871/110255353-37656000-7fb9-11eb-8bfd-1f6ec16d0d8c.png)
![image](https://user-images.githubusercontent.com/80052871/110255356-3cc2aa80-7fb9-11eb-9f91-29f23c1be189.png)

library hold time and hold slack = -9.4ps and 222.5ps respectively


### DAY 5
#### PNR interactive flow tutorial
![image](https://user-images.githubusercontent.com/80052871/110255563-66c89c80-7fba-11eb-8367-678203f6a07e.png)

Go to Day 5 labs

Open terminal

Type below commands

*cd
cd vsdflow/my_picorv32
qflow route picorv32
qflow sta picorv32
qflow backanno picorv32
leafpad log/sta.log*

![image](https://user-images.githubusercontent.com/80052871/110255456-d427fd80-7fb9-11eb-8b61-6940477e68f2.png)
pre-layout frequency = 314 MHz

log/post_sta.log
![image](https://user-images.githubusercontent.com/80052871/110255490-12bdb800-7fba-11eb-8118-103a00d66d70.png)
post-layout frequency = 297 MHz

## Acknowledgement

Kunal Ghosh -CO Founder VSD(VSD Corp.pvt.ltd)


