# VSD-physical-design
## Physical Design using Open-Source EDA Tools
### A 5 day course on physical designing using open source tools.
### CONTENTS:
1. **DAY 1 Study and review various components of RISC-V based picoSoC**
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
2. **DAY 2 Chip planning strategies and introduction to foundry library cells**
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

3. **DAY 3 Design and characterize one library cell using Magic Layout tool and ngspice**
  * SKILL 1
  * SKILL 2
  * SKILL 3
  * SKILL 4

4. **DAY 4  Pre-layout timing analysis and importance of good clock tree**
  * SKILL 1
  * SKILL 2
  * SKILL 3
  * SKILL 4

5. **DAY 5 Final steps for RTL2GDS**
  * SKILL 1
  * SKILL 2
  * SKILL 3
  * SKILL 4
### TOOLS USED
#### The open source tools that are involved in this workshop are as follows

1. Yosys – for Synthesis, 
2. Graywolf – for Placement, 
3. Qrouter – for Routing, 
4. Netgen – for LVS, 
5. Magic – for Layout and Floorplanning, 
6. Qflow – RTL2GDS integration, 
7. OpenSTA & Opentimer -Pre-layout and Post-layout Static timing analysis

### LABS
### DAY1
### D1SK4 - MCQ3

1.Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal. 2.Now type the command "yosys". What do you see next?
![image](https://user-images.githubusercontent.com/80052871/110253187-e94b5f00-7fae-11eb-929d-bb1fb697bba0.png)

### D1SK4 - MCQ4

which sta
![image](https://user-images.githubusercontent.com/80052871/110253094-7fcb5080-7fae-11eb-9ed3-1b75f330c92e.png)

### D1SK4 - MCQ5

git clone https://github.com/kunalg123/vsdflow.git
![image](https://user-images.githubusercontent.com/80052871/110253199-fe27f280-7fae-11eb-851c-ec6b04cb2187.png)


### D1SK4 - MCQ6
*cd vsdflow
./vsdflow spi_slave_design_details.csv
ls -ltr outdir_spi_slave/*
![image](https://user-images.githubusercontent.com/80052871/110253315-accc3300-7faf-11eb-8c72-c6149d4766ab.png)



### D1SK4 - MCQ7

*cd outdir_spi_slave
qflow display spi_slave*
It will open 2 windows "layout1" and "tkcon"
![image](https://user-images.githubusercontent.com/80052871/110253341-d2593c80-7faf-11eb-9630-c390d2d4b2d2.png)

![image](https://user-images.githubusercontent.com/80052871/110253547-f406f380-7fb0-11eb-8622-13647c3d112d.png)




### D1SK4 - MCQ8
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


### D2SK4 - MCQ5
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



### D3SK1 - MCQ5,6,7
*cd
git clone https://github.com/kunalg123/ngspice_labs.git
cd ngspice_labs
cat inv.spice*
![image](https://user-images.githubusercontent.com/80052871/110253698-c53d4d00-7fb1-11eb-8721-5c2f23537d20.png)


### D3SK1 - MCQ8

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



### D3SK1 - MCQ10
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

### D3SK2 - MCQ1
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

### D3SK3 - MCQ3

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


### D3SK3 - MCQ4
Go to labs, open terminal

Type below command

*cd
cd ngspice_labs
magic -T min2.tech fn_postlayout.mag &*

![image](https://user-images.githubusercontent.com/80052871/110254238-5e6d6300-7fb4-11eb-9e84-37d86df7fe68.png)


### D4SK1 - MCQ6

*cd
git clone https://github.com/kunalg123/ngspice_labs
cd ngspice_labs
cat inv_tran.spice*
![image](https://user-images.githubusercontent.com/80052871/110254534-9cb75200-7fb5-11eb-80a3-167808b73d25.png)
 input rise slew and fall slew = 10ps, 10ps respectively

### D4SK1 - MCQ7
Go to Day 4 (When you start Day 4 labs, system will enable Day 2 labs for you. Click on Desktop icon)

Open terminal and Type below commands

*cd
cd ngspice_labs
cat inv_tran.spice
ngspice inv_tran.spice*
![image](https://user-images.githubusercontent.com/80052871/110254396-fb300080-7fb4-11eb-9625-fa418abd2f25.png)

![image](https://user-images.githubusercontent.com/80052871/110254432-2286cd80-7fb5-11eb-8fd2-1e74b7d0ba78.png)

![image](https://user-images.githubusercontent.com/80052871/110254422-16027500-7fb5-11eb-885f-9a18ebe66b86.png)


### D4SK2 - MCQ6

Go to labs Open below file using "leafpad" or "less" or "vim" - whichever you are comfortable with)

/usr/local/share/qflow/tech/osu018/osu018_stdcells.lib

![image](https://user-images.githubusercontent.com/80052871/110254465-3fbb9c00-7fb5-11eb-9a7b-6dc505d60735.png)
Changing the load to 20f.



### D4SK2 - MCQ11
Go to labs

Type below command

*cd
cd vsdflow/my_picorv32
leafpad picorv32.sdc*
Type below lines in the file picorv32.sdc file which you have just opened above

create_clock -name clk -period 2.5 -waveform {0 1.25} [get_ports clk]
Save and close the above file

Now type below command

leafpad prelayout_sta.conf
Type below lines in prelayout_sta.conf file which you have just opened above

*read_liberty /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
read_verilog synthesis/picorv32.rtlnopwr.v
link_design picorv32
read_sdc picorv32.sdc
report_checks*


Now type below command

sta prelayout_sta.conf


### D4SK4 - MCQ2
Perform all steps in D4SK2 - MCQ11

You are now at below "sta" terminal

%
Type below command in above terminal

*set_propagated_clock [all_clocks]
report_checks*




### D4SK4 - MCQ5
Perform all steps in D4SK4 - MCQ3

Type below command

report_checks -path_delay min -digits 4




### D5SK2 - MCQ1
Go to Day 5 labs

Open terminal

Type below commands

*cd
cd vsdflow/my_picorv32
qflow route picorv32
qflow sta picorv32
qflow backanno picorv32
leafpad log/sta.log*



### D5SK2 - MCQ2

log/post_sta.log




