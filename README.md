# miit_fdp
Day 1 Content

Introduction to Verilog RTL Design and Synthesis
Labs using iverilog and gtkwave
mkdir vsd  
 cd vsd  
 git clone https://github.com/kunalg123/vsdflow.git  
 mkdir vlsi  
 cd vlsi  
 git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git  
 cd SKY130RTLDesignAndSynthesisWorkshop  
 cd my_lib  
 cd lib  
 cd ..  
 cd verilog_model  
 cd ..  
 cd ..  
 cd verilog_files
 
 ![image](https://user-images.githubusercontent.com/123365830/214255354-a501ec35-f3ca-419f-9f02-97ab900b6b2d.png)
 
Below screenshot shows the above directory structure inside the vsd upto my_lib directories that was set up through the terminal.

![image](https://user-images.githubusercontent.com/123365830/214255608-c510ea15-7cba-4859-bde0-09a1327426bc.png)

Below screenshot is git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop

![image](https://user-images.githubusercontent.com/123365830/214255725-ebac961f-5015-4757-86bf-f10216e7c25b.png)

Below screenshot shows directory by cloning the sky130RTLDesignAndSynthesisWorkshop

![image](https://user-images.githubusercontent.com/123365830/214255834-dca48b8e-2139-42cb-81f7-0edbc9e12958.png)

Below screenshot shows the list of verilog files.

![image](https://user-images.githubusercontent.com/123365830/214255953-3ccf2e7a-8744-4f4a-a402-443025199f2e.png)

After this command - iverilog good_mux.v tb_good_mux.v, following list of files can be seen.

![image](https://user-images.githubusercontent.com/123365830/214256202-9a09099f-9d56-4610-a205-2d0b42868e7c.png)

Below screenshot shows dumping the output into a vcd file by ./a.out

![image](https://user-images.githubusercontent.com/123365830/214256320-93710ae8-3979-4c24-8974-0f2807eb1c36.png)

Below screenshot is gtkwave window.

![image](https://user-images.githubusercontent.com/123365830/214256431-11dd6fbb-e0aa-4d3a-9ac0-442cf04d689a.png)

after that Error can be occured : gvim tb_good_mux.v -o good_mux.v

![image](https://user-images.githubusercontent.com/123365830/214256856-f633342f-a9ce-49d9-a4d3-3cc62adee5ed.png)

Below screenshot is vim tb_good_mux.v -o good_mux.v

![image](https://user-images.githubusercontent.com/123365830/214256968-15bf2b1d-eed8-4b50-a7e1-d3fd63334446.png)

Below screenshot shows after synth -top good_mux

![image](https://user-images.githubusercontent.com/123365830/214257163-953bfae9-7817-4145-b3a0-e89d7e8dcb52.png)

![image](https://user-images.githubusercontent.com/123365830/214257267-ab8c8c7e-8f47-49b2-9517-ea4cd8d62d0a.png)

Below screenshot is after show command.

![image](https://user-images.githubusercontent.com/123365830/214257375-66e5085b-a03e-4d56-a04c-fdfeb9aa81c8.png)

Day 2 - Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

The following window appears that shows the library file sky130_fd_sc_hd__tt_025C_1v80.lib
!vim ../lib/SKY130_fd_sc_hd__tt_025C_1v80.lib

![image](https://user-images.githubusercontent.com/123365830/214502415-d01d4b82-4899-4ff9-a684-29c4e54e1e5f.png)

Switching off the syntax color red
  Command used : syn off

![image](https://user-images.githubusercontent.com/123365830/214502458-da91030a-10cb-4e84-9678-d0ba74e0cabf.png)


Enabling the line numbers
  Command used :se nu

![image](https://user-images.githubusercontent.com/123365830/214502577-d3fe858e-b470-4e54-b146-d1280e02f498.png)


![image](https://user-images.githubusercontent.com/123365830/214502605-8ecc27df-64ca-412e-8195-8dde77a635e1.png)

![image](https://user-images.githubusercontent.com/123365830/214502638-1b09d5a9-3350-4968-b92d-6ab8ff44ec4e.png)

![image](https://user-images.githubusercontent.com/123365830/214502665-f362755e-b50f-4c8a-84ae-bdb544e2330e.png)


Command used - :vsp

![image](https://user-images.githubusercontent.com/123365830/214502706-3d1673de-19a0-4104-9fdc-065dfb555f73.png)

Command used -  🆚

![image](https://user-images.githubusercontent.com/123365830/214502770-1e465fd7-95f5-4e0b-a5a6-6e9a0fa1f584.png)

Command used -    !vim multiple_modules.v

![image](https://user-images.githubusercontent.com/123365830/214502821-8c63f2a8-a8b6-4fb6-9ecf-4d1b44660049.png)

After the command ----  synth –top multiple_modules, the following screenshot will be shown.

![image](https://user-images.githubusercontent.com/123365830/214502868-4003d1bf-21ba-4a84-8068-f3f6c1e3c80a.png)

Command used -- abc  –liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![image](https://user-images.githubusercontent.com/123365830/214502916-b8f32520-d081-4bae-bd58-eeb8e9aba340.png)

After the command ------ show multiple_modules, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365830/214502966-df5c856b-66ab-4b1d-8318-b8c02b2f03c4.png)

yosys>write_verilog –noattr  multiple_modules_hier.v
$!vim multiple_modules_hier.v

![image](https://user-images.githubusercontent.com/123365830/214503042-865e456a-f1e0-4901-b230-834bf444dc64.png)





