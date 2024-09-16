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

**Design preparation step**

prep -design picorv32a

![image](https://github.com/user-attachments/assets/aecb44c5-38b3-43cd-af5a-46f30ba676b1)











**Day 4** 

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
















