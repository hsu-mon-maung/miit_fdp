# miit_fdp
Day 1 Introduction to Verilog RTL Design and Synthesis

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

yosys> show

![image](https://user-images.githubusercontent.com/123365830/214506541-ccfad12b-90af-4a56-a77d-59644cdd7a8e.png)

SUB MODULE LEVEL SYNTHESIS AND ITS NECESSITY

In the following example, I am going to synthesize at sub_module 1 level

yosys>synth –top sub_modules1
yosys>abc –liberty ../lib/ sky130_fd_sc_hd__tt_025C_1v80.lib
yosys>show

After above command, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365830/214506705-7845b51d-bcfe-46f1-af00-2deedd42b4ca.png)

Glitches
Asynchronous and Synchronous Resets
In yosys terminal, type the command - !vim dff_asyncres.v –o dff_async_set.v

![image](https://user-images.githubusercontent.com/123365830/214506826-5de171b0-841b-40ff-b939-a793512dfacf.png)

$ iverilog dff_asyncres.v tb_dff_asyncres.v
$./a.out
$gtkwave tb_dff_asyncres.vcd

![image](https://user-images.githubusercontent.com/123365830/214506936-b7f1ed7e-d1e9-4a95-920b-0ff93b41422f.png)

•	Q follows d only at the posedge of the clock.
•	But as and when async_rest=1,Q becomes 0 without waiting for the next edge of the clock.

![image](https://user-images.githubusercontent.com/123365830/214506994-ad1a6c72-0a81-46f4-9aa0-7cda2d2c5585.png)

•	In the result,  when async_reset goes low(1 to 0),Q doesn't become 1 immediately ,it waits for the next clock edge to follow D.
•	Even if asunc_reset=1 and D=1, Q=0 as reset takes high precedence(that is how the code has been written,if condition of reset is checked first).

Synthesis implementation results : asynchronous set:

![image](https://user-images.githubusercontent.com/123365830/214507131-8c268266-f380-4d8a-bdba-534bea1efb26.png)

Synthesis implementation results : asynchronous reset

![image](https://user-images.githubusercontent.com/123365830/214507145-6d158823-3570-46e4-8c6a-f7310f7e24e0.png)

For Synchronous, Synchronous Reset and set :

![image](https://user-images.githubusercontent.com/123365830/214507203-6c09f864-c9a6-445d-a7f5-b33dfde424c1.png)

Synthesis Results:

![image](https://user-images.githubusercontent.com/123365830/214507246-8a6b5c12-4990-49ff-8404-34fc7f860ec5.png)

Case where in both both asynchronous and synchronous resets are applied together :
RTL Code:

![image](https://user-images.githubusercontent.com/123365830/214507286-20b00509-ad70-4cc3-9dfa-65de8d2111f9.png)

Synthesis results:

![image](https://user-images.githubusercontent.com/123365830/214507342-e9048eea-c4af-421d-87fb-6a99e8e1efb5.png)


Optimization
Let's Consider the following design where the 3 bit input is multiplied by 2 and the output is a 4 bit value.
RTL Code:

![image](https://user-images.githubusercontent.com/123365830/214507409-b55b4e7a-4e1e-47d6-9113-07c0cff9c611.png)

Synthesis Result:

![image](https://user-images.githubusercontent.com/123365830/214507477-f94f142d-d896-4258-9932-929dde86152a.png)

Let's consider the following design where the 3 bit input is multiplied by 9 and the output is a 6 bit value.
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a* 9;
endmodule

![image](https://user-images.githubusercontent.com/123365830/214507543-c64cf302-cdca-4f8e-b8da-28e2f9e2b3e6.png)

# Day 3 - Combinational and Sequential Optimizations

Introduction to Logic optimisations
The simulator performs many types of optimisations on the combinational and sequential circuits.
	1.Combinational optimisation methods:
	2.Sequential optimisation methods:


















