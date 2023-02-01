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

## Glitches

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
	
## Combinational Logic Optimisations

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

# Day 4 : Gate Level Simulations,Blocking vs Non Blocking assignments,Synthesis-Simulation Mismatch

## Introduction to Gate Level Simulations

GLS is running the test bench with the Netlist as Design under test.The RTL design is valided by providing stimulus to the testbench and it is checked whether it meets our specifications earlier that is running the test bench with the RTL code as our design under test.

Under GLS ,the netlist is applied to the testbench as desh under test . The behavioral level in the RTL code got transformed to the net list in terms of the standard cells present in the library. Therefore,net list is logically same as the RTL code. They both have the same inputs and outputs so the netlist should seamlessly fit in the place of the RTL code. The netlist is put in place of the RTL file and run the simulation with the test bench.

In GLS using iverilog flow, the design is a netlist which is given to Iverilog simulator in terms of standard cells present in the library. The library has different flavours of the same type of cell available. The GATE level verilog models is also given as an input to make the simulator to understand the specification of the different annotations of the cell . If the GATE level models are timing aware (delay annotated ),then we can use the GLS for timing validation as well.

## Synthesis Simulation Mismatches

* Missing sensitivity list
	
* Blocking and non blocking statements
	
## Blocking and non blocking statements Inside always block

* Blocking Executes the statements in the order it is written So the first statement is evaluated before the second statement

* Non Blocking Executes all the RHS when always block is entered and assigns to LHS. Parallel evaluation

## Labs on GLS and Synthesis-Simulation Mismatch

#### Example 1: A mux designed with the help of ternary operator. The RTL code is shown below.

Use the command : vim ternary_operator_mux 

	module ternary_operator_mux (input i0 , input i1 , input sel , output y);
		assign y = sel?i1:i0;
	endmodule

The synthesized result of the above example is shown below. To get this result, in the yosys terminal, use the following commands:

	read_liberty -lib ../lib/sky130RTLDesignAndSynthesisWorkshop
	
	read_verilog ternary_operator_mux.v
	
	synth -top ternary_operator_mux
	
	abc -liberty ../lib/sky130RTLDesignAndSynthesisWorkshop
	
	write_verilog -noattr ternary_operator_net.v
	
	show

Note : Make sure the directory is your directory.

