# miit_fdp
# Day 1 Introduction to Verilog RTL Design and Synthesis

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

After that Error can be occured : gvim tb_good_mux.v -o good_mux.v

![image](https://user-images.githubusercontent.com/123365830/214256856-f633342f-a9ce-49d9-a4d3-3cc62adee5ed.png)

Below screenshot is vim tb_good_mux.v -o good_mux.v

![image](https://user-images.githubusercontent.com/123365830/214256968-15bf2b1d-eed8-4b50-a7e1-d3fd63334446.png)

Below screenshot shows after synth -top good_mux

![image](https://user-images.githubusercontent.com/123365830/214257163-953bfae9-7817-4145-b3a0-e89d7e8dcb52.png)

![image](https://user-images.githubusercontent.com/123365830/214257267-ab8c8c7e-8f47-49b2-9517-ea4cd8d62d0a.png)

Below screenshot is after show command.

![image](https://user-images.githubusercontent.com/123365830/214257375-66e5085b-a03e-4d56-a04c-fdfeb9aa81c8.png)

# Day 2 - Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

The following window appears that shows the library file sky130_fd_sc_hd__tt_025C_1v80.lib

!vim ../lib/SKY130_fd_sc_hd__tt_025C_1v80.lib

![image](https://user-images.githubusercontent.com/123365830/214502415-d01d4b82-4899-4ff9-a684-29c4e54e1e5f.png)

Switching off the syntax color red
  Command used : syn off

![image](https://user-images.githubusercontent.com/123365830/214502458-da91030a-10cb-4e84-9678-d0ba74e0cabf.png)

yosys> show

![image](https://user-images.githubusercontent.com/123365830/214506541-ccfad12b-90af-4a56-a77d-59644cdd7a8e.png)

# SUB MODULE LEVEL SYNTHESIS AND ITS NECESSITY

In the following example, I am going to synthesize at sub_module 1 level

yosys>synth –top sub_modules1
yosys>abc –liberty ../lib/ sky130_fd_sc_hd__tt_025C_1v80.lib
yosys>show

After above command, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365830/214506705-7845b51d-bcfe-46f1-af00-2deedd42b4ca.png)

# Glitches

Asynchronous and Synchronous Resets

In terminal, type the command - !vim dff_asyncres.v –o dff_async_set.v

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
	
# Combinational Logic Optimisations

To understand each of the combinational optimisations, we can try through different RTL code examples. 
To understand how the optimisations take place, we check the synthesis implementation through yosys All the optimisation examples are in files opt_check.v, opt_check4.v, and multiple_modules_opt.v and these files are present under the verilog_files directory.

Example 1: opt_check.v

module opt_check (input a, input b , output y);
	assign y = a?b:0;
endmodule

In this example, the constant 0 propagates further in the logic. we obtain y = ab by using boolean simplification.
Synthesizing this in yosys : After the command : synth –top opt_check, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365830/214760492-240f8950-508b-4d2c-887a-4b585f5e478c.png)

To remove all unused cells and wires to prduce optimised digital circuit using the opt_clean -purge command as shown below:

![image](https://user-images.githubusercontent.com/123365830/214760572-6eb57b66-2a56-4488-878b-a6cda287255a.png)

Next, we use the following commands.

	abc -liberty ../my_lib/lib/sky130_fd_sc_hd_tt_025C_1v80.lib  
 	write_verilog -noattr opt_check_netlist.v 
 	show

The graphical synthesis realisation is shown in the following figure and the Yosys has synthesized an AND gate.

![image](https://user-images.githubusercontent.com/123365830/214760912-a5c907ec-f304-42d0-a4d5-da552b2d1545.png)

Example 2 : opt_check2.v

![image](https://user-images.githubusercontent.com/123365830/214761104-3d791d13-3277-47a4-bd66-100f823ec1fd.png)

In this example, the expected output y to be an OR gate, because the output of the mux can be simplified to y = a + b. If we generate the netlist and its graphical representation is like the  following result.

![image](https://user-images.githubusercontent.com/123365830/214763724-fb88d9b9-9823-451a-b6f9-9b18a71a4ab5.png)

The synthesis tool instead of OR gates infers a nand gate with inverted inputs based on Demorgan's Law.

Example 3: opt_check3.v

The RTL verilog code of opt_check3.v is:

![image](https://user-images.githubusercontent.com/123365830/214763939-cbac5c38-266d-4d00-955a-dd30a583fc47.png)

The output is to be a 3 input AND gate based on constant propagation and boolean logic optimisation.The output y can be simplified to y = abc.

After synthesis, graphical representation of its is shown in below. Yosys synthesizes a 3 input AND gate as expected because of optimisations.

![image](https://user-images.githubusercontent.com/123365830/214764271-7ab5f054-8919-43ef-825f-a4ab55f0cc78.png)

Example 4: opt_check4.v

In this example, the boolean logic optimisation simplifies the output y = a xnor c (single xnor gate). The RTL code is:

![image](https://user-images.githubusercontent.com/123365830/214764987-0c0b5bc3-90b4-4de9-98dd-b5c719ecb0fa.png)

After the synthesis, generate the netlist and observe its graphical representation is like below:

![image](https://user-images.githubusercontent.com/123365830/214765053-a793ba58-a9eb-4b03-8b52-d8dc46207824.png)

Example 5: multiple_module_opt.v

RTL Code :

![image](https://user-images.githubusercontent.com/123365830/214765567-b57df713-ed39-4ff8-8b37-54fd35384515.png)

In synthesizing process, use flatten before opt_clean -purge. 

Both submodule1 and 2 are instantiated in this multiple_module_opt. 
We must use Flat Synthesis here otherwise the optimisations will not be performed on the sub module level. The synthesized result is shown below.

![image](https://user-images.githubusercontent.com/123365830/214765615-f5024c1b-db4b-493c-b47c-d06d18540507.png)

Example 6: multiple_module_opt2.v


![image](https://user-images.githubusercontent.com/123365830/214765887-a50c5ce5-db03-44bf-a0a5-06e8b5a5cc28.png)

In this boolean optimisation, obtain the output y=1 simply. It's synthesis yields:

![image](https://user-images.githubusercontent.com/123365830/214765946-fb136644-2f0c-43cf-a744-cc0a99a44b0e.png)

# Sequential Logic Optimizations

Example 1: dff_const1.v

![image](https://user-images.githubusercontent.com/123365830/214766653-0f9a6bb0-46bf-42dd-b929-478295600e09.png)

In this example, the output Q should be equal to an inverted reset or Q= !reset. However, as the reset is synchronous, even if the flop has D pinned to logic 1, when reset becomes 0, Q does not immediately go to 1. It waits untill the positive edge of the next clock cycle.

![image](https://user-images.githubusercontent.com/123365830/214766760-1fc3ec07-8ace-4a1e-b96b-cdabf7ce99b4.png)

In the gtk waveform above , when reset becomes 0, Q becomes 1 at the next clock edge. Since Q can be either 1 or 0,we do not get a sequential constant, and no optimisations should be possible here. 

In yosys synthesis,  the netlist is generated by using the following command.

	abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib 
	
	write_verilog -noattr dff_const1_netlist.v 
	
	show
While synthesis, we use the command : dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib

dfflibmap is a switch that tells the synthesizer about the library to pick sequential circuits( mainly Dff's and latches) from.

![image](https://user-images.githubusercontent.com/123365830/214767358-10361de3-c17e-42ab-8dd2-dc06244002ef.png)

In this output : No optimisation is performed in th yosys implementation during synthesis.

Example 2 : dff_const2.v

![image](https://user-images.githubusercontent.com/123365830/214767647-8eefa01c-10f0-4e0a-8071-9877c142ff0c.png)

In this example, regardless of the inputs, the output q always remains constant at 1 and viewing the VCD with GTKWave as follows:

![image](https://user-images.githubusercontent.com/123365830/214767688-ec872701-94cf-4637-9717-53bf5cc32aba.png)

It can easily be optimised during synthesis because the output q is always constant.

![image](https://user-images.githubusercontent.com/123365830/214767737-2a59d7e2-d2a8-4dbe-bab1-2c4b4d6e6d7f.png)

Example 3 : dff_const3.v

![image](https://user-images.githubusercontent.com/123365830/214768233-6715960e-a8da-4be1-ab63-599c8d8ed502.png)

When reset goes from 1 to 0, Q1 follows D at the next positive clock edge in an ideal ckt. 

But in reality, Q1 becomes 1 a little after the next positive clk edge(once reset has been made 0)due to Clock-to-Q delay.

So, q takes the value 0 until the next clock edge when it read an input of 1 from q1. The simulated result is shown in below.

![image](https://user-images.githubusercontent.com/123365830/214768386-03fe3b22-a620-4914-a7e4-3af1042d6d24.png)

It is wrong to say that Q=!(reset) or Q=Q1 because Q takes both logic 0 and 1 values in different clock cycles.

Hence, both the flip-flops are retained and no optimisations are performed on this design. Both the D flip-flops are present in the synthesized netlist.

Yosys synthesis result is shown in below:

![image](https://user-images.githubusercontent.com/123365830/214768790-053164e2-2ffd-4091-94db-b35a29cb62ea.png)

Example 4: dff_const4.v

RTL Code is : 

![image](https://user-images.githubusercontent.com/123365830/214769112-9270738f-3b71-4312-8925-dca6c1025a16.png)

In this example, regardless of the input whether reset or not , Q1 is always going to be constant i.e. Q1=1 . As q can only be 1 or q1 depending on the reset input , but q1 = 1 . Therefore,  q is also constant at the value 1. 

The simulated waveform is shown in below:

![image](https://user-images.githubusercontent.com/123365830/214769499-bbc85ae3-8c9b-472d-bc2a-4fed5a095bfa.png)

As the output is always constant, it can easily be optimized. The yosys synthesis is shown in the following.

![image](https://user-images.githubusercontent.com/123365830/214769545-06ee7f3e-8e02-4af8-b4b8-c193e1046a00.png)












































