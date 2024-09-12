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







 




