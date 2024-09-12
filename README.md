Day 0: Important Links
VSD-IAT

nickson-jose/vsdstdcelldesign: This repository contains all the information needed to run RTL2GDSII flow using openlane flow. Apart from that, it also contain procedures on how to create a custom LEF file and plugging it into an openlane flow. (github.com)

To continue working on a particular run folder, <desired_tage> is the folder name:

prep -design <design_name> -tag <desired_tag>
Workshop Github material https://github.com/google/skywater-pdk https://github.com/nickson-jose/vsdstdcelldesign ttps://sourceforge.net/projects/ngspice/ https://github.com/ https://www.vlsisystemdesign.com/wp-content/uploads/2017/07/Introduction-to-Industrial-Physical-Design-Flow.pdf

Day 1
open lane directory structure

![image](https://github.com/user-attachments/assets/f781a17e-b9e8-461f-b77a-8454d8a0ff67)

![image](https://github.com/user-attachments/assets/ea4fe63a-768a-455c-ab1d-4c7d8f2fd657)

![image](https://github.com/user-attachments/assets/460962a4-1633-45fc-8f22-3bf55ac8ebcc)

![image](https://github.com/user-attachments/assets/2e24fea1-633d-4267-bb3d-467f649e1f7d)



![image](https://github.com/user-attachments/assets/5b613966-4279-4824-9841-92fd778dfde0)










Day 4 

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