![image](https://user-images.githubusercontent.com/123365830/215016542-a72ce11c-c3ce-4625-b904-40adf8e4ef13.png)

To invoke GLS,

* We need to read our netlist file and the test bench file assosciated with it.

* We need to read 2 extra files that contain the description of verilog models in the netlist.

To see the waveform of RTL simulation,we execute the following commands further

	iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
	
	./a.out
	
	gtkwave tb_ternary_operator_mux.vcd

The generated netlist does behave like a 2X1 multiplexer.

![image](https://user-images.githubusercontent.com/123365830/215020191-2d0d9d20-17cb-45fe-9278-b7242203193d.png)

#### Example 2: 
In this example,javascriptalways is evaluated only if javascriptselect is high.It is insensitive to javascriptio or i1 because javascriptselect is low.

	module bad_mux (input i0 , input i1 , input sel , output reg y);
	always @(sel)
	begin
		if(sel)
			y <= i1;
		else
			y <= i0;
	end 
	endmodule
	
The GTKwave simulation result is shown in following figure.

The design simulates a latch rather than a 2x1 mux. 

![image](https://user-images.githubusercontent.com/123365830/215020481-6f92cf23-567f-41ec-81ce-7b4a401dd729.png)

But the Yosys implementation shows a 2X1 mux .

![image](https://user-images.githubusercontent.com/123365830/215020548-9752a637-1c1d-4d44-a4f2-b20244f52ece.png)

Implement it's GATE level netlist through GLS and observe the waveform,it shows the behaviour of a 2X1 mux as shown below:

![image](https://user-images.githubusercontent.com/123365830/215020702-47b0970a-25fc-4712-9e98-700774a4f98a.png)

Since,the waveforms of stimulated RTL Code : Is of a LATCH the waveforms of gate level netlist thruogh GLS after synthesis: Is of 2X1 MUX We see a Synthesis-Simulation Mismatch.

#### Example 3: synthesis-simulation mismatch due to wrong order of assignment in blocking assignments

	module blocking_caveat (input a , input b , input c , output reg d);
	reg x;

	always @(*)
	begin
		d = x & c;
		x = a | b;
	end 
	endmodule
	
In this example, enter into the loop whenever any of the inputs a b or C changes but D is assigned with old X value since it is using the value of the previous Tclk ,the simulator mimics a delay or a flop. Whereas, during synthesis we see the the OR and AND gates as expected.

The GTKwave simulation result is shown in following figure.

![image](https://user-images.githubusercontent.com/123365830/215021520-91f1a5a8-3af5-40ad-aa39-bc8577f656b1.png)

At the instance where both the inputs a and b are 0. a | b should output 0, which when ANDed with c, should give an output y of 0. The output y thus should hold the value 0.Instead,it holds the value 1. 

But due to the blocking statements in the rtl code, x actually holds a the value of a OR b from the previous clock, hence giving us an incorrect output.

The netlist representation on synthesis is shown as below:

![image](https://user-images.githubusercontent.com/123365830/215021772-101b6cdb-2b7c-4930-8322-4f54f352dc42.png)

The synthesizer does not see the sensitivity list rather the functionality of the RTL design. The netlist representation does not include any latches to hold delayed values pertaining to the previous cycle. It only includes an OR 2 AND gate.

We observe the following waveform when we run gate level simulations on this netlist in verilog using the following command and do the same process that described above.

	iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
	
![image](https://user-images.githubusercontent.com/123365830/215022317-53b838f3-08e1-4403-923d-f6da6321e63b.png)

# Day 5 - If, Case, For Loop and For Generate

Using the If condition is to to write priority logic. The condition one has a priority or if it has more priority than the consecutive else statements. Only when condition 1 is not met, condition 2 is evaluated and so on. y is assigned accordingly depending on the matching conditions.

If-else block implements a Priority logic that is if cond_1 is satisfied, next if statements are not executed. The following if-else code translates to cascaded multiplexer structure in the final design instead of a single multiplexer.

	if (cond_1)
	begin 	
		y = statement_1;
	end
	else if (cond_2)
	begin
		y = statement_2;
	end
	else if (cond_3)
	begin
		y = statement_3;
	end
	else
	begin
		y = statement_4;
	end

#### Dangers of using Incomplete If statements Inferred Logic, which occurs due to bad coding styles that is incomplete if statements as shown in below.

	if (condt1) 
	    y=a;
	else if (condt2)
	    y=b;

In the sample code, if y is equal to a, it matches condt 1 and else if y is equal to b, it matches condt2. In this case, there is no matching condition when y does not match condt2. As a result of which the simulator tries to latch this case to the output y.It wants to retain the value of y.

Enable of this latch is OR of the condition 1 and condition 2. If neither condition 1 or condition 2 is met the OR gate output disables the latch . The latch retains the value of y and stores it. This is a combinational loop to avoid that the simulator infers a latch. 

This is called the inferred latch due to incomplete if statements which is very dangerous for RTL designing. It should be avoided except for some special cases like the counter.

Note:
If-case statements are used inside always block.
In verilog whatever variable we use to assign in if or case statements must be a register variable.

### CASE Constructs

Here, the inferred hardware should be a 4:1 multiplexer and Let's look at the following verilog code block. The CASE statements do not have priority logic like IF statements.

	always @(*)
	begin
	     case(sel)
			2'b00: begin
				y = statement_1;
				end
			2'b01: begin
				y = statement_2;
				end
			2'b10: begin
				y = statement_3;
				end
			2'b11: begin
				y = statement_4;
				end
		endcase
	end

Depending on the cases matching the select y is assigned accordingly.Some caveats with using CASE statements:

### 1.Incomplete CASE

	reg [1:0] sel
	always @(*)
	begin
	     case(sel)
	     2'b00: begin
			   . condition 1
			   end
	     2'b01: begin
			   . condition 2
			   end
	    end case
	    end
	    

Then select is C1 or C3 the conditions are not specified. It causes an incomplete case which results in inferred latches for these two cases that latch on to output y.This occurs when some cases are not specified inside the CASE block .For example, if the 2'b10 and 2'b11 cases were not mentioned , the tool would synthesize inferred latches at the 3rd and 4th inputs of the multiplexer. Solution is code case with default inside the CASE block so that the tool knows what to do when a case that is not specified occurs.

#### Correct code :

	reg [1:0] sel
	always @(*)
	begin
	     case(sel)
	     2'b00: begin
			   . condition 1
			   end
	     2'b01: begin
			   . condition 2
			   end
	    default :begin
			   . condition 3
			   end   
	    end case
	    end
	    
#### 2.Partial Assignments

	always @(*)
	begin
		case(sel)
			2'boo: begin
				x = a;
				y = b;
			2'b01: begin
				x = c;
			default: begin
				x = d;
				y = d;
				end
		endcase
	end
	
In the above example,the 2 outputs x and y and this will create two 4X1 multiplexers with the respective outputs. If we look at case 2'b01, we have specified the value of x for this case ,but not the value of y. It appears that it is okay to do so, as a default case is specified for both the outputs, and if we don't directly specify the value of y for any case, the simulator will implement the default case. This, however , is incorrect. In partial assignments such as this, the simulator will infer a latch at the 2nd input for multiplexer y as no value is specified for a particular case.

#### 3.Overlapping cases

	always @(*)
	begin
		case(sel)
			2'b00: begin
				y = a;
			2'b01: begin
				y = b;
				end
			2'b10: begin
				y = c;
			2'b1?: begin
				y = d;
				end
		endcase
	end

In the above sample code block ,2'b1? specifies that the corresponding bit can be either be 0 or 1. This means that when the sel input is holding a value 3 i.e 2'b11, cases 3 and 4 both hold true. What is synthesized depends on the mercy of the simulator. It can lead to Synthesis-Simulation mismatches.
If we used an IF condition here, due to priority logic, condition 4 would be ignored when condition 3 is met. However,in the CASE statement , even if the upper case is matched,all the cases are checked.So,if there is overlapping in cases,it poses a problem as the cases are not mutually exclusive. And we would get an unpredictable output.

## Labs on Incorrect IF and CASE constructs

Example 1: Incomplete If statements

The following file is incomp_if.v, and it can be found in the directory verilog_files. Use the command vim incomp_if.v.

	module incomp_if(input i0 , input i1 , input i2 , output reg y);
	always @(*)
	begin
		if(i0)
			y <= i1;
	end
	endmodule
	
In this code, an incomplete IF statement is contained and no else condition corresponding to it is mentioned . After simulating this design, following gtkwave is obtained.

![image](https://user-images.githubusercontent.com/123365830/215254366-327001a3-6317-4709-bba0-30286581f87e.png)

From the above waveform,there is no change in y when i0=0. It's equal to previous value when io=0. This result shows that latching Action, which is verified by looking at the synthesis implementation using Ysosys.

![image](https://user-images.githubusercontent.com/123365830/215254402-9534502c-46f3-410b-bc1f-3ba6d690c5a6.png)


Example 2: a similar example of incomp_if2.v

	module incomp_if2(input i0 , input i1 , input i2 , input i3,  output reg y);
	always @(*)
	begin
		if(i0)
			y <= i1;
		else if (i2)
			y <= i3;

	end
	endmodule
	
The above code contains an incomplete IF statement as well. Here, we have 2 inputs i1 and i3, as well as 2 conditional inputs i0 and i2. As we do not specifythe case when both i0 and i2 go low,which results in an issue in the synthesis. The gtkwaveform of the simulated design is below

![image](https://user-images.githubusercontent.com/123365830/215254441-9790de27-96df-4301-b333-0c6e9eefc548.png)

In this waveform result, When io is high,output follows i1. When io is low,it looks for i2.If i2 is high,it follows i3. But if i2 is low(and io is already low),y attains a constant value=previous output.

This can be verified by checking the graphical realisation of the yosys synthesis as shown in below.

![image](https://user-images.githubusercontent.com/123365830/215254471-4431ffd3-7d5d-47de-800c-48792be275e6.png)

Example3: A design with Incomplete Case's specification in a mux.

	module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);
	always @ (*)
	begin
		case(sel)
			2'b00: y = i0;
			2'b01: y = i1;
		endcase
	end
	endmodule

The truth table for the above 2X1 mux looks like as below. Whenever se[1]=1 ,latching action takes place.

![image](https://user-images.githubusercontent.com/123365830/215254566-f6ca15e3-269b-4ed2-b11c-408d577a0211.png)

The yosys synthesis implementation is given below.

![image](https://user-images.githubusercontent.com/123365830/215254598-a3e8b632-a784-474c-a845-8c6fba5f5c73.png)

Observation: 1. !(sel[1]) is going to D latch enable. 2.The inputs io,sel[0], !(sel[1]) go to the upper mixing logic that is implemented on D pin of the latch.

Example 4: Complete Mux along with all the cases specified.

	module comp_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);
	always @ (*)
	begin
		cae(sel)
			2'b00: y = i0;
			2'b01: y = i1;
			default:y = i2;
		endcase
	end
	endmodule
	
If i1 and io go low, output follows i2 at default case. Hence a 4X1 mux is synthesized without any latch that can be verified below.

![image](https://user-images.githubusercontent.com/123365830/215254712-a97056f0-088f-47b8-a5f2-4212cd9911aa.png)

Example 5: Partial Assignments

	module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel , output reg y , output reg x);
	always @ (*)
	begin
		cae(sel)
			2'b00: begin
				y = i0;
				x = i2;
				end
			2'b01: y = i1;
			default: begin 
				x = i1;
				y = i2;
				end
		endcase
	end
	endmodule
	
Expected Circuit: The 2X1 mux with output y is inferred without any latch. To find out the latching condition of the second mux we take the help of the following truth table:

![image](https://user-images.githubusercontent.com/123365830/215254755-d206e8fe-00af-4b8e-acf5-9b73d05a6c9d.png)

Condition for enabling:               en=sel[1]+!(sel[0]) 

sing #### Redundancy Theorem

After synthesis,Yosys implementation of the above design is:

![image](https://user-images.githubusercontent.com/123365830/215254806-8b29cb53-33f8-42a6-b322-67422022e23f.png)

Only 1 D latch is inferred for X. No latch is inferred for y.

Example 6: Design of 4X1 mux having overlapping cases

	module bad_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);
	always @ (*)
	begin
		cae(sel)
			2'b00: y = i0;
			2'b01: y = i1;
			2'b10: y = i2;
			2'b1?: y = i3;

		endcase
	end
	endmodule
	
In gtkwaveform of RTL simulation:

![image](https://user-images.githubusercontent.com/123365830/215254848-fe0977cc-d4b0-4294-a40f-9c1950a87eee.png)

Observation : When sel[1:0]=11, the output neither follows i2 nor i3. It simply latches to 1.

Whereas while running GLS on the netlist,the waveform of the synthesized netlist behaves as 4X1 mux as shown below:

![image](https://user-images.githubusercontent.com/123365830/215254862-28665718-4640-41a1-8ecc-3e79a0098643.png)

Thus ,Overlapping cases confuse the simulator and leads to Synthesis-Simulation Mismatches.

## Introduction to Looping Constructs

There are two types of FOR loops in verilog.

1.FOR loop 1.Used within the always block2. Used to evaluate expressions  

2.Generate FOR loop 1.Only used outside the always block 2.Used for instantiating hardware

### Necessity of FOR loops

For loops are extremely useful when we want to write a code /design that involves multiple assignments or evaluations within the always block. Lets us take an example: If we want to write the code for 4:1 multiplexer, we can easily do so using a either four if blocks or using a case block with 4 cases,as seen in the previous if-else blocks.But this approach is not suitable for complicated design with numerous inputs/outputs say 256X1 mux.If we wanted to design a 256X1 multiplexer, we will have to write 256 lines of condition statements using select and corresponding assignments. But in for loop ,be it 4X1 or 256X1 we would always be writing 4 lines of code only. Although we need to provide 256 inputs using an internal bus.

	integer k;
	always @(*)
	begin
		for (k = 0, k < 256, k= i  +1)
		begin
			if (k== sel)
				y = in[i];
			end
		end
	end

This code can be infinitely scaled up by just replacing the condition i < 256 with the desired specification for our multiplexer.Similarly, we can create High input demultiplexers as well.

	integer k
	always @(*)
	begin
		int_bus[15:0] = 16b'0;
		for (k= 0; k< 16; k= k+ 1) 
		begin
			if (k == sel)
				int_bus[k] = inp[k];
			end
		end
	end
	
Here , we have created a 16:1 demultiplexer using for loops within the always block. The int_bus[15:0] specifies our internal bus which takes on the input of the demux. It is necessary to assign all outputs to low for a new value of sel else latches will be inferred resulting in the incorrect implementation of our logic.

Below are few of the examples of FOR construct.

Example 1: file mux_generate.v that generates a 4X1 mux using For loop.

	module mux_generate (input  i0, input i1 , input i2 , input i3 , input [1:0] sel , output reg y);
	wire [3:0] i_int;
	assign i_int = {i3,i2,i1,i0};
	integer k;

	always @(*)
	begin
		for(k = 0; k < 4; k=k+1)begin
			if(k == sel)
				y = i_int[k];
		end
	end
	endmodule
	
The 4 inputs get assigned to a the internal 4 bit bus named i_int. After the simulation, the gtkwave is obtained as follow:

![image](https://user-images.githubusercontent.com/123365830/215255047-c3096ab6-7fe2-4c23-be39-6c4e94256019.png)

Example 2: Similar to example 1, file demux_generate.v that generates a 4X1 demux using For loop.

	module demux_generate (output o0 , output 02 , output o3 ,  output o4 , output o5 , output o6 , output o7 , input [2:0] sel , input i);
	reg [7:0]y_int;
	assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
	integer k;

	always @(*)
	begin
		y_int = 8'bo;
		for( k = 0; k < 8; k++) begin
			if(k == sel)
				y_int[k] = i;
		end
	end 
	endmodule

The above code has good readabilty,scalability and easy to write as well. Let's verify if it functions as a 8X1 demux as expected by viewing its gtkwave simulated waveform.

![image](https://user-images.githubusercontent.com/123365830/215255075-5577527e-c401-4d81-875f-44df953dc0c2.png)

### FOR Generate and its Uses

FOR Generate is used when we needto create multiple instances of the same hardware. We must use the For generate outside the always block.

We take example of a 8 bit Ripple Carry Adder(RCA) to understand the ease of instantiations provided by the For generate statement. An RCA consists of Full Adders tied in series where the carry out of the previous full adder is fed as the carry in bit of the next full adder in the chain. Hence, we can make use of generate for to instantiate every full adder in the design , as they are all represent the same hardware.

For this example , we use the file rcs.v which holds the code for the ripple carry adder. It also needs to be included in our simulation.

	module rca (input [7:0] num1 , input  [7:0] num2 , output [8:0] sum);
	wire [7:0] int_sum;
	wire [7:0] int_co;

	genvar i;
	generate
		for (i = 1; i < 8; i=i+1) begin
			fa u_fa_1 (.a(num1[i]),.b(num2[i],.c(int_co[i-1],.co(int_co[i]),.sum(int_sum[i]));
		end

	endgenerate
	fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));

	assign sum[7:0] = int_sum;
	assign sum[8] = int_co[7];
	endmodule
	
Here, fa references another verilog design file containing the definition of for the full adder submodules .This is shown below, from the fa.v file

	module fa(input a, input b , input c,  output co, output sum);
		assign  {co,sum} = a +b + c;
	endmodule

n the RCA verilog code, we instantiate fa in a loop using generate for outside the always block.

Rules for addition :

N + N bit number --> Sum will be N + 1 bits N +M bit number --> Sum will be max(N,M) +1 bits

Now, let us simulate this design in verilog and view its waveform with GKTWave .As the rca design referances the file fa.v , we must specify it in our commands as follows

	iverilog fa.v rca.v tb_rca.v
	./a.out
	gtkwave tb_rca.v
	
The resulting gtkwaveform is shown below that shows an adder being simulated:

![image](https://user-images.githubusercontent.com/123365830/215255162-35689924-6b32-4447-8acf-8f5da2aaa704.png)


#### Acknowledgment:

1.Kunal Ghosh - Co-founder(Vsd corp. pvt.ltd.)

2.Shon Taware

# Day 6 Introduction to FPGA Programming

#### Example : counter_clk_div.v

The simulation result of this is shown as below

![image](https://user-images.githubusercontent.com/123365830/215696423-39693d8e-009f-44a4-8571-7dc5e6107ccd.png)

![image](https://user-images.githubusercontent.com/123365830/215696454-0368e3aa-76b0-4940-8dc0-ffbce646b707.png)

RTL Schematic Design:

![image](https://user-images.githubusercontent.com/123365830/215696821-3586e4ee-51a5-4874-be8c-d3c940c89353.png)

Synthesized Design :

![image](https://user-images.githubusercontent.com/123365830/215697068-ff87b790-69c2-4d86-9026-d91de505bf9c.png)

![image](https://user-images.githubusercontent.com/123365830/215697130-9a860fc9-1556-4e02-b997-a9fe7a533108.png)

#### constraints.xdc

![image](https://user-images.githubusercontent.com/123365830/215700732-9af0af0f-4e5c-4dad-af08-a6661b671e70.png)

Report Timing Summary : All users specifeid timing constraints are met and the screenshot is shonw in below:

![image](https://user-images.githubusercontent.com/123365830/215697786-3c8c196a-2be7-4bdd-8bd0-98c0e6c43769.png)

Report Utilization:

![image](https://user-images.githubusercontent.com/123365830/215698300-abbc6ecf-0762-4a4d-af11-2cc2920a2bcf.png)

Generate Bitstream and write to target device (bassy3 board)

![image](https://user-images.githubusercontent.com/123365830/215698864-5acefb38-e391-4209-8f17-9eb680999156.png)

![image](https://user-images.githubusercontent.com/123365830/215698898-4adb4f30-ac91-4f68-8243-ce948629cee2.png)

Warning! is occured in this process like that "The debug hub core was not detected at user scan chain 1 or 3."

#### counter_clk_div_vio.v

![image](https://user-images.githubusercontent.com/123365830/215699612-76e10aa9-453e-48cc-ad64-1ff6579dd3ae.png)

![image](https://user-images.githubusercontent.com/123365830/215699821-d840dbfa-03ed-4231-830f-e839eeb4a5fa.png)

After that the following errors has occured.

![image](https://user-images.githubusercontent.com/123365830/215699969-54f36f16-9030-4b4a-ab80-183bea8791d7.png)

![image](https://user-images.githubusercontent.com/123365830/215700027-55a7a2b4-729a-4f6f-b3ab-bafade7f96eb.png)

# Day 7 Openlane

OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault and custom methodology scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII - this capability will be released in the coming weeks with completed SoC design examples that have been sent to SkyWater for fabricaiton.

### Openlane Directory Structure

![image](https://user-images.githubusercontent.com/123365830/215971305-66a0e738-721b-4453-8706-7179534a303f.png)

the command used : cd libs.ref

![image](https://user-images.githubusercontent.com/123365830/215974498-3078122f-0664-4b5a-a0bc-d0695abfd8cf.png)

the command used : cd libs.tech

![image](https://user-images.githubusercontent.com/123365830/215974550-26ebee48-c62e-464c-a026-8762ad5fb7ec.png)

### Setting up docker bouilt:

	git clone git@github.com:efabless/openlane --branch rc2

	cd openlane/docker_built

	make merge

![image](https://user-images.githubusercontent.com/123365830/215976381-21ce87ff-b715-42a8-a73c-76cbe8d1a732.png)

### Running Openlane

After Successfully built, type the commands:

cd ..

docker

./flow.tcl –interactive

After that, the following result is shown

![image](https://user-images.githubusercontent.com/123365830/215976692-0d699ed9-9814-44f7-8ef5-5dba4b85055f.png)

Adding a design:

cd /Desktop/work/tools/openlane_working_dir/openlane/designs

ls -ltr 

![image](https://user-images.githubusercontent.com/123365830/215976853-a1a07c2b-02b8-4cfb-9a04-acf98c3a9378.png)

![image](https://user-images.githubusercontent.com/123365830/215976898-772bbfe2-b431-4f62-939e-aa776d29a02a.png)
































	
















































