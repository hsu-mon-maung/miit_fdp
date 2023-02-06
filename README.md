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

# Day 7 Introduction to Openlane

OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault and custom methodology scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII - this capability will be released in the coming weeks with completed SoC design examples that have been sent to SkyWater for fabricaiton.

It is started as an Open-source flow for a true Open Source tape-out Experiment. striVe is a family of open everything SoCs:

* Open PDK
* Open EDA
* Open RTL

The main goal of OPENLANE is to produce a clean GDSII with no human intervation (no-human-in-the-loop). here the meaning of clean is that:
* No LVS violations

* No DRC Violations

* No timing Violations

OPENLANE is tuned for skyWter130nm open PDK. it can be used to harden Macros and chips.there is two mode of operation

* Autonomus : it is the push botton flow. with the push botton , it is a some time base design and due to this push botton, we get final GDSII

* interactive : here we can run comamds and steps one by one.

It has large number of design examples(43 designs with their best configurations).

### Openlane Directory Structure

![image](https://user-images.githubusercontent.com/123365830/215971305-66a0e738-721b-4453-8706-7179534a303f.png)

the command used : cd libs.ref

![image](https://user-images.githubusercontent.com/123365830/215974498-3078122f-0664-4b5a-a0bc-d0695abfd8cf.png)

the command used : cd libs.tech

![image](https://user-images.githubusercontent.com/123365830/215974550-26ebee48-c62e-464c-a026-8762ad5fb7ec.png)

### OpenLANE Design Stages

OpenLANE flow consists of several stages. By default all flow steps are run in sequence. Each stage may consist of multiple sub-stages. OpenLANE can also be run interactively which will be shown below.

#### 1. Synthesis

yosys - Performs RTL synthesis

abc - Performs technology mapping

OpenSTA - Pefroms static timing analysis on the resulting netlist to generate timing reports

#### 2.Floorplan and PDN

init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)

ioplacer - Places the macro input and output ports

pdn - Generates the power distribution network

tapcell - Inserts welltap and decap cells in the floorplan

#### 3. Placement

RePLace - Performs global placement

Resizer - Performs optional optimizations on the design

OpenDP - Perfroms detailed placement to legalize the globally placed components

#### 4. CTS

TritonCTS - Synthesizes the clock distribution network (the clock tree)

#### 5. Routing *

FastRoute - Performs global routing to generate a guide file for the detailed router

TritonRoute - Performs detailed routing

#### 6. GDSII Generation

Magic - Streams out the final GDSII layout file from the routed def

#### 7. Checks

Magic - Performs DRC Checks & Antenna Checks

Netgen - Performs LVS Checks

### 8. OpenLANE ASIC Flow (Detailed)

![image](https://user-images.githubusercontent.com/123365830/216042455-0611e571-f057-4610-a333-10d3ec218c50.png)

The design exploration utility is also used for regression testing(CI). we run OpenLANE on ~ 70 designs and compare the results to the best known ones.

### 9. DFT(Design for Test)

It perform scan inserption, automatic test pattern generation, Test patterns compaction, Fault coverage, Fault simulation

![image](https://user-images.githubusercontent.com/123365830/216042788-41d82404-a407-4671-95d1-e6e01a57ae2b.png)

After that physical implementation is done by OpenROAD app. physical implementation involves the several steps:

* Floor/Power Planning

* End Decoupling Capacitors and Tap cells insertion

* Placements: Global and Detailed

* Post Placement Optimization

* Clock Tree synthesis (CTS)

* Routing: Global and Detailed
Every time the netlist is modified.(CTS modifies the netlist and Post Placements optimization also modifies the netlist).so for that verification must be performed. The LCE(yosys) is used to formally confirm that the function did not change after modifying the netlist. ### Dealing with antenna rules Violation: when a metal wire segment is fabricated, it can act as antenna.as an antenna, it collect charges which can demaged the transister gates during the fabrication.

![image](https://user-images.githubusercontent.com/123365830/216043393-2978f405-d20a-40be-b808-8b629eb7eea1.png)

To address this issue, we have to limit the lenght of the wire. usually this is the job of the router. If router fails to do this, then there are two solutions:

* Bridging attaches a higher layer intermediary

![image](https://user-images.githubusercontent.com/123365830/216043502-da9ebae8-1ef5-4577-9e03-eb086145a001.png)

Add antenna diode cell to leak away charges.(Antenna diodes are provided by the SCL)

![image](https://user-images.githubusercontent.com/123365830/216043900-389bf10b-d9bf-4cf3-9ed3-ce2504ff4dfc.png)

With OpenLANE, we took a preventive approach. here we add fake antenna diode next to every cell input after placement. Then run the Antenna checker on the routed layout. If the checker reports a violation on cell input pin, replace the fake diode cell by a real one.

![image](https://user-images.githubusercontent.com/123365830/216043957-b8e12ad9-842f-4b01-95a0-f5f41719c8bf.png)

### Static Timing analysis(STA)

It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. resulting report will shows the timing violations if any violations is there.

### Physical Verification (DRC and LVS)

Magic is used for design Rules checking and SPICE Extraction from Layout. Magic and Netgen are used for LVS.

## OpenLANE Directory Structure in detail

To list the details in cronological order, cd, ls and ls -ltr commands are used.

Here we are working in Sky130_fd_sc_hd PDK variant : 

where, "sky130" is process name or node name.

"fd" is a foundary name (skyWater foundary).

"sc" means standerd cell librery files and the last one "hd" stands for high density(basically one type of varient).

Sky130_fd_sc_hd varient contains many technology files like verilog, spice, techlef, meglef,mag,gds,cdl,lib,lef,etc. (techlef file contains the layer information).

### Design Preparation Step

Open the terminal and go to the path “openlane” like

	cd work/tools/openlane_working_dir/openlane

	dodcker

	./flow.tcl -interactive 

When we enter in the OpenLANE, we have to use flow.tcl because as a name says, it will goes with the flow using the script. And by using interactive switch, we will do step by step process. 
Without interactive switch, it will run complete flow from RTL to GDSII. Now OpenLANE is open and we can see that prompt will change now as shown in following figure.

![image](https://user-images.githubusercontent.com/123365830/216044599-d826f24d-6267-4a08-8774-afef0df6a704.png)

Now we have to input all the packages which required to run the flow.

Command used :

	% package require openlane 0.9

Now, here we are ready to execute the command. Now, if we are going into the design folder in openlane, there are nearly 30-40 designs are already builted. Out of them we can open any of the design. for example, here we are opening the picorv32a.v design. In this design we can see many files are available. i.e., scr, config.tcl, etc. This config.tlc file contains every details about the design. for example, details about enrollment, clock period, clock period port etc.

In the terminal,

	cd work/tools/openlane_working_dir/openlane/designs/picorv32a

	ls

![image](https://user-images.githubusercontent.com/123365830/216044904-b35a8ddc-463d-4f3d-9cfd-32688a1fa8c2.png)

Command used : less config.tcl and then the following figure will be appeared.

![image](https://user-images.githubusercontent.com/123365830/216045029-b3cfceec-744a-4704-b30a-47d95149d918.png)

Here we can see that the time period is set to the 5.00 nsec. But, we see in the openlane sky130_fd_sc_hd folder, the period is set about 24 nsec. so it is not override to the main file. If it override then give first priority to the main folder.

Command used : 

	less sky130A_sky130_fd_sc_hd_config.tcl 
	
![image](https://user-images.githubusercontent.com/123365830/216045200-9cbadee4-9af4-4359-a54b-d6349e105440.png)

In openlane, we are going to run the synthesis, but before synthesis, we have to prepare design setup stage. for that command is " prep -design picorv32a".

Command used : 

%prep –design picorv32a

After preparation is completed, the following figure will be appeared.

![image](https://user-images.githubusercontent.com/123365830/216045409-d134bd1d-15d6-4fc0-bafc-8670cef3cce8.png)

### Review after design preparation and run synthesis

After completing the preparation, in the picorv32a file, the run directory is created.

 Inside the folder, Today's date is created, so in this terictory some folders are available which is required for openlane.
 
 ![image](https://user-images.githubusercontent.com/123365830/216045566-1ac03098-eaa9-4b37-aafd-f65a4cf31d4b.png)

In the temp file, merged.lef file is available which was created in preparation time. If we open this merged.lef file, we get all the wire or layer level and cell level information. To open this file

	cd work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-02_09-25/tmp
	
	less merged.lef
	
![image](https://user-images.githubusercontent.com/123365830/216045729-5dc3a849-7977-45c0-b284-d9d263abad66.png)

![image](https://user-images.githubusercontent.com/123365830/216045783-e7b33e3d-5eaa-4406-bddd-3c2ac2b518a6.png)

While, in the result folder is empty because till we have not run anything and in the report folder all the folders are there about synthesis, placement, floorplanning,cts,routing,magic,lvs.

![image](https://user-images.githubusercontent.com/123365830/216045908-622163af-e985-4a2f-b111-6240aede0c06.png)

Now here also one config.tcl file is available similar like design folder. But this config.tcl file contains all default parameter taken by the run.

![image](https://user-images.githubusercontent.com/123365830/216046002-e813eefb-08d8-40e9-be88-8b83727bc9b9.png)

When we make some changes in the origional configuration and then we run.

For example if we make a change in core utilization in the floorplanning and then we run the floorplanning, at this time in the congig.tcl file, the core utility will change and by cross checking it we can check that the modification is reflected in the exicution or not.

Now, cmds.log file takes all the record of the commands, what we have fab.

![image](https://user-images.githubusercontent.com/123365830/216046223-36d2482d-312e-4060-8232-7eb16113cc0f.png)

Now in the openlane, run the synthesis by using command : run_synthesis

It will take some 3-4 minutes to run the synthesis and finally synthesis will complied and the result will be shown in below.

![image](https://user-images.githubusercontent.com/123365830/216046663-3bd5b972-c7df-495d-acec-0d25fbce344f.png)

From the data of synthesis, total number of counter D_flip-flops is 1613 and the number of cells is 14876.

In the following figure, the number of D_flip-flops is shown.

![image](https://user-images.githubusercontent.com/123365830/216046793-ae1e0b78-bd25-4e06-8c57-90478a49fef2.png)

In the following figure, the number of cells is shown.

![image](https://user-images.githubusercontent.com/123365830/216046883-71c8dfe6-d684-4d48-a4a9-4d3f7f37c951.png)

So, the flop ratio = (number of flip flops)/(number of total cell).And therefore, the flop ratio is 10.84%.

Before run, we saw that the result folder is empty. but now, after running the synthesis, we can see that all the mapping have been done by ABC.

![image](https://user-images.githubusercontent.com/123365830/216047061-3c72400f-fbfa-4df5-9946-81047d4a72f7.png)

And in the report, we can see when the actual synthesis has done. and the actual statistics synthesis report is showing below, which is same as what we have seen before.

![image](https://user-images.githubusercontent.com/123365830/216047111-e00f1b61-e7ce-407e-9841-2c7f0f04052e.png)

# Day 8 Good Floorplanning Vs Bad Floorplanning and Introduction to Library Cells

### Chip floorplanning considerations

### Utilization factor and aspect ratio

#### 1. defining the width and height of core and Die

![image](https://user-images.githubusercontent.com/123365830/216516916-c24c9527-ed02-43f9-acc3-9b4ce4661e0b.png)

Let's begin with netlist( Netlist describes the connectivity of an electronic designs). Considering a netlist with 2 flops and 2 gates.

![image](https://user-images.githubusercontent.com/123365830/216516979-7e4cbc86-23fd-4462-afc2-1f9a619c7de0.png)

Lets giving the height and width of standerd cell is 1 unit. So, the area of standerd cell is 1 square unit. And assuming the same area for the flip flops also. Now lets calculate the area occupied by the netlist on a silicon wafer by arranging them together. The total area occupied by netlist in silicon wafer is 4 square units.

![image](https://user-images.githubusercontent.com/123365830/216517074-7b66da0d-5103-49d1-a2ff-abae8d69c65d.png)

#### what is the core and die?

A 'core' is the section of the chip where the fundamental logic of the design is placed.

A 'Die', which is consist of core, is small semiconductor material specimen on which the fundamental circuits is fabricated.

![image](https://user-images.githubusercontent.com/123365830/216517175-e0bf4a06-86a9-42b9-a45b-6f42c240f851.png)

If we put the 'arranged netlist' in the core, then whole core is occupied by netlist. that means utilization of core is 100%.

![image](https://user-images.githubusercontent.com/123365830/216517231-9e2c5233-b6d0-42dd-b22b-f30d39c24b11.png)

#### Utilization factor

It is defined as, 'the area occupied by netlist' devided by the 'total area of core'. So, in the above case, the utilization factor is 1. Practically, we don't go with 100% uti;ization and utilization factor is about 50%-60% to add other extra cells (like buffer) in the core after netlist is placed.

#### Aspect Ratio
it is defined as (height)/ (width). here in above example the aspect ratio is 1.

### Concept of pre-placed cells

#### 2. Define locations of preplaced cells

To define the preplaced cells, let's take a combinational logic i.e., mux, multiplier, clock devider, etc. and assuming that the output of the circuit is huge and assuming that the circuit has some 100k gates. so let devides in two blocks of 50k gates.

![image](https://user-images.githubusercontent.com/123365830/216517693-9503a509-bbcc-42c8-87d7-cb9b5a394d3c.png)

This both blocks are implimented separatly. Now, extending the input and output pins from the both blocks and let's detached these box. We will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. now we make separate them out.

![image](https://user-images.githubusercontent.com/123365830/216517833-9f7ccb23-7e1c-445b-83d5-f6f6c8a3f384.png)

This blocks are implemented in netlist once and then we can reuse it multiple time. Similarly, there are other modules or IPs also readily available.i.e.,memory, clock gating cell, comparater, mux. these all are part of the top level netlist.They recieve some signals, they perform some functions, they deliver the outputs but the functionality of the cell is implemented only once. That what we called as preplaced cells.

The arrangement of these ip's in a chip is refferd as floorplanning.These IP's have user-defined locations, and hence are placed in chip before automated placement and routing are called "preplacement cells".These cells are place din such fashion that, the placement and routing tool not touch the location of the cell.

![image](https://user-images.githubusercontent.com/123365830/216517894-5f3c7d2d-023f-4833-ace0-1a2c50d481cb.png)

Let consider memory as a preplaced cells as a block 'a', block 'b' and block 'c'. Memory of any device is implemented once and reused multiple times. These preplaced cells are located as per the design bacckground. the location of the cells are never touched.

### De-coupling capacitors

#### 3. Surround pre-placed cells with Decoupling capacitors

Let consider some circuit, which is part of the blocks which were defined above. When some gate (let consider AND gate) switched from 0 to 1 ot 1 to 0, considered amount of the switching current required because of small capacitance is available there. This capacitor should be completely charged to represent logic 1 and completly discharged to represent logic 0. The required amount of the charge is suplied from the Vdd and absorb from the Vss. During supplying the current, wire has some drop of voltage due to resistence and inductunce of the physical wire.

![image](https://user-images.githubusercontent.com/123365830/216518116-c37ff36a-aa04-4a7e-806e-f2a68bbe89e9.png)

Therefore, due to this if ideal logic 1 = 1 volt then here practically it can be less then 1 volt i.e., 0.97 volts (Vdd'). So, for any signal to be considered as Logic '0' and '1' in the NM low and NM high range. It is danger case.

![image](https://user-images.githubusercontent.com/123365830/216518180-5f4100e7-9e8a-46a6-b868-140faee3d6ab.png)

To solve this problem,, we have to put De-coupling capacitor in parallel with the circuit. Every time the circuit switches, it draws current from Cd, whereas, the RL network is used to replacenish the charge into Cd.

![image](https://user-images.githubusercontent.com/123365830/216518219-d2a58a90-8f69-4c37-96f7-9b95731cad65.png)

![image](https://user-images.githubusercontent.com/123365830/216518234-59691c97-4096-460e-941e-461a82e680fb.png)

#### 4. How to do power planning?

Up to here, we have taken care of local communication. Now let consider that local circuitory as a black box and it can be repeat multiple times and power supply is also connected to all of them as shown below.

![image](https://user-images.githubusercontent.com/123365830/216518353-164c51aa-74f1-4361-9c3b-fd7e5b83b583.png)

Now 16 bit bus has to retain the same signal from driver to the load. so it should get the sufficient power from the supply. But at this bus, there is no de-coupling capacitor is available because it is not physible to put capacitor at all over the place. now, power supply is far away from the bus, that is why some drop between them will definalty occurs.

Let consider this 16 bit bus connected to inverter. So, all capacitor are initially charged will get discharged and vice-versa due to inverter.

![image](https://user-images.githubusercontent.com/123365830/216518407-dfa0231e-7fec-452a-94e8-e2f88df2252c.png)

But the problem is occurs due to all capacitor is connected to the single ground. This will cause a bump in 'ground' tap point during discharging.

![image](https://user-images.githubusercontent.com/123365830/216518460-815b6408-5da9-423f-8e1f-71d4ba796aef.png)

Same problem will occurse during the charging time also. at that time lowering of voltage occurse at 'Vdd' tap point.

![image](https://user-images.githubusercontent.com/123365830/216518593-3265e5c1-a1b4-490b-ae85-b48fd452f7ae.png)

The solution of the problem is use multiple power supply. So, every block will take charge from neartest power supply and similarly dump the charge to the nearer ground. this type of power supply is called mesh.

![image](https://user-images.githubusercontent.com/123365830/216518624-3fdf1ea2-81cb-4f4b-a291-32743e4fea6f.png)

And the power planning is shown below,

![image](https://user-images.githubusercontent.com/123365830/216518669-c47939f0-6de5-49a0-b947-ed7c7b5306ab.png)

### Pin placement and Logic floor planning considerations

#### 5. Pin Placement

Lets take below designs for example that needs to implemented.


![image](https://user-images.githubusercontent.com/123365830/216518739-9c89cfc9-cf6b-468f-907c-c8841a92ca3e.png)
Both the sections has different inputs like Din1 and Din2 and operated from different clocks like clock 1 and clock 2. along with that we have preplaced cells as well. So, basically now we have 4 input ports and 3 output ports.

Let's have one more design that needs to be implemented. This types of circuits are very much helpful to understand the timing analysis of inter clocks.Now complete design becomes like given below which has 6 input ports and 5 output ports. it is called the 'Netlist'.

![image](https://user-images.githubusercontent.com/123365830/216518831-2660089f-16e4-401e-bad8-e212bac59292.png)

Let's put this netlist in the core which we have designed before and let's try to fill this empty area between core and die with the pin information. The frontend team who decides the netlist input and output and the backend team who done the pin placements. So according to the pin placements, we have to locate the preplaced blocks nearer to the inputs of the preplaced blocks.

![image](https://user-images.githubusercontent.com/123365830/216518880-4d15cb0b-11ca-41ad-9d62-9d248556be27.png)

Here one thing that we noticed is that clock-in and clock-out pins are bigger in size as compared to input and output pins. Reason behind this is that, input clocks are conntinuously provides the signal to the every elements of the chip and output clock should out the signal as fast as possible. So, we need least resistance path for the clocks inputs and clocks outputs. So, bigger the size, lower the resistance.

One more thing is need to take care about is that, this pin placement area is blocked for routing and cell placements. Therefore, we nned to do logical cell placement blockage. This blockage is shoown in above image in between pins. So, floor plan is ready for Placement and Routing step.

## Steps to run floorplan using OpenLANE

Before run the floorplanning, we required some switches for the floorplanning. We can get from the configuration from openlane.

![image](https://user-images.githubusercontent.com/123365830/216519687-c2bac752-7942-4dd4-b09c-1238739d2095.png)

Here we can see that the core utilization ratio is 50% (bydefault) and aspect ratio is 1 (bydefault). Similarly other information is also given. But it is not neccessory to take these values. we need to change these value as per the given requirments also.

Here FP_PDN files are set the power distribution network. These switches are set in the floorplane stage bydefault in OpenLANE.

![image](https://user-images.githubusercontent.com/123365830/216519873-748e9d23-ecf9-4a85-80bd-286c0b795ab9.png)

Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance. In the OpenLANE lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

Now we see, with this settings how floorplan run.

Reviewing floorplan files and steps to view floorplan.

In the run folder, we can see the connfig.tcl file. this file contains all the configuration that are taken by the flow. If we open the config.tcl file, then we can see that which are the parameters are accepted in the current flow.

Commands used:

	$ cd work/tools/openlane_woriking_directory/openlane/designs/picorv32a/runs/02-02.../
	$ less config.tcl
	
![image](https://user-images.githubusercontent.com/123365830/216520701-1c513920-3216-4d38-8831-15408f33b41f.png)

Here we can see that, the core utilization is 35%, aspect ratio is 1 and core margin is taken as 0. While in default the core utilization is 50%. This is the issue. because this design is override the system. but it is the taken from PDK varient.tcl file. So priority vise it is true.

To watch how floorplane looks, we have to go in the results. In the result, one def( design exchange formate) file is available. If we open this file, we can see all information about die area (0 0) (660685 671405), unit distance in micron (1000). it means 1 micron means 1000 databased units. So 660685 and 671405 are databased units. and if we devide this by 1000 then we can get the dimensions of chips in micrometer.

Commands used :

	$ cd work/tools/openlane_woriking_directory/openlane/designs/picorv32a/runs/02-02.../results

	$ less picorv32afloorplan.def
	
![image](https://user-images.githubusercontent.com/123365830/216522503-f20a914c-1469-47db-8a32-57690121d4ac.png)

So, the width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer.

To see the actual layout after the flow, we have to open the magic file by adding the command,

	$ magic -T /home/hsu_mon_maung/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 	picorv32a.floorplan.def
	
And then after pressing the enter, Magic file will open. here we can see the layout.

![image](https://user-images.githubusercontent.com/123365830/216522872-7c5e5950-1ccf-44ea-9f9e-aefcb144b032.png)

### Reviewing floorplan layot with magic.

In the layout we can see that, input output pins are at equal distance.

![image](https://user-images.githubusercontent.com/123365830/216522976-0d7db1a7-b784-4143-8e5d-19decde66542.png)

After selecting (To select object, first click on the object and then press 's' from keyboard. the object will hight lited. to zoom in the object, click on the object and then press 'z' and for zoom out press 'sft+z') one input pin. 

![image](https://user-images.githubusercontent.com/123365830/216523169-e2ee346b-c276-44e7-bc4a-cabb26b59b34.png)

If we want to check the location or to know at on which layer it is available, we have to open tkcon window and type "what". it will shows all the details about that perticular pin.

![image](https://user-images.githubusercontent.com/123365830/216523115-11babade-1bd3-4d2e-9c3f-f4d83fa2e483.png)

![image](https://user-images.githubusercontent.com/123365830/216523228-8e978ff9-609a-425f-a575-a75db3db1c35.png)

So, it show that the pin is in the metal 3.similarly doing for the vertical pins, we find that this pin is at metal 2.

![image](https://user-images.githubusercontent.com/123365830/216523321-7ff8653e-0f7a-411c-ac85-0698d192b68a.png)

Along with the side rows,the Decap cells are arranged at the border of the side rows.

![image](https://user-images.githubusercontent.com/123365830/216523657-bf6ae6df-dc8c-4d52-9da0-c117c1f5ef80.png)

Another cells also placed here, which is a tap cells. These cells are meant to avoide the latch-up problems in the CMOS devices. It connect N-well to the Vdd and substrate to the Ground. these tap cells are placed at diagonally equal distance.

![image](https://user-images.githubusercontent.com/123365830/216523719-a9f22067-e36c-4216-967d-aa0c195d576b.png)

In the floorplane, standerd cells are not placed but here standerd cells are available in the left side of the floorplan. we can see few boxes are there.

![image](https://user-images.githubusercontent.com/123365830/216523762-ddec05d5-ba09-41ed-8245-a420e786a699.png)

Here we can see that first standerd cells is for buffer 1. similarly other cells are for buffer 2, AND gate etc.

### Library building and Placement

#### Netlist binding and initial place design

#### 1.bind netlist with physical cells

Taking netlist as what we taken before,

![image](https://user-images.githubusercontent.com/123365830/216523992-c2111a39-c507-40b5-9f81-ac50290b31f5.png)

Here, we can see that every gate or flip-flops have a shape to understand the functionality of the element. But practically, this cells are square or rectangular boxes which has internally some logic to perform. So, here we are taking all the elements from netlist and giving them a perfact height and width with perticular dimention. These all cells together are called 'self'. And this self are stored in the lybrary. Library have all the innformation about all the blocks, like height, width , time delay, conditional innformation, etc. library also have a option for the similar cells (with same functionality) like this with different height and width. According to our space available at floorplanning we can choose out of them.

![image](https://user-images.githubusercontent.com/123365830/216524021-3985ddd9-108d-462e-b0f2-0738c4d1a3b9.png)

After giving size and shape to each and every box, next step is to take the boxes or element from library and placed in the floorplan. This is called placements of the cells.According to the design of the netlist, we have to put physical blocks in the floorplan which we have design before.Put all the blocks according to the input and output of that perticular blocks.

![image](https://user-images.githubusercontent.com/123365830/216524069-78f8ad83-ab4e-49d2-8627-f53a8cbca987.png)

Up to here we have done stage one and stage two placement. Now we will going for stage 3 and 4. here we have to place FF1 of stage 3 nearer to the Din3 and FF2 of stage 3 nearer to the Dout3. But Din3 and Dout3 are at somme distance from eachother. same thing is there for FF1 and FF2 of stage 4. Let's we placed these all element in such manner that all elements are closed to it's input and output pins.

![image](https://user-images.githubusercontent.com/123365830/216524124-2d8af8cd-50af-41fc-a7b6-32b1ce965952.png)

But, the distance of FF1 of Stage 4 and Din4 is still far them others. By optimizing the placement, we can solve this problem.

### Optimize placement using estimated wire lenght and capacitance

#### 2. Optimize Placement

As we seen that the distance from Din2 to FF1 of stage 2 is higher. so if we connect the wire between them then resistance and capacitance of the wire comes in to the picture. and due to this the signal integrity can not maintain.

To maintain the integrity of the signal out from Din2 to FF1, we have to put some repeaters like buffers on between Din2 and FF1. But it will cause of loss of area.

In the stage 1, there is no need of any repeater to transmit the signal. But in stage 2, due to high distance, the lenth of wire is high and signal is not transmitted in perticular range. so we required repeater.

![image](https://user-images.githubusercontent.com/123365830/216524249-9a34f371-828c-403d-8962-ee484165baf9.png)

#### Final Optimization

Similar as stage 2, in Stage 3 also we required the buffer between gate 2 and FF2.

![image](https://user-images.githubusercontent.com/123365830/216524320-b7a0b84b-5007-4180-a0cf-1b604f5f519a.png)

Now we have to check that, what we have done is correct or not. For that we need to do Timing analysis by considering the ideal clocks and according to the data of analysis, we will understand that, the placement is correct or not.

### Need for libraries and characterization.

#### Library charactorization and modelling

In whole IC design, we have to go through synthesis, floor/power planning, placement, routing , STA. In all this steps one thing remain common, which is "Gates or Cells". That is where the library charactorization becomes very important.

### Congestion aware placement using RePLAce

Right now we are not constrain about timing, but constrain about the congestion. so, we are making the congrstion is less.

The placement is donne in two stages. Global and detailed. In global placement, legalization is not happened but after detailed placement legalization will be done. When we run the placement, first Global placement is happens. main objective of glibal placement is to reducing the length of wires.

Now opening the Magic file to see actual view of standerd cells placement.And the actual view in the magic file is given below,

![image](https://user-images.githubusercontent.com/123365830/216524764-90ee2418-5d0f-49a9-b733-d77f7ac8b77a.png)

If we zooom into this, we find the buffers, gates, flip flops in this.

![image](https://user-images.githubusercontent.com/123365830/216524834-e345f43e-4ed3-4a9c-8705-59d9768d239c.png)

### Cell design and characterization flows

#### Inputs for cell design flow

#### Cell design flow

As we know that standerd cells are placed in the library. And in the library many other cells are available which have same functionality but the size is different. As size is different the parameters like hVt, Ivt also different for each standerd cells. If we take one of the standerd cells called inverter, it has their own design flow by this it can be understandable to EDA tool.

The cell design flow is devided into three part.

* Inputs

* Design steps

* Outputs

![image](https://user-images.githubusercontent.com/123365830/216525066-30edff94-a99a-4768-8965-09e51dd585fe.png)

#### 1. Inputs

Inputs required for cell design is PDKs, DRC and LVS rules SPICE models, library and user defined specs.

### Circuit design steps

#### 2. Design Steps

Steps are circuit design, layout design, characterization

#### 3. Outputs

The typical output what we get from the circuit design is CDL(circuit description language) file,GDSII,LEF,extracted spice netlist(.cir).

### Layout design steps

* Implement Function

![image](https://user-images.githubusercontent.com/123365830/216525450-edb1bc25-2214-4c71-a9a5-ce7981142a64.png)

* Derive the NMOS and PMOS network graph

![image](https://user-images.githubusercontent.com/123365830/216525530-8c35a37a-84e4-4512-8736-d88609b802bc.png)

* Obtain the Euler's path

![image](https://user-images.githubusercontent.com/123365830/216525579-c8bb1d63-5724-4d14-bfc1-aa014e3018da.png)

* Stick Diagram

![image](https://user-images.githubusercontent.com/123365830/216525645-084d68e2-cf7d-40c6-add3-ffe3e4420d0d.png)

* Convert stick diagram into proper layout

![image](https://user-images.githubusercontent.com/123365830/216525713-d21cca40-c16f-4fcf-af29-12da727ed8d3.png)

After layout design, we have to ecxtract the layout and characterize it. In characterization step, we can get the information about Timing, Noice,power.libs and function.

### Characterization Flow

As of now, from the circuit design and layout design, we have final layout of buffer cell. where two buffers are connected in series with each other.

![image](https://user-images.githubusercontent.com/123365830/216525805-67bc1eb7-8102-41c3-84d4-0629a7cf2cb0.png)

Now steps of flow is:

* Read the model file

* read the extracted spice netlist

* reconize the behavior of buffer

* Read the subcircuit of the inverter

* Ateched the neccessory power source

* Apply the stimulus

* Provide the necessory of output capacitance

* Provide the necessory simulatin command

This all steps we have to give in "GUNA" software. and this software will give the timing, noise, power.libs and functions.

### General Timing characterization parameters

#### Timing threshold defination

![image](https://user-images.githubusercontent.com/123365830/216526097-36d43812-0462-4394-ae51-6748c7bde5c0.png)

Let we take the waveform from the output of the first buffer and it will be input of the second buffer and taking output of the second buffer also.

![image](https://user-images.githubusercontent.com/123365830/216526142-694b09e2-72cb-4d29-bc34-958ef011cffb.png)

![image](https://user-images.githubusercontent.com/123365830/216526169-8ffee570-42d4-4160-a066-a7ddd008f755.png)

* slew_low_rise_thr

Here low means nearer to the ground, and rise tresold means we want to measer the slope of the increasing graph. Typical value of slew low rise thr is around 20-30%.

![image](https://user-images.githubusercontent.com/123365830/216526265-7aa558b0-d160-48cc-bea0-e32fd91499c9.png)

* slew_high_rise_thr

Same as above, high means nearer to high value.

![image](https://user-images.githubusercontent.com/123365830/216526333-7f11a413-6ba5-46a9-8d56-6749f5ca2a0b.png)

Whenever we want to calculate the slew, take the point at 20% from the low and take the point at 20% from the high. according to these point, take the time data and the time difference between them will helps to calculate the slew.

* slew_low_fall_thr

![image](https://user-images.githubusercontent.com/123365830/216526383-52a84f20-f014-4c55-ac30-4d0ad6809b00.png)

NOw, taking the waveform of input stimulus which is input of the first buffer and with that taking output of the first buffer.

Similar as a slew, thresolds are for delay also available. for that same as slew, we have to take some rise and fall points from the waveforms. this tresolds are almost 50%.

* in_rise_thr

![image](https://user-images.githubusercontent.com/123365830/216526449-26c1e87d-26a7-4d83-a166-93744a798839.png)

* in_fall_thr

![image](https://user-images.githubusercontent.com/123365830/216526494-30af86e5-3c29-452b-b4bc-19afe51e489e.png)

* out_rise_thr

![image](https://user-images.githubusercontent.com/123365830/216526538-09112650-8917-4024-9009-681b59640b77.png)

* out_fall_thr

![image](https://user-images.githubusercontent.com/123365830/216526598-8d0b10ce-4d22-4f8e-97fd-6a26c37297f9.png)

So, according to rise and fall theresold we can find the rise delay and fall delay of the buffer.

![image](https://user-images.githubusercontent.com/123365830/216526642-1590e965-f8ff-491a-9711-12a8f4a21791.png)

### Propogation delay and Transition time

#### Propogation Delay

Let's take the same setup for understand the propogation delay. Time delay = Time(out_thr)-time(in_thr).Let's take waveform on which we can apply above formula.

![image](https://user-images.githubusercontent.com/123365830/216526764-b29d7c3f-807d-4798-be9a-b69a5bba1d5b.png)

In any case if thresold point move at the top, at that time we get negative delay because output comes before input. so reason behind the negative delay is the poor choice of the tresold points. which is not acceptable. so, choosing the thresold point is very important.

![image](https://user-images.githubusercontent.com/123365830/216526803-83e5e9e5-e63f-4985-aedb-69d946f4ba2c.png)

Taking another example where the wire delay is very high because of high distance between two elements. so, here by choosing correct thresold point then also we get the negative delay.

![image](https://user-images.githubusercontent.com/123365830/216526862-737fceea-862b-4bff-9c50-85ebd7373757.png)

#### Transition time

transition time = time(slew_high_rise_thr)- time(slew_low_rise_thr)

or

transition time = time(slew_high_fall_thr)- time(slew_low_fall_thr)

Let's take waveform for understand the slew calculation.

![image](https://user-images.githubusercontent.com/123365830/216526969-b9d5e265-e519-4354-9bca-ed722f2e4fd4.png)

# Day 9 -Design library cells using Magic Layout and ngspice characterization

## Labs for CMOS inverter ngspice simulations

## SPICE deck creation for CMOS innverter

### IO placer revison

Till now, we have done floor planning and run placement also. But if we want to change the floorplanning, for example, in our floor planning, pins are at equal distance and if we want to change it then we can also make it by "Set" command.

	% set ::env(FP_IO_MODE) 2
	
![image](https://user-images.githubusercontent.com/123365830/216665081-d645d384-e74b-4562-83d6-31f0d2e6fd87.png)

For that first we have to check the swithes in the configuration and from that we have to take the syntax "env(FP_IO_MODE) 1". and make it to the "env(FP_IO_MODE) 2". then again run the floorplanning.

Then check the changes in the pins location through magic -T.

![image](https://user-images.githubusercontent.com/123365830/216665177-c51795d3-a29f-4b7a-ab0d-2ed310278b25.png)

So, here we can see that there are no pins in the upper half side. all pins are in the lower half of the core.

### SPICE deck creation for CMOS inverter

#### VTC- SPICE simulations

Before entering into the simulation, we have to creat the spice deck. The spice deck is nothing but netlist. so, we have to creat the spice deck for CMOS.

* Component connectivity

![image](https://user-images.githubusercontent.com/123365830/216665573-e7f0b1c2-c9e5-4373-af98-59ad979516f1.png)

* Define the components values

![image](https://user-images.githubusercontent.com/123365830/216665651-5f96fc3d-78be-45df-a7ca-6f29b1eb2fd1.png)

* Identyfy the nodes

![image](https://user-images.githubusercontent.com/123365830/216665714-4418a344-ab4f-4bf3-b37c-049c731975ef.png)

* Name 'Nodes'

![image](https://user-images.githubusercontent.com/123365830/216665765-49fc87db-25e6-4d06-a598-b0387ae7da33.png)

Now, let's strat the writing the SPICE deck

![image](https://user-images.githubusercontent.com/123365830/216665863-d57cb279-cfde-4ff4-85b7-764c7f7e1880.png)

Here, in the syntex, It is like Name of the mosfet, drain , gate, substrait , source. so, the meaning of the syntex is that, name of the mosfet is M1, Drain is connected to OUT node, Gate is connected to IN node, Substrait is connected to Vdd and the Source is connected to Vdd node. PMOS says the type of mosfet and the Width and lenth of channel is defined. similarly, For M2, syntex were written.

### SPICE simulation lab for CMOS

Tile we discribe the connectivity information about CMOS inverter only. Now we have to discribe connectivity information about other components also like source, capacitor etc. so, lets look into the other components.

First we discribe the load capacitor and then about the Vdd and Vin.

![image](https://user-images.githubusercontent.com/123365830/216665993-06136d98-6e2d-45cc-97ba-ef311528829b.png)

Now, we have to give simulation command. which is about swiping the Vin from 0 to 2.5 with the steps of 0.05. Because we want Vout while changing the Vin.

![image](https://user-images.githubusercontent.com/123365830/216822105-4f0b99d2-523e-4b47-943d-a07dc85538eb.png)

![image](https://user-images.githubusercontent.com/123365830/216822117-bb2036b2-f577-4128-916c-7c5597aea3e1.png)

The final step is to discribe the Model file.Model file contains all the details about PMOS and NMOS. from this file only we get the information about PMOS and NMOS.

![image](https://user-images.githubusercontent.com/123365830/216822127-b28fd3e8-4444-489a-87df-2aa0f5955fdc.png)

So, the total program is given below,

![image](https://user-images.githubusercontent.com/123365830/216822143-7cd21237-1666-4c1d-9c55-56e494e0ef50.png)

Now, doing the simulation and get the graph like this,

![image](https://user-images.githubusercontent.com/123365830/216822155-a9fe3df2-a5f4-48d0-9844-b4bdaefdaada.png)

Now, doing other simulation in which we change the PMOS width to 3 times of NMOS width. and after diong the simulation, we get the graph like this,

![image](https://user-images.githubusercontent.com/123365830/216822206-fdfcf4f7-863a-4abd-8608-493dead1ff8f.png)

The difference between this two graph is that in the second graph the transfer charactoristic is lies in the ecxact middle of the graph where in the first graph it is lies left from the middle of the graph.

### Switching Thresold Vm

These both model of different width has their own application. By comparing this both waveform, we can see that the shape of the both waveform is same irrespective of the voltage level.

This thing tell us that when Vin is at low, output is at high and when Vin is at high, the output is at low. so the charactoristic is maintain at all kind of CMOS with different size of NMOS or PMOS. That is why CMOS logic is very widely used in the design of the gates.

Switching thresold, Vm (the point at which the device switches the level) is the one of the parameter that defined the robustness of the Inverter. Switching thresold is a point at which Vin=Vout.

![image](https://user-images.githubusercontent.com/123365830/216822252-8a6b01b5-7980-40c5-b826-8161565aacce.png)

In this figure, we can see that at Vm~0.9v, Vin=Vout. This point is very critical point for the CMOS because at this point there is chance that both PMOS and NMOS are turned on. If both are turned on then there is chances of leakage current(Means current flow direcly from power to ground).

By comparing this both the graph we can understang the concept of switching thresold voltage.

![image](https://user-images.githubusercontent.com/123365830/216822265-cb901de9-a50b-439c-8f69-95c0e41181f2.png)

![image](https://user-images.githubusercontent.com/123365830/216822273-d947989a-fc1f-4842-b57b-3b4938ad2a36.png)

### Lab steps to git clone vsdstdcelldesign

To get the clone, copy the clone address from reporetery and paste in openlane terminal after the command "git clone". this will create the folder called "vsdstdcelldesign" in openlane directory.

	$ cd work/tools/openlane_working_dir/openlane
	
	$ git clone https://github.com/nickson-jose/vsdstdcelldesign.git
	
![image](https://user-images.githubusercontent.com/123365830/216822377-223f2134-d77c-40ee-8b50-9bd23d464855.png)

now, if we open the openlane directory, we find the vsdstdcelldesing folder in the openlane directory.

![image](https://user-images.githubusercontent.com/123365830/216822456-4e773e19-90ca-4add-b246-b8019182d834.png)

Now if we goes in the vsdstdcelldesign folder and open it, we get the .mag file,libs file etc.

![image](https://user-images.githubusercontent.com/123365830/216822575-0f65ddfc-f70d-49e9-90e8-9baabf14c2f4.png)

Now, let's open the .mag file and see that which layers are used to build the inverter. But before opening the mag file, we need tech file. so we will copy this file from this given below address. And do copy by "cp" command to the location which is given below,

![image](https://user-images.githubusercontent.com/123365830/216822610-1fa7f2f3-0b82-4e6a-a186-dfd5e4a6ac6f.png)

Now, we can see that this file is copied in the vsdstdcelldesign folder.

![image](https://user-images.githubusercontent.com/123365830/216822662-1a36d27c-d226-408e-bd3e-1a334db6a4dc.png)

Now, here to see the layout in magic, we don't need to write the whole address because we copy the tech file here.

Now, appying the magic comand like this,

	$cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesigns

	$magic -T sky130A.tech sky130_inv.mag &
	
Now, we can see the layout of CMOS inverter in the magic like this,

![image](https://user-images.githubusercontent.com/123365830/216822842-eee61873-1885-4dc4-8eab-fa307ed16e06.png)

### Inception of layout CMOS fabrication process

### create active region

#### 1) selecting a substrate

we select P-type silicon substrate with high resistivity(5~50 ohms) with moderate dopping and orientation is (100).

#### 2) creating active region for transister

First, we create the isolation layer by depositing the Sio2 layer (~40nm) on the substrate.

![image](https://user-images.githubusercontent.com/123365830/216822933-934e5e33-e8ca-4fef-ba99-766728447f13.png)

Now, we are depisiting the Si3N4 layer (~80 nm) on the Sio2 layer.

![image](https://user-images.githubusercontent.com/123365830/216822952-40943344-ab1f-486b-8df6-5b888d9a00be.png)

Now we do patterning by using depositing photoresist and using Mask 1 through UV light.

![image](https://user-images.githubusercontent.com/123365830/216822977-e018d47c-f991-4b96-b922-7b69f5709b09.png)

Now, first we remove the mask and doing etching of Si3N4 layer on the exposed area.

![image](https://user-images.githubusercontent.com/123365830/216823004-710be873-6fb5-4576-aad0-9305fd523e45.png)

Now, next step is to remove photoresist by chamical reaction, because now to Si3N4 layer itslef behaves like good protecting layer for Sio2 layer. now, if we do LOCOS (local oxidation of silicon) process, the exposed sio2 part will gown and bird break also form. This grown sio2 will provide the perfect isolation between two PMOS and NMOS.

![image](https://user-images.githubusercontent.com/123365830/216823029-7a8d7c89-d6f6-4413-92f7-63e0765ecbd8.png)

Next step is to etchout the Si3N4 layer by hot phosphoric acid.

![image](https://user-images.githubusercontent.com/123365830/216823064-7756a0c5-3e73-4a56-a349-d1e1b2517a4f.png)

### Formation of N-well and P-well

#### 3) N-well and P-well formation

we can not form P-well and N-well at a same time. we have to protect a region while forming one of the region by photoresist. And then using mask 2 and UV light, we will do patterning of photoresist to form P-well.

![image](https://user-images.githubusercontent.com/123365830/216823122-0247280e-0488-4296-84a2-625cc40ace81.png)

Now, the area where we want to form the P-well is exposed. now we remove the mask and by applying the ion implantaton method (~200kev)to form P-well using Boron. But still it is P implant. After performing the high temparature anneling, it will become P-well.

![image](https://user-images.githubusercontent.com/123365830/216823165-9b86d6ed-f47e-4887-94aa-09e70177ce9b.png)

We wiil do a similar process to form N-well by using mask 3 and using Phosphorus ions.

![image](https://user-images.githubusercontent.com/123365830/216823188-1e6d08fe-f8d2-4eba-b864-2deac1f9b726.png)

till now depth of wells are not define. so, by putting into the high temparature furnace (drive-in diffusion), we will define the depth of wells.

![image](https://user-images.githubusercontent.com/123365830/216823227-4c8b9cad-b042-4278-830f-4214e785b364.png)

### Formation of gate terminal

#### 4)Gate formation

Gate terminal is the most important terminal of the PMOS and NMOS because from the gate terminal only we can control the thresold voltage. doping concentration and oxide capacitance will control the thresold voltage.

so, first we are maintain the doping concentration here. for that we use mask 4 and again doing the ion implantation of boron ion at lower energy (~60kev).

![image](https://user-images.githubusercontent.com/123365830/216823248-d6e1fa19-46a6-4be5-9fb7-18826fe8f21b.png)

same process we will repeat for N-well also by using mask 5 and Arsenic ion.

![image](https://user-images.githubusercontent.com/123365830/216823266-b19e6e6a-b957-4764-9744-7c14dd66d156.png)

Next step is that we have to fix the oxide layer. but before that we have to remove the oxide layer because this layer is got dammeged because of the privious processes. so,first we remove the layer using HF solution and again re-grown the high quality oxide layer with same thickness.

The final step is the deposition of polysilicon layer over oxide layer with more impurities for low resistance gate terminal.Then etched out this polysilicon layer by using mask 6 and photoresist.

![image](https://user-images.githubusercontent.com/123365830/216823291-8665bd0e-cd7a-4509-94de-42159889094a.png)

After etching, remove the photoresist and gate terminal looks like,

![image](https://user-images.githubusercontent.com/123365830/216823305-992ba464-38f9-4807-aa2e-22e1dddf9400.png)

### Lightly doped drain (LDD) formation

#### 5) LDD formation

Here, we actully want P+,P-,N doping profile in the PMOS and N+,N-,P doping profile for NMOS. Reason for that is

* Hot electron effect

* short channel effect

For the formation of LDD, we again do ion implantation in P-well by using mask 7 and here we use phosphoros as a ion for light doping.

![image](https://user-images.githubusercontent.com/123365830/216823360-98dbc2b7-4e61-4b51-9e7b-6da2942f5369.png)

Same process we will repeat for N-well. there we use mask 8 and BOron Ion.

![image](https://user-images.githubusercontent.com/123365830/216823378-6d50adbd-a0c3-4231-bf25-2c33a2e6aecf.png)

Now, by creating the spacers, we can protect the actual structre remain constant of P-implantt and N-implant. For that we deposite a thick Sio2 or Si3N4 layer over the gate tereminal.

![image](https://user-images.githubusercontent.com/123365830/216823406-b097eff3-36dc-47f9-a86a-883764ed72ca.png)

Now, we do Plasma anisotropic etching. By that side-wall spacers are formed.

![image](https://user-images.githubusercontent.com/123365830/216823425-b07a918a-4733-4c5f-9003-4b176caeb9b6.png)

### Source and drain formation

#### 6)source-drain formation

Next step is deposite the very thin screen oxide layer to avoid the effect of channeling.

![image](https://user-images.githubusercontent.com/123365830/216823475-d4e383b1-1d14-477f-a927-82189ba40ba9.png)

Now to form the drain and source, again we do the ion implantation of arsenic at 75kev to create the N+ implant by using mask 9 in the P-well to form PMOS.

Same process we will repeat for NMOS by using the mask 10 and boron ion in the N-well at 50kev to creat P- implant.

![image](https://user-images.githubusercontent.com/123365830/216823495-d3fce123-eb8f-47b2-b03b-da2372ef0b78.png)

Now we put this Half made CMOS into the high temparature (1000 degree)anneling. So P+ implant and N+ implant now become the source and drain.

![image](https://user-images.githubusercontent.com/123365830/216823517-16cfbb1b-3b86-4fe2-a68d-60404de7ef85.png)

### Local interconnect formation

#### 7)steps tp form contacts and local interconnects

First step is remove the thin screen oxide layer by etching. Then deposite the titanium (Ti) using sputtering. here Ti is used because Ti has very low resistivity.

![image](https://user-images.githubusercontent.com/123365830/216823545-1d156c3c-5690-4592-8613-2289265de57c.png)

Next step is to create the reaction between Ti layer and source, gate, drain of CMOS. For that wafer is heated at about 650-700 degree temparature in N2 ambient for about 60 seconds. and after reaction, we can see the titanium siliside over the wafer. One more reaction is heppend there between Ti and N. and it results the TIN which is used for local communication.

![image](https://user-images.githubusercontent.com/123365830/216823570-89f8c23c-83ad-4727-a5db-260001a8eada.png)

Now by using mask 11 and photoresist, we will etched out the TIN and make perticular contacts. TIN is etched out by using RCA cleaning.

![image](https://user-images.githubusercontent.com/123365830/216823587-1da092ca-337b-4211-b7f7-3002ea4bde12.png)

Now, local interconnects are formed after etching and removing the photoresist.

![image](https://user-images.githubusercontent.com/123365830/216823604-77a049bb-a8fd-4d84-85a9-3c4987480156.png)

### Higher level metal formation

#### 8)Higher level metal formation

These steps are very semilar like previous steps. First thing that we are noticing is that the surface is non planner. it is not good to use this type of non planner serface for matel interconnects because of the problems regarding the metal disconinuty. so, we have to plannerize the surface by depositing the thick layer of sio2 with some impurity to make less resistive layer. and then we used CMP (chemical mechanical polishing) technique to plannerise the surface.

![image](https://user-images.githubusercontent.com/123365830/216823633-8604888e-aa69-4631-9885-a8cdfd63d25c.png)

Now using mask 12 and photorsist we etched the sio2 layer to diposite the metal in it.

![image](https://user-images.githubusercontent.com/123365830/216823641-b556371c-ba4f-4268-b01c-05271786607c.png)

Now remove the photoresist and seposite the thin later of TIN (~10nm) over the wafer. Because TiN is act as very good adession layer for sio2 and also act as a barrier between bottom layer and top layer of metal interconnects.

![image](https://user-images.githubusercontent.com/123365830/216823656-2fc2a5f5-9d1f-492b-afbe-ecf1ad24c220.png)

Next step is to deposite the blanket tungsten (W) layer over the wafer. and then do the CMP here to plannerize the surface.

![image](https://user-images.githubusercontent.com/123365830/216823681-36434fff-22ca-4fbb-9a1d-822efb22dce0.png)

This W is act as a contact holes and this holes needs to connect to the Higher metal layer. so we will deposite the Al (aluminium) layer.

![image](https://user-images.githubusercontent.com/123365830/216823692-2e7333d6-9bef-4b1e-b6f9-ce4f288ac7c4.png)

Then by using the mask 13 and photoresist, we etched the W layer out to form the contact at perticular place by Plasma etching.

![image](https://user-images.githubusercontent.com/123365830/216823719-db19f786-db94-4a11-95b8-4ebfa1ee7777.png)

This is our first level of metal interconnets. now we again do the same process as above to deposite the second level of metal interconnect by using mask 14 for etched out the sio2 and using mask 15 for etched out Al leyer.

![image](https://user-images.githubusercontent.com/123365830/216823728-1eefe0cb-ae6f-4ce7-a1c7-c595505bba4d.png)

The upper layer of Al is bit thicker as compared to lower layer of Al.Now, again deposite the layer of sio2 or si3N4 to protect the chip.

![image](https://user-images.githubusercontent.com/123365830/216823744-2ed1fb3c-78df-4ad3-8049-c2a3a8edd910.png)

And finally our CMOS is looks like this after the fabrication.

![image](https://user-images.githubusercontent.com/123365830/216823765-8a8eed52-e59f-43ec-ae36-e349d732c487.png)

### Lab introduction to Sky130 basic layer layout and LEF using inverter

![image](https://user-images.githubusercontent.com/123365830/216823786-358a59a3-c7a0-444b-8af9-f503beb00959.png)

In sky130, every color is showing the different layer. here the firsst layer is for local interconnect shown by blue_perpel color, then second layer is metal 1 which is showm by light perple color, and the metal 2 is shown by pink color. N-well is showm by solide das line. green is N-diffusion region. and red is for polysilicon gate. similarly the brown color is for P-diffusion.

In tckon window, we can see that the selected area is NMOS and similarly we can chech PMOS also. and that is how we can check that the CMOS is working or not.

![image](https://user-images.githubusercontent.com/123365830/216823812-73f352af-91dc-4158-8820-f6874737b17d.png)

semilarly we check for the output terminal also.(by double pressing "S" to select the entire thing at output Y).

![image](https://user-images.githubusercontent.com/123365830/216823827-431aa4cb-6350-4848-b260-e97aa5b60dae.png)

so, we can see that "Y" is attached to locali in cell def sky130_inv.

we can check the source of the PMOS is connected to the ground or not. and similarly we can check it for NMOS also.

### Lab steps to create std cell layout and extract spice netlist

To extract the file from here, we have to write the command in tckon window. and the comand is "extract all".

![image](https://user-images.githubusercontent.com/123365830/216823885-93b20537-c6d1-436e-9634-c6719e6646c3.png)

Now let's go to this location from the terminal. it is exctracted.

![image](https://user-images.githubusercontent.com/123365830/216823941-583581b4-ed68-4deb-a7bd-04888b386d3f.png)

we will use this .ext file to create the spice file to be use with our ngspice tool. for that we have apply the comand "ext2spice cthresh 0 rthresh 0". this will not create anything new. now again we have to type "ext2spice" comand in tckon window.

![image](https://user-images.githubusercontent.com/123365830/216823962-db31d30a-cb3c-4e89-b12b-3012d90b598f.png)

let's see what inside the spice file by "vim sky130_inv.spice".

![image](https://user-images.githubusercontent.com/123365830/216824015-b72837e6-caac-4683-b643-fabcec9142be.png)

### Sky130 Tech File labs

### Lab steps to create final SPICE dexk using sky130 tech.

![image](https://user-images.githubusercontent.com/123365830/216824050-199ccbf0-4653-408a-9683-9d3472f96e3c.png)

here, we can see the all details about the connectivity of the NMOS and PMOS and about the power supply also.

X0 is NMOS and X1 is PMOS and both's connectivity is shown as GATE DRAIN SUBSTATE SOURCE.

But here the scale is 10000 um. but in Magic simulation, it is 0.01.

![image](https://user-images.githubusercontent.com/123365830/216824068-017a1004-46b9-40d6-b01c-59015b2170a1.png)

SO, we are going to change the dimension here in the terminal. so any measurement will be in this scale of 0.01u. i.e., width=37*0.01u.

Now we have to include the PMOS and NMOS lib files. it is inside the libs folder in the vsdstdcellsdesign folder.

![image](https://user-images.githubusercontent.com/123365830/216824090-705b49a6-2dcf-4c6c-94b5-8c1ad53fae80.png)

so, now we include this file in the terminal by ".include ./libs/pshort.lib" and ".include ./libs/nshort.lib" comand.

And then set the supply voltage "VDD" to 3.3v by "VDD VPWR 0 3.3V" comand. and similarly set the value of VSS also.

Now, we need to specify the input files. by Va A VGND PULSE(0V 3.3V 0 0.1ns 2ns 4ns).

Also add the comand for the analysis like, ".tran 1n 20n", ".control" , "run",".endc",".end".

![image](https://user-images.githubusercontent.com/123365830/216824107-d216fbaf-68a1-477e-9718-7f1ed72bf836.png)

after running this file we get output of ngspice like this,

![image](https://user-images.githubusercontent.com/123365830/216824125-6049713a-abbb-412e-b3ec-08ee610c4397.png)

Now, ploting the graph here by comand, "plot y vs time a".

![image](https://user-images.githubusercontent.com/123365830/216824144-6f6ad28c-12e0-4f6f-b57f-8a89122e89dd.png)

### Lab steps to characterize inverter using sky130 model file

Here, we have to find value of 4 parameters.

* rise time

it is time taken to the output waveform to 20% value to 80% value.

![image](https://user-images.githubusercontent.com/123365830/216824174-91734c10-dd8b-46e4-a71c-28aff473c538.png)

so, rise time= (2.19857-2.18002)e-09 = 0.0185 nsec.

* propogation delay

it is the time difference between the 50% of input and 50% of the output.

![image](https://user-images.githubusercontent.com/123365830/216824215-7e31dd0f-3732-4552-9c76-5c0a93061e5c.png)

so,propagation delay = (2.18045-2.15013)e-09 = 0.03 nsec.

# DAY 10 Pre-layout timing analysis and importance of good clock tree

## Timing modelling using delay tables

### Lab steps to convert grid info to track info

Till now we have done synthesis, floorplaning, placement and how to extract the spice out of it, done charecterization of it. till now, for placement and routing, we doesn't required any information about input/output port,logic path, power, ground.

Now the concept of 'lef' file will comes into the picture. it contains all the information which we discuss earlier. so our next objective is to extract the '.lef' file out of the '.mag' file. and next step is that extracted file could be placed into the picorv32a flow.

you need to folow certain guideline while making standerd cells.the guidelines are

* The input and output port must lie on the intersection of the verticle and horizontal tracks

* The width of the satnderd cell should be odd multiple of the track pitch and the height should be odd multiple of track verticle pitch
Now oprning the track file from the pdk/sky130/libs.tech /openlane/sky130_fd_sc_hd/track.info. where we get the info like this,

![image](https://user-images.githubusercontent.com/123365830/216833260-dcf74933-830e-4805-89b9-a4406a8bfdec.png)

so, the track is basically nothing but it is used during the routing stage.Rout will be go over the tracks. tracks are basically trases of matel layers.i.e., metal 1, matel 2, etc.

PNR is a automated. so we need to specified, where from we want routs to go. this specification is given by tracks. here we can see that each of the tracks are placed at (0.23 0.46)um horizontaly and (0.17 0.34)um vertically for li1, metal 1, metal 2 layer.

In layout, we can see that the ports are on the li1 layer. so we need to insure that the ports are on the intersection of the tracks or not. For that we have to cinvert the grid into the tracks. for that we have to first into the tracks file and the open the tckon window and type the "help grid" comand.

![image](https://user-images.githubusercontent.com/123365830/216833285-a75860b9-2276-4425-9531-7acd37a2e479.png)

Then again write comand according to the track file.

![image](https://user-images.githubusercontent.com/123365830/216833312-2b5e24fd-9d23-4e9e-9993-fd2d783d3578.png)

Let's see the changes in the layout.

![image](https://user-images.githubusercontent.com/123365830/216833319-9c3afba6-1af3-46b7-8474-9ba125085393.png)

Here we can see that, as per the guideline the ports are placed at the intersection of the tracks.

now, between the boundaries, there is 3 boxes are coverd. so our second requirment also satisfied here.

### Lab steps to convert magic layout to std cell LEF

here already the port name and the port definationa is seted, if not seted the we have to set the definanation and the name of the port.

As it parameters are set, we are ready to extract the 'LEF' file from the "mag" file. but before the extraction, let give the name to the cell by using tckon window.

Now we can see this file in the vsdstdcellsdesign folder.

Now, we open this file in the magic by using comand "magic -T sky130A.tech sky130_vsdinv.mag &".

Now to extract the lef file we have to write the comand in the tckon window "lef write". so it will create a lef file and we can check it in the vsdstdcellsdesign folder.

![image](https://user-images.githubusercontent.com/123365830/216833362-f387c4ef-26c8-4db8-963d-2539a7c9c234.png)

Now, lef file is created and now next step is plug this lef file in picorv32a. before that we move our files to src folder where all the design files are available at one location.

for that we are copiying this file in the src folder by 'cp' comand.

### Introduction to timing libs and steps to include new cell synthesis

The basic idea is that we have to include our custom cell into openlane flow. and the first stage in the openlane is the synthesis.

here, also we required library. so we copiying the library to the src folder.

Before we do anything, we have to modified our congig.tcl file. so opening this file by "vim" comand and modifiying it.

Now, start the new terminal and open the openlane by docker, make flow interactive and then add the package and then prep design with the privios run by the comand " prep -design pecorv32a -tag [last running time i.e.27-01_17-53] -overwrite".

Now comes the deciding part. we have to see that the synthesis run and its maps our custom vsd inveter into this flow. so, run the synthesis.

### Introduction to delay tables

Power Aware CTS

If we make enable pin at logic '1' in the AND gate, the clock will propogatee to the AND gate. similarly, if we make enable pin at logic '0' in the OR gate, here also clock propogate to the OR gate.

Similarly if we make enable pin at logic 'o' in the AND gate, gate will block the clock and same this will happend with the OR gate if we make enable pin at logic '1'.

The advantage of this scenario is that, during this time period of the blocking the clocks, we can save lots of power in the clock tree. now the question is that how can we use this scenario in the clock tree.

let say we have a clocktree like this given below,

![image](https://user-images.githubusercontent.com/123365830/216833462-5028abbf-de42-4606-b08c-edb907e778e9.png)

Here we spitted the load of the 4 FF into the 2 buffers and the load of the 2 buffers is given to the level 1 buffer. here assumptions are,

* Assume c1=c2=c3=c4=25fF

* Assume Cbuf1=Cbuf2=30fF

* Total Cap at node 'A'=> 60fF

* Total Cap at node 'B'=> 50fF

* Total Cap at node 'C'=> 50fF

We have done some observations here,

* 2 levels of buffering

* At every level,each node driving same load

* Identical buffer at same level

so, here capacitance at the every node of the clock tree is not the same. it is varying. Now load is varying then input transition is also verying because the output load at the level 1 buffer is the input of the other buffers of level 2. so, we have variety of the delays. To capture it, we have delay tables.

How delay tables are prepared?
To prepare the delay table, the perticukar element is taken out of the circuit and saparetly verying the input transition and output load and according to the variation, we will charactorize the delay of the element and make the delay table frpm it.

![image](https://user-images.githubusercontent.com/123365830/216833547-f86031a6-d763-4777-a5ff-9f917c3e36ac.png)

### Delay table usage part 1

Let's looks into the sample examples and making the table for Cbuf'1' and Cbuf'2',

![image](https://user-images.githubusercontent.com/123365830/216833584-8f315743-d51a-43da-97f4-e270c9cb36bf.png)

let's take practical example on the circuit. we take 40psec as input transition on the level 1 buffer and as per assumption load is around 60fF. and delay is comes between x9 and x10. lets take x9' as the delay of the buffer of level 1.

### Delay table usage part 2

Next step is to calculate the delay of the buffers of level 2. And after that we can find the letancy at the 4 clock end points.

now input transition is common for both the buffers. now assuming that the transition is around the 60psec and load at both the buffers is 50fF. so it will give the delay of y15.

The total delay from input to the output is= x9' + y15.(here we are ignoring the delay of the wires). that means the skew at the any output point is zero.

If load is not same at the every nodes, the skew will not be the zero.

### Lab steps to configure synthesis settings to fix slack and include vsdinv

After synthesis, we observed that the slack is nagative here. wns(worst negative slack)= -24.89 and tns(total negative slack)= -759.

![image](https://user-images.githubusercontent.com/123365830/216833634-5b95b14c-c4ea-4ff4-9cf2-228848a64780.png)

let's do some modification here. for that opening the READme file from the /openlane/configuration/ less READme.md

Now lets try to make balance between area and the delay of the synthesis by changing the stratagy. comand for checking the current strategy is "echo $::env(SYNTH_STRATEGY)", and comand for changing the stategy is "set ::env(SYMTH_STRATEGY) 1". by doing this area will increase the little but but timing will improve.

Then checking the synth_bufferung and synth_sizing. if any one them is off then make it on by set the value of it by 1.

Till here we not get slack 0. to make slack 0, we ahve to write comand "set ::env(SYMTH_STRATEGY) DELAY 0"

After running synthesis we will get improved timing.

![image](https://user-images.githubusercontent.com/123365830/216894935-3a71525b-86ed-4bf7-ab81-e04f1fb40a1b.png)

Next command for run is :

	set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

	add_lefs -src $lefs

Then again run the synthesis.

#### Timing analysis with ideal clocks using openSTA

### Setup timing analysis and introduction to flip-flop setup time

### Timing analysis (with ideal clock)

we start with taking the ideal clock and we will do timing analysis for the ideal clock first.

Let's start the setup analysis with the ideal clock(single clock). specifications of the clock is

* clock frequency =1 GHz

* clock period =1 nsec

Let's take lainch Flop and Capture flop with clock. here clock tree is not built yet. so it is ideal scenario. here we have to do analysis between '0' and 'T'. with that assume that the delay of logic is 'θ'.

![image](https://user-images.githubusercontent.com/123365830/216895207-c06afbe5-bc7c-430d-8ca4-5ae1bfe4bc0c.png)

Setup timing analysis says that θ<T. this condition should be neccessory for the the comninational logic work.

Now let's introduce the practical scenario here. Opening the capture flop and it has two mux inside it.

![image](https://user-images.githubusercontent.com/123365830/216895260-3c478111-216e-4892-9836-0b7d76ce2a55.png)

The way flop work, it will shown by the timing graph like this,

![image](https://user-images.githubusercontent.com/123365830/216895307-84c2e067-a3a1-4ac1-9c9b-f081a895256a.png)

So, here mux 1 and mux 2 both have their own delay. these delay will restrict the combination delay to the requirment.

Hence finite time 's' required before clk edge for 'D' to reach Qm.

So, we can write that the internal delay of the MUX1 = set up time(S).

So, now θ<T becomes θ<(T-S).

### Introduction to clock jitter and uncertainty

Let's bring one more practical scenario here. clock is taking from the some clock source or PLL. So, because of some delay from the practical source of clock or PLL, clock pulse will not comes exacly at t=0 or at t=T. that in built variation of the clock is called jitter.

![image](https://user-images.githubusercontent.com/123365830/216895467-10bfbc37-c1b0-4012-a298-b0ca7f7c8fd5.png)

lets consider this uncertantity time(US) in consideration. So, now equation becomes like, θ<(T-S-US). Now assuming that 'S'=0.01ns and 'US'=0.09ns. by taking that, lets identify the timing path for our existing scenario. in our circuit stage 1 and stage 3 logic path has single clock.

NOw, what we have to do is identify the combinational path delay for the given both logics.

![image](https://user-images.githubusercontent.com/123365830/216895540-1132a631-9adc-4e95-9a76-f24285d00abe.png)

![image](https://user-images.githubusercontent.com/123365830/216895556-24c89106-ff49-45c6-bfb3-76e3dcb7ff5e.png)

### Lab steps to configure OpenSTA for post-synth timing analysis.

When we do CTS, CTS is a stage where, we add clock buffers along with clockpath and build the clock tree. so, actually we are changing the netlist. Along the running CTS, actually the netlist file also created. so, after running the CTS, we will see the new Verilog file here.

Now, we see what is in the my_base.sdc file.

![image](https://user-images.githubusercontent.com/123365830/216895665-b79ff41b-e98e-4a82-95ed-3d669ac1397a.png)

Here, we can see the capacitor load and clock period and clock port etc.

Now, to reduce the fanout we use the command is : "set ::env(SYNTH_MAX_FANOUT) 4" and then run the synthesis.

but here also slack doesn't reduce.

Now next step is run floorplan, place IO, do global placement or detail placement and genrate pdn file the run the cts by following comands.

	inut_floorplan

	place_io

	global_placement_or

	detailed_placement

	tap_decap_or

	detailed_placement

After running the floorplaning and done the global placement we get positive slack.

![image](https://user-images.githubusercontent.com/123365830/216895791-a9881cf4-e2ed-4c31-bb49-0f4118360f3e.png)

Then check the file which is created. Go to the placements folder under results and then invoke the magic tool and load the def file. The command is:magic -T /home/hsu-mon-maung/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

![image](https://user-images.githubusercontent.com/123365830/216896207-80e3a2a5-6c79-40a6-bd01-fa89551c6385.png)

#### Clock tree synthesis TritonCTS and signal integrity

### Clock tree routing and buffering uisng H-Tree algorithm

What is clock tree synthesis?

As shown in below, figure, let's connect clk1 to FF1 & FF2 of stage 1 and FF1 of stage 3 and FF2 of stage 4 with out any rules.








































































































	
















































