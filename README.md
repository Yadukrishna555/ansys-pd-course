# Physical Design Training

## *Overview*
![image](https://github.com/user-attachments/assets/dfbef3dc-cc12-43ea-96b2-f972bc6c5ab3)

### Reference links 

Git hub link : [https://github.com/hari-govind-p-k-2k/ansys-pd-course/blob/main/url](url)

Youtube video : [https://github.com/hari-govind-p-k-2k/ansys-pd-course/blob/main/url](url)

## OPENLANE

![image](https://github.com/user-attachments/assets/410708ec-491c-4734-96eb-cab0363d21f7)

![image](https://github.com/user-attachments/assets/e968a17c-2c31-4cfc-821e-53e77af12f96)

**Openlane ->**

OpenLane is an open-source, automated RTL-to-GDSII flow for digital chip design. It is designed to support end-to-end chip development using open-source tools, primarily leveraging the SkyWater 130nm process node. 
OpenLane integrates various tools like Yosys (for synthesis), OpenROAD (for placement and routing), Magic (for layout verification), and others, providing a complete flow for hardware designers to tape out chips with minimal manual intervention. 
Skywater PDK : This PDK is an open-source package that provides the necessary data, models, and tools to design and manufacture chips using their 130nm process. It was released in collaboration with Google to promote innovation in the chip design ecosystem by allowing designers to prototype, verify, and manufacture their designs in an open and accessible manner.

***Openlane Flow***

![image](https://github.com/user-attachments/assets/7a5c4401-8680-4c6e-9eb2-8ac6a6134482)

We will be uswe Openlane to do the RTL2GDS flow for a design called picorv32a . 

To continue working on a particular run folder, <desired_tage> is the folder name:

prep -design <design_name> -tag <desired_tag>
Workshop Github material https://github.com/google/skywater-pdk https://github.com/nickson-jose/vsdstdcelldesign ttps://sourceforge.net/projects/ngspice/ https://github.com/ https://www.vlsisystemdesign.com/wp-content/uploads/2017/07/Introduction-to-Industrial-Physical-Design-Flow.pdf

## Day 1 ##

Openlane directory structure

![image](https://github.com/user-attachments/assets/8f7a0f48-5c1a-48a9-8bb7-8dfde34e0e53)


PDK dir - Having all the information such as lib, tech, lef verilog files etc for various open technologies including sky130A 
Wentr through the flow.tcl, tech.lef and other files.
![image](https://github.com/user-attachments/assets/f781a17e-b9e8-461f-b77a-8454d8a0ff67)

![image](https://github.com/user-attachments/assets/ea4fe63a-768a-455c-ab1d-4c7d8f2fd657)

![image](https://github.com/user-attachments/assets/460962a4-1633-45fc-8f22-3bf55ac8ebcc)

![image](https://github.com/user-attachments/assets/2e24fea1-633d-4267-bb3d-467f649e1f7d)



![image](https://github.com/user-attachments/assets/5b613966-4279-4824-9841-92fd778dfde0)

***Invoking openlane***

![image](https://github.com/user-attachments/assets/36def94b-eafd-48fe-a239-e73434af7c68)

.flow.tcl can run full process step by step 

***import all the packages needed to run the flow***

![image](https://github.com/user-attachments/assets/c43a6d57-07b0-49ed-bb9d-6f09fb834261)

Reviewing design related files of picorv32a 

![image](https://github.com/user-attachments/assets/9530284b-e706-46cf-a691-4178543a8eba)

Reviewing config.tcl

![image](https://github.com/user-attachments/assets/3f61b924-bb28-4331-9c6c-ab4e764face3)

Priority wise : Default setting from openlane < config.tcl < sky130A_sky130_fd_sc_hd_config.tcl

<u>**Design preparation step**</u>

prep -design picorv32a

![image](https://github.com/user-attachments/assets/aecb44c5-38b3-43cd-af5a-46f30ba676b1)

***Running synthesis***

![image](https://github.com/user-attachments/assets/390cc50a-4879-4f98-a3a6-84515e73fdbf)


**Chip Area**
![image](https://github.com/user-attachments/assets/a7432186-24e5-4787-9825-3047aa7f32be)

Chip area after synthesis = 147712.918400

### Calculating Flop Ratio ###

![image](https://github.com/user-attachments/assets/7101946e-35c0-4a8f-b3f9-976174027794)

#### Flop Ratio = Number of D flip flops/total no of cells = 1613/14876 = 0.01908 = 10.8429% ####


## DAY 2 floor Planning & Placement ##

***Core & Die***
![image](https://github.com/user-attachments/assets/a521784c-a343-4ce3-b673-108b2aa8ddde)

![image](https://github.com/user-attachments/assets/e9e77780-abcb-43bc-be84-413f95e6c557)

![image](https://github.com/user-attachments/assets/d78d3b26-08d3-40b1-83da-dd90c38f3675)

### Utilization factor ###

![image](https://github.com/user-attachments/assets/dab3dd61-4f14-470e-ac12-feb98d2ad64d)

The utilization ratio is typically set between 0.5 and 0.6 for optimizations, decoupling capacitors (decaps), and routing. These parameters can be controlled using specific keywords.

***Aspect ratio = core height/core width***


### Preplaced cells ###

![image](https://github.com/user-attachments/assets/73c31111-60c7-406e-b8a9-eccc52348cad)

Floorplanning is done before placement to position pre-placed cells or blocks. This process fixes their positions and creates blockages for the placer in that area. Blocks are formed by partitioning the logic and assigning pins, then handed off to block owners for implementation, with guidance on area and dimensions. Blocks usually consist of cells that are repeated multiple times across the design or contain complex logic.

Placing these blocks is an optimization problem that considers factors such as proximity to ports and the order in which the blocks operate. Flylines help determine block placement during this phase.

### Need of Decaps ###

![image](https://github.com/user-attachments/assets/de201ff4-07cb-429a-bcd5-7ab98ee9119e)

For any signal to be considered as logic '0' and logic '1', it should be in the Noise Margin. 

Decoupling capacitors (decaps) act as local charge sources for instances, charging when no switching occurs and providing charge when switching happens. This helps reduce dynamic voltage drops. Decaps are typically placed around the blocks.


![image](https://github.com/user-attachments/assets/db711b5b-45d7-41a3-bcd4-a39579adfe83)

Decaps will ensure all the switching captured and no crosstalk problems.

### Power Planning ###

![image](https://github.com/user-attachments/assets/906fd80a-a5bc-4633-af2d-8859b0a2fb4a)

A single pathway for power delivery results in IR drop, even with decaps, as decaps can only charge up to Vsource - IR. Using a grid structure is crucial because it provides multiple pathways for different instances.

### Pin Placement and logical pin placement blockage


![image](https://github.com/user-attachments/assets/222163ec-dd1a-40c7-8548-ec01e60b5101)

The area between the core and die is blocked off using logical cell placement blockages to prevent the placer from positioning cells there. Pins are placed in this region and can be equidistant or spaced randomly, depending on the block's input needs. Clock pins are larger than signal pins since they handle large fanout and require lower resistance.

The Power Distribution Network (PDN) is generally implemented during floorplanning, but in this case, it will be done after Clock Tree Synthesis (CTS).


## Floorplanning ##

***Reviewing floorplanning.tcl 
![image](https://github.com/user-attachments/assets/ae025a74-2d38-4375-997d-a485e5136422)

**Running Floorplanning**

Command : run_floorplan

![image](https://github.com/user-attachments/assets/64a818ef-7207-4424-ae42-9c3d6cf469f9)

Lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_config.tcl).

**Reviewing floorplan related files**

![image](https://github.com/user-attachments/assets/78753a17-39be-458e-971b-22249b68474d)

![image](https://github.com/user-attachments/assets/827321d7-2e50-4b3c-9638-084e4cf60d0b)

**Floorplan results dir**

![image](https://github.com/user-attachments/assets/33ba36fd-3078-4b4b-928f-43c9626f85bb)


**Reviewing floorplan.def**

Reviewing floorplan output def file 

![image](https://github.com/user-attachments/assets/76fd8c54-8cc4-48d1-9664-b77982c1a077)

Found DIE AREA from DEF file (DB unit 1000 so to get actual die area in micron, divide the reported DIEAREA value by 1000)

**Die Area from DEF file = (660685/1000) * (671405/1000) = 660.685 * 671.405 = 443587.21 sq microns**

### Using Magic to visualize the created def ###
<table> </table>

**Magic Layout Window**

![image](https://github.com/user-attachments/assets/9bdb6dfd-1e36-4347-8584-f6135108aeb0)
 
**tkon window**

![image](https://github.com/user-attachments/assets/775d6afe-98ea-4fdc-97db-fd918d08dd8d)

![image](https://github.com/user-attachments/assets/2f5999fa-70c3-42d8-9000-e524fa3ba99a)

As seen all the instances in lower left. Tap cells diagonally equidistant and all pins random but equidistant as FP_IO_MODE is set to 1.

***Querying attributes of a decap:***

![image](https://github.com/user-attachments/assets/1ec81510-5ef3-4ade-aa91-3d9ab754487e)

### Placement ###

Placement is done post placement of blocks and IO pins.

The idea is to take the library information of the cells to implement the netlist on the design and come up with an optimal placement which could possibly pass timing.

![image](https://github.com/user-attachments/assets/11c7827d-5cb4-434c-82d6-21529aad24ab)

![image](https://github.com/user-attachments/assets/a024b757-b556-40e2-af14-69757d1063b6)

Inserting repeaters to optimize the placement 

![image](https://github.com/user-attachments/assets/3263ed66-bd99-4faa-bbba-e07e2429c17c)

![image](https://github.com/user-attachments/assets/5cd152a2-a184-4428-9689-1ede3a73602d)


Till now, we only placed the Macros/ IPs along with IO ports. We did not place the standard cells. The idea is to take library information of cells in the design to implement the netlist and come up with an optimal placement which could possibly pass timing. The instances are placed according to the netlist on the design instances close to the pins are placed near the IO pads.

If there are hard paths then placement is performed and then based on wireload estimations cap is calculated and if slew threshold is not met buffers are added to regenerate the signals and help with signal integrity.

To do this, we do placement. Placement is of two types:

Global placement : Coarse placement and no legalizations considered
Detailed placement: legalizations are done (for example, where instances are placed according to standard cell rows.)
To run placement, the command is run_placement

![image](https://github.com/user-attachments/assets/ecf9c88e-c0db-420e-9eb4-7814a37a610e)

***Placemenr results dir***

![image](https://github.com/user-attachments/assets/3b669946-8625-4bf1-83a3-4c29cba2bd74)

***Layout after placement in Magic**

![image](https://github.com/user-attachments/assets/95a989fe-9787-4091-8a27-9e6038ebe956)

### Cell design flow ###

![image](https://github.com/user-attachments/assets/470c2878-5e64-4168-9a78-27898940d12e)

We need to first design a cell according to the inputs as shown above. Spice models contain fixed information from foundry like VTHO, tox, capacitances, etc. There could be a lot of user defined specification like cell height, drive strengths, VM (point where Vin == Vout), position of pins, supply voltage, pin layers required, drawn gate length.

In circuit design the circuit is implemented to get required functionality and W/L is found for PMOS and NMOS for creating layout.

Euler's path is used to come up with stick diagrams and are then implemented according to DRC rules.

The stage is design is complete. Now the characterization is performed to obtain .libs.


Charactization is of three types and performed in GUNA(spice simulator):
![image](https://github.com/user-attachments/assets/2f73ab60-a7f4-4b92-96d2-549dea7b2e49)

<Timimng characterization> 

## Day 3 ##

**Modifying the def and jump starting floorplan**

Modifying the floorplan.tcl 

![image](https://github.com/user-attachments/assets/c933d63d-e2fe-4b5e-831c-188f94c6515d)

![image](https://github.com/user-attachments/assets/1a2f5aa5-c507-491d-aa24-a6552401a25f)

Changed floorplan tracks.info

![image](https://github.com/user-attachments/assets/a1060777-b5c6-4057-9f4b-3567bc4b193d)

### Mask Layer based CMOS fabrication ###

Selecting the appropriate substrate, here we choose p type:

![image](https://github.com/user-attachments/assets/0470e0c5-5a3e-427b-859b-2802b55db299)

To create active regions, the first step is to grow a silicon oxide layer that will serve as an insulator. Next, a layer of Si3N4 is deposited on top. After this, photoresist is applied, and UV light is projected onto the areas to be removed. The red regions are protected by a mask, while the rest of the exposed regions react and can be washed away.

![image](https://github.com/user-attachments/assets/7c365fff-aec1-4584-916f-2569312ba4c9)

![image](https://github.com/user-attachments/assets/327a9a18-bee5-4278-b68d-242044603e29)

![image](https://github.com/user-attachments/assets/eb7adc4d-7a2f-4590-8d88-10cb19552f41)

![image](https://github.com/user-attachments/assets/d244916c-49ea-499d-a345-86ad5100a719)


Next step is to remove the photoresist.


![image](https://github.com/user-attachments/assets/f4a5c8b0-e641-4bed-bb90-6cdc44196ec0)

![image](https://github.com/user-attachments/assets/781ebb84-5f18-4fc2-bb08-c8f024c08884)

![image](https://github.com/user-attachments/assets/0af2f0cf-d241-47af-bb62-52210b89ae7f)


Next step is to remove or etch out the Si3N4.


![image](https://github.com/user-attachments/assets/86c856eb-faad-4707-8e94-9994823590d4)


Next, we need to create the n-well and p-well.

The n-well is used for PMOS fabrication, and the p-well is used for NMOS fabrication. Since both cannot be fabricated simultaneously, one area must be protected while the other is being processed.

The same steps are followed here: a layer of photoresist is deposited, and the pattern for the area to be protected is defined. Mask2 is then used to shield one area while fabricating the other.


![image](https://github.com/user-attachments/assets/90a6caa5-ff00-4e9e-a9f9-b7043c871424)


Next step is to expose this photoresist to the UV light. So, same this UV light will react only to the exposed photoresist area.

![image](https://github.com/user-attachments/assets/cf4021e9-9839-4de3-97d9-7ef70eda1017)


When we wash this particular thing into a solution, that exposed area of photoresist will washed away.

![image](https://github.com/user-attachments/assets/d9f37b7a-f84e-49b3-882f-7cf54d35b302)

We do ion implantation with boron atoms in this region. The oxide layer will be damnaged but will be taken care later.

![image](https://github.com/user-attachments/assets/c33100db-658e-4b3f-b7d8-e7fe600d9a47)


![image](https://github.com/user-attachments/assets/bc6164bf-9348-4078-941f-18cce858ecfe)


![image](https://github.com/user-attachments/assets/8f2e1f01-4ac1-4c58-88d0-2b2421cb38b2)


![image](https://github.com/user-attachments/assets/32786eea-b57b-4c71-9773-39c81d9eb9eb)

Now heat up the chip to reach required depth for the n and p well

![image](https://github.com/user-attachments/assets/ddb297af-7c65-448e-b9fb-16047a3501a0)

Threshold voltage is a function of doping concentration and oxide thickness. Hence it is important to be able to vary this.


![image](https://github.com/user-attachments/assets/8ce4e4d2-d9f5-4396-a51a-8274d20bf108)


![image](https://github.com/user-attachments/assets/b0ced528-43b8-4987-a0ae-b9d87ef211d3)


![image](https://github.com/user-attachments/assets/2a6dd3ac-0b26-4cbd-bbe0-69747b5b05f3)


![image](https://github.com/user-attachments/assets/9e5390ea-9b9e-4596-bfdf-e2549132640d)

![image](https://github.com/user-attachments/assets/6d70d734-a379-45e6-9eda-3bc64547ed9a)


![image](https://github.com/user-attachments/assets/eedd8032-f123-40c4-93e9-7b74715b29c1)


![image](https://github.com/user-attachments/assets/6473bcca-4935-425b-82b1-821f5a7fb688)


![image](https://github.com/user-attachments/assets/2439fd66-ce16-4934-a163-2d6b38a6c92b)



![image](https://github.com/user-attachments/assets/9b874e8e-ab19-4cca-867c-219b786b6741)


![image](https://github.com/user-attachments/assets/34ee1d2e-ed49-423c-8956-f9eef40dc4ed)

![image](https://github.com/user-attachments/assets/c49361c3-c1f0-4a02-8fd0-8d592285db74)


![image](https://github.com/user-attachments/assets/87d4c82e-fa03-4491-b573-5827540b259e)

![image](https://github.com/user-attachments/assets/1ea988e8-a1ec-4295-96e5-42ee29ce8d3f)

Till here, we have the local interconnects (0 level of metal), 1st level of interconnects (Aluminium interconnects).

Now the next step is to again take this metal levels to the higher level metal.

![image](https://github.com/user-attachments/assets/0a7c3932-a07c-459c-87d7-a1628c1b0cc8)

![image](https://github.com/user-attachments/assets/a67ad2ae-36a9-494d-9647-b83faf01679d)

![image](https://github.com/user-attachments/assets/db0e75b6-469e-4aed-abc3-66178acb74a8)

Final ooutcome": 

![image](https://github.com/user-attachments/assets/094628ae-dc33-40eb-83d9-8eaf9f27bddd)


**Design library cell using Magic layout and ngspice characterization**


Git cloning

![image](https://github.com/user-attachments/assets/c0c51808-8bd2-4650-ab04-e0aaae83a850)


Opening inverter layout 

![image](https://github.com/user-attachments/assets/721d01bc-48e0-4216-9675-b5ea043228c8)

Extracting the inverter & creating spice file:

![image](https://github.com/user-attachments/assets/16b3fa9f-2233-48b8-a611-93862689b99c)

![image](https://github.com/user-attachments/assets/7038b7c9-5c87-4664-a21b-03b65060dca9)


running the spice netlist:

![image](https://github.com/user-attachments/assets/39f3cfec-78aa-4aac-ad31-39e898b59f60)

![image](https://github.com/user-attachments/assets/2a480cf4-5438-462e-b3f9-5bb49b1c9a81)


***DRC checks***

Magicrc file 

![image](https://github.com/user-attachments/assets/69da132e-521a-4f84-b371-7d2b476c66ce)


View in Magic 

![image](https://github.com/user-attachments/assets/37ef0d36-7ffb-41ee-a86e-a91909f2ab59)

Opening MET3 in magic layout 
![image](https://github.com/user-attachments/assets/df1aa788-f806-434c-9564-305ec5a0fa57)

10 DRC violations found.

![image](https://github.com/user-attachments/assets/28b6b547-d9bb-475e-8927-3ab7a8cdea36)

Selecting a part of layout by left click and right click and hen press : drc why. It gives the reason for DRC violation and rule no.

![image](https://github.com/user-attachments/assets/6acebd96-6974-4da5-a48d-2d11be72d87a)

Rule 

![image](https://github.com/user-attachments/assets/15ed3fb9-dabb-41b7-8a93-be61ac45fc24)


Openinh tech file 

![image](https://github.com/user-attachments/assets/7c646292-e7fb-4540-a1de-f76a6739fbfa)

No rule defined between poly resistor to poly. Adding rule:

![image](https://github.com/user-attachments/assets/fad09b73-7652-49fc-9630-dbeb68dbbb1d)

tech load sky130A.tech 

Run DRC again and check

## Day 4 Pre layout design & clock Tree Synthsesis 

 

Timing modeling using delay tables

LEF file is having all the info regarding port definition. 
For place and route, we don't have these info. 

![image](https://github.com/user-attachments/assets/e2800f07-46f2-417f-b890-9c201ac429e8)

![image](https://github.com/user-attachments/assets/f0186cd4-9e5a-4654-86de-6a5cf2a716eb)

Extract LEF file and plugged into the flow. 

Guidelines
IO port must lie in the intersection of vertical & Horizontal tracks.

IWidth of std cell should be in the odd muliple of track pitch.Heightwill be odd multiple of vertical pitch. 

![image](https://github.com/user-attachments/assets/3484906b-1bc3-42ae-b8ee-75ba4e0e4138)

![image](https://github.com/user-attachments/assets/51a1401e-7115-4ba9-8b33-44b2d8241a7c)

Used during routing stage. Route can actually go over the tracks. 

Pressing G IN mAGIC will activate the grid. Convert grid to track value to verify the rule

SKY_L2 : Convert Magic Layout to std cell LEF  

Width of std cell should be odd multiple of 



SKY L4 Introduction to delay tabels

![image](https://github.com/user-attachments/assets/f4111046-ff13-45f7-a724-ce26a9c97f61)

Clock gating 







Delay tables usage part 1: 

![image](https://github.com/user-attachments/assets/0659b869-55b4-43dc-af0a-6ee072762656)
 
 each buffer is characterized for range of slew and range of load caps

Delay table of buffer with size 1
![image](https://github.com/user-attachments/assets/5547cc01-401c-46f1-b8d4-ffe064d77cd6)


When we are saying about changing the size of the buffer, we will be changing the W/L ratio of PMOS and NMOS. 

Delay table of buffer with size 2

![image](https://github.com/user-attachments/assets/c8cfc8f8-cd86-4796-8789-ecf364eaebeb)

And when we are increasing the PMOS size, we are actually reducing the resistance.And by varying the resistance we will be varying the RC delay. 
That's why we have individual delay tables for each buffer with different size.

Extraploiting delay(clock latency) numbers using numerical methods deducing an equation from the delay tables.

![image](https://github.com/user-attachments/assets/516580e7-6763-4cd6-a3c3-bfdefc2cee19)


 Calculating delay for buffer size 2

![image](https://github.com/user-attachments/assets/e1de7236-2e23-49a7-aabe-2a3ed872c779)

Calculating latency in each branch

![image](https://github.com/user-attachments/assets/5a4f3fd9-78c1-42e9-8191-0be98901c66c)

x9' + y15

Resultant skew seems to be zero 

![image](https://github.com/user-attachments/assets/917ddbf7-0b63-475f-a347-0a71f9eb4d17)

What if in each level we are driving different load? 
Skew will be having a non zero value. 
Clock Skew is the time difference between arrival of the same edge of a clock signal at the Clock pin of the capture flop and launch flop. 

Power Aware CTS 

![image](https://github.com/user-attachments/assets/d1a9843e-c0eb-418f-bf99-ad5c83817492)





SK2

Setup timing analysis and intro to flip flop setup time

Timing analysis using ideal clocks

Ideal scenario where clock trees are not yet build 

![image](https://github.com/user-attachments/assets/67aa8bbc-5c97-4f33-8124-93bc1b5840a7)

Combinaional delay should be less than clock period. 

![image](https://github.com/user-attachments/assets/a38c468c-b224-4599-a0d4-a3295ae1e6c1)

If delay exceeds the T, the clock period will be 

![image](https://github.com/user-attachments/assets/d8b1afd6-b737-438e-b7c6-1cc0cd7cf57f)

![image](https://github.com/user-attachments/assets/7717320e-ed3e-4109-932b-7a65d8ba9738)

![image](https://github.com/user-attachments/assets/acfecf0c-6358-4602-bec8-96f4fa73e11a)

Introduction to clock jitter and uncertainity. 

![image](https://github.com/user-attachments/assets/af2370fd-f8ba-4e04-a820-27e008cc9541)

Clock circuitry (PLLs) will not be able to egenrate clk perid with edge exactly at 0ns or tns. There will be inbuilt variation. 

![image](https://github.com/user-attachments/assets/a7887b1c-8752-47fc-a846-bde185fde1a9)

![image](https://github.com/user-attachments/assets/6ca2baba-5c5f-4b19-ac72-4a56012aabf5)

SU -> Setup uncertainity

![image](https://github.com/user-attachments/assets/a7a423bb-9db0-40ed-b140-fc99baa8220b)

![image](https://github.com/user-attachments/assets/105e0a0d-5c0d-4023-9fc3-7d4b72423b35)

![image](https://github.com/user-attachments/assets/f6844902-bccf-4f96-ab01-9fb477941de4)

<lab>


SK3

CTS TritonCTS & signal integrity

What is clk Tree synthesis and how does it fits into overall flow. 

![image](https://github.com/user-attachments/assets/885f83ca-f3e6-4528-bec7-5a0f2283c437)

Scenario : Physically connecting all the FF to clock path

![image](https://github.com/user-attachments/assets/15ed6e5f-1783-43cb-9a4e-50f8cac8e10f)

![image](https://github.com/user-attachments/assets/9b95d4cc-5d8b-477b-864f-692868150013)

Let say time taken by the clk to reach FF1 is t1
and time required to reach FF2 is t2 .Then t2-t1 --> Skew.
Clock skew refers to the difference in the arrival time of the clock signal at different points in the circuit (such as different flip-flops). 
Even though the clock signal is theoretically the same throughout the circuit, variations in the actual delivery time to different flip-flops can create timing issues. 
Clock skew directly affects the setup and hold time constraints of flip-flops. These are critical for ensuring that data is correctly captured by the receiving flip-flop (capture flop).

Setup Time Violation:

If the clock arrives too late at the capture flop compared to the launch flop, the data might not have enough time to propagate through the combinational logic and stabilize before the capture flop tries to capture it. This is called a positive skew scenario.
This can lead to a setup violation, where the data isn't stable before the capture clock edge, causing the capture flop to latch incorrect or unstable data.
Hold Time Violation:

If the clock arrives too early at the capture flop compared to the launch flop, the capture flop might try to capture data before it has had a chance to settle. This is called negative skew.

Ideally we will make skew as close to zero. 
![image](https://github.com/user-attachments/assets/c9444bfe-7378-4f1d-b10f-02d36967d5a4)

In order to get minimum skew, the above clock route will not be sufficient.

![image](https://github.com/user-attachments/assets/5800d97d-6273-4ecd-9766-5a044f844feb)

H-Tree

This will calculate the distance from clk source point to all other FFs and then calculate midpoint and design the tree.

![image](https://github.com/user-attachments/assets/65d098c7-c5cf-45e3-b479-4ada075ac87b)

Clock tree buffering 

![image](https://github.com/user-attachments/assets/53c08ee7-d450-47f9-9cb8-e60620c8d67f)

We will insert repeaters to reduce the delays caused by wire lenths.
Th repeater used in clk path have equal rise and fall time.
Each repeater buffer will reproduce the signal waveform and sends to the remaining cells with the help of repeaters
![image](https://github.com/user-attachments/assets/a8b8196e-63c1-4b5c-bd07-7317bd20d810)

Crosstalk & clock net shielding 

We have built clk tree such the clk skew = 0 using clk buffering and all. 
Clk nets are the critical nets in the design. Sometimes crosstalks will occur and the signal will be deteriorated. 

 Let's say I have shielded below highlighted clk net
![image](https://github.com/user-attachments/assets/60c40b9a-d44d-48ab-999e-3d23d0bc25e3)

It's like we are encapsulating the clk net from outside world. 
If the coupling cap between the clk net and the neighbouring net is high, as a result glitch and delta delay. 

![image](https://github.com/user-attachments/assets/a8e4f29d-cc52-4900-9a22-f0c29056f16c)

Red one is the aggresor and white is victim. This a clk net without shielding. 
A glitch can be a direct result of crosstalk between adjacent signal lines.

Crosstalk-Induced Glitches:
Crosstalk occurs when a switching signal (called the aggressor signal) induces unwanted voltage fluctuations in a neighboring, inactive signal line (called the victim signal).
This can cause the victim signal to momentarily change its state, leading to a glitch. For instance, if the victim line is supposed to stay at logic 0, crosstalk from the aggressor line can cause it to briefly spike to logic 1 and then return to 0. This spike is a glitch.

![image](https://github.com/user-attachments/assets/159f591c-0394-4eda-b269-46a3dc1fab15)

Shielding can avoid this. We will be breaking the coupling cap between aggressor and victim 
Shielding in the context of reducing crosstalk means inserting conductive traces (typically connected to ground or a fixed voltage) between signal lines to isolate them from each other. This helps reduce both capacitive coupling and inductive coupling, the two primary sources of crosstalk.

Capacitive coupling occurs when signal lines running close to each other behave like a capacitor, allowing electric fields to influence neighboring lines.
Inductive coupling happens due to magnetic fields generated by current-carrying conductors, causing interference in nearby conductors.
2. Techniques for Using Shielding to Reduce Crosstalk
a) Grounded Shield Traces
One of the most common techniques is placing grounded shield traces between signal lines.

How it works: By inserting grounded metal traces between high-speed signal lines, the capacitive and inductive coupling between adjacent signal lines is significantly reduced. The shield traces act as a barrier that absorbs and dissipates the electric and magnetic fields generated by the switching signals.

Implementation: For example, in a printed circuit board (PCB) layout, you can route ground traces between every critical signal trace or between groups of signal traces. This effectively creates a shield that prevents signals on one line from affecting adjacent lines.

Benefits: This significantly reduces crosstalk and is especially effective in critical signal integrity paths, such as data buses and clock lines.

b) Shielding Planes (Ground or Power Planes)
Another approach is to use ground planes or power planes in multilayer PCBs.

How it works: A ground or power plane is a large, continuous layer of copper connected to ground or a power supply. It provides a stable reference voltage and helps absorb the noise caused by high-speed signals.

Implementation: Typically, in multilayer PCBs, signal traces on one layer are placed above or below a ground plane. This creates a low-impedance return path for the signal and reduces the effect of crosstalk by providing better signal isolation.

Benefits: Ground planes not only reduce crosstalk but also improve signal integrity, reduce electromagnetic interference (EMI), and enhance the overall performance of high-speed circuits. 

<lab> 


SK4 

Setup time analsysis using real clocks

![image](https://github.com/user-attachments/assets/49814ec9-2a24-4d4d-b23d-03c20c0d68f3)

So here the clock will reach the FFs through real buffers and wires. (Clock net delay)

![image](https://github.com/user-attachments/assets/c6abca9d-9b5e-4c4c-b11a-dd35c81ca98d)

![image](https://github.com/user-attachments/assets/6716b175-3a37-4966-ac4d-c744b4a2a009)

![image](https://github.com/user-attachments/assets/3dfd6690-0e50-48eb-acff-0a1961dc2dbf)

![image](https://github.com/user-attachments/assets/0f0b872a-16fe-4098-8c47-09bdad830b4e)

![image](https://github.com/user-attachments/assets/98a59cce-e151-4fed-965d-8f641826fd30)

![image](https://github.com/user-attachments/assets/f62c7df9-d662-4db5-adf7-5791cc3dd1b4)

![image](https://github.com/user-attachments/assets/6880141d-2495-42b8-9a9e-b252f20b4342)

![image](https://github.com/user-attachments/assets/062bef3a-845b-456c-87a8-76c00ae60b8c)

We should make sure that the slack should be positive. Otherwise it's a violation

Hold timing analysis

 ![image](https://github.com/user-attachments/assets/113ffad2-6bd9-4885-8e9b-b6e8a2da68af)

Combinational delay > Hold time 

![image](https://github.com/user-attachments/assets/9b011b51-ae87-4bdb-9c6b-8a86d309cadb)

![image](https://github.com/user-attachments/assets/db38c8ee-0f57-4116-b048-de8938eaa00c)

In digital circuit design, **jitter** and **uncertainty** refer to variations in the timing of clock edges or signal transitions, which can affect the timing analysis of a circuit. **Hold time analysis** is generally less sensitive to jitter and uncertainty compared to **setup time analysis** for several reasons. Here's why jitter or uncertainty is typically **less critical** in hold time analysis:

### 1. **Nature of Hold Time Violations**:
Hold time violations occur when data changes too early, i.e., before the clock edge has stabilized at the capture flip-flop. The goal of hold time analysis is to ensure that the data remains stable for a certain period after the clock edge to avoid capturing incorrect values.

- **Hold time violations are concerned with very small time windows** (typically a few nanoseconds or less). The delay that needs to be analyzed is the **minimum path delay** between the launch and capture flip-flops (including the hold time margin).
- Since hold time constraints are met by ensuring the **data path delay** is not too fast, the impact of clock jitter (small timing variations) has a lesser effect because the clock edge must only ensure the signal doesn't change too early after launch.

### 2. **Comparison to Setup Time Analysis**:
In **setup time analysis**, we are concerned with ensuring that the data arrives at the capture flip-flop **before the next clock edge**. Here, any variation (jitter) in the clock edge can **directly reduce the available time** for data to propagate from the launch to the capture flip-flop.

- **Setup analysis** deals with the **maximum path delay** (i.e., how long the data takes to propagate through the combinational logic). Jitter in the clock signal can decrease the time available for the data to reach the capture flip-flop before the next clock edge, increasing the risk of a setup time violation.
- Hence, **jitter is more critical in setup time analysis** because even small variations in the clock edge can reduce the data arrival window significantly, affecting timing closure at higher clock speeds.

### 3. **Clock Skew and Hold Time**:
In hold time analysis, **clock skew** can sometimes work in favor of hold time requirements.

- **Positive skew** (where the clock arrives later at the capture flip-flop compared to the launch flip-flop) helps to **increase the effective hold margin**, reducing the risk of a hold violation.
- **Jitter in the clock signal** typically results in small variations around the ideal clock arrival time, but because hold time violations occur when the data changes too quickly, small timing variations don't usually cause issues. The timing margins in hold time analysis are more about preventing the data from changing too soon after the clock edge.

### 4. **Shorter Time Window for Hold Violations**:
The **time window** for hold time violations is typically much shorter than for setup time violations. Hold violations are generally concerned with the immediate vicinity of the clock edge, where the clock uncertainty (jitter or skew) does not have enough room to cause significant deviations.

- Since hold time violations are evaluated within a few nanoseconds or less, the small amount of jitter (in the range of picoseconds or small nanoseconds) is unlikely to push the circuit outside its valid timing window.

### 5. **Data Path Timing in Hold Analysis**:
In hold time analysis, the **data path delay** is typically dominated by the **minimum delay** through the combinational logic between two flip-flops. As long as this minimum delay is greater than the hold time requirement, the circuit is safe from hold violations.

- **Jitter affects the clock signal** but not the data path delay directly. In hold time analysis, since the delays are much smaller, the jitter in clock arrival times has a smaller impact compared to setup time analysis.

### Summary:
- **Hold time analysis** is concerned with ensuring that data does not change too quickly after the clock edge.
- **Jitter** and **clock uncertainty** tend to have a smaller effect on hold time violations because they only slightly shift the clock edge, and hold time constraints deal with much smaller timing windows compared to setup time.
- In many cases, **clock skew** can work in favor of hold time requirements, further reducing the sensitivity of hold time analysis to jitter.
- **Setup time analysis**, in contrast, is more sensitive to jitter, as the available time for data to stabilize is longer and more vulnerable to variations in clock timing.

Thus, jitter or uncertainty is less of a concern in **hold time analysis** because the timing windows involved are shorter, and small variations in clock edges are less likely to cause timing violations.

![image](https://github.com/user-attachments/assets/892a9e9b-97ee-43e9-9e45-80d2b72ad30c)

![image](https://github.com/user-attachments/assets/25131ead-8200-4cea-b222-67cc9aa9a18a)

![image](https://github.com/user-attachments/assets/6dd6c63b-3053-46d0-9254-d95d319275a4)

![image](https://github.com/user-attachments/assets/0c168432-b680-4fe8-9242-10b100fa0ad4)

![image](https://github.com/user-attachments/assets/6815d8f3-5449-41be-9089-ded47a44205a)
















