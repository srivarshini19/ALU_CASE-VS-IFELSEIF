# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

 <img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/b5f95c0d-1fd6-4c3c-9a35-11eb9c86cba3" />

#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
```
module alu_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;		//AND Operation
3'b001:y=a|b;		//OR Operation
3'b010:y=~(a&b);	//NAND Operation
3'b011:y=~(a|b);	//NOR Operation
3'b100:y=a^b;    	//XOR Operation
3'b101:y=a+b;		//Addition
3'b110:y=a-b;		//Subtraction
3'b111:y=a*b;		//Multiply 
default:y=32'bx;
endcase
end 
endmodule

```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_case_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_case dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00110001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#100 $finish; 
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using If Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;			//AND Operation 
else if (f==3'b001)
y=a|b;	         	//OR Operation
else if (f==3'b010)
y=~(a&b);        	//NAND Operation
else if (f==3'b011)
y=~(a|b);		//NOR Operation
else if (f==3'b100)
y=a^b;			//XOR Operation
else if (f==3'b101)
y=a+b;        		//Addition
 else if (f==3'b110)
y=a-b;			//Subtraction 
else if (f==3'b111)
y=a*b;			//Multiply 
else
y=32'bx; 
end 
endmodule
```

#### Test Bench :
```
module alu_ifelseif_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00110001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end initial
#100 $finish; 
endmodule
```

Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below

<img width="1920" height="1080" alt="Screenshot (170)" src="https://github.com/user-attachments/assets/fccd3099-2b03-40dd-a23c-d470b2fb66db" />


#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.

<img width="1920" height="1080" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/c6500dd8-5b14-4051-a4de-a531d03a446c" />


#### Fig 3: Nclaunch Window

#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

<img width="1920" height="1080" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/3e0dea5a-a809-4eea-9189-cc74b387a7fb" />


#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.

<img width="1920" height="1080" alt="Screenshot (171)" src="https://github.com/user-attachments/assets/eb8de055-b2e5-4bc1-8346-fa1cfdddd44f" />


#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

<img width="1920" height="1080" alt="Screenshot (175)" src="https://github.com/user-attachments/assets/61888245-81f3-4ba6-9e56-808b0aec3f21" />


#### Fig 6: Design Browser window for simulation

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (167)" src="https://github.com/user-attachments/assets/98169307-2925-4577-98b3-9c61c85313fa" />

#### ALU IFELSE:
<img width="1920" height="1080" alt="Screenshot (167)" src="https://github.com/user-attachments/assets/98169307-2925-4577-98b3-9c61c85313fa" />

#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### ALU CASE:

<img width="1920" height="1080" alt="Screenshot (177)" src="https://github.com/user-attachments/assets/7c4fd4b6-7152-42cb-9b4b-b416d8911f57" />

#### ALU IFELSEIF:

<img width="1920" height="1080" alt="Screenshot (182)" src="https://github.com/user-attachments/assets/e842bd6b-e6c2-4d4f-a1d5-2deb03c26f74" />


#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (213)" src="https://github.com/user-attachments/assets/6a999a70-92ff-4984-aa6c-f64fe5668720" />

#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (211)" src="https://github.com/user-attachments/assets/ff2b534c-affb-4b2b-b222-6c069d21dda0" />


#### Fig 9: Area report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (214)" src="https://github.com/user-attachments/assets/8e586238-48c2-453a-9570-99c9a7bc6437" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (210)" src="https://github.com/user-attachments/assets/a1ee917e-1751-489e-9198-2bbebabb9769" />


#### Fig 10: Power Report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (215)" src="https://github.com/user-attachments/assets/d99a91f1-6c10-4dc4-be8f-ca9f127a56b1" />



#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (212)" src="https://github.com/user-attachments/assets/60c30829-7063-4158-8202-f186a9ac039c" />



#### Fig 11: Timing Report of case and ifelseif construct

<img width="955" height="631" alt="image" src="https://github.com/user-attachments/assets/b8c2aada-ed46-44ba-92b2-4b8dff4f3e4f" />

#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors. Both implementations were functionally correct and synthesizable. Synthesis using Cadence Genus generated gate-level netlists along with area, timing, and power reports.
A comparative analysis revealed that the case-statement-based ALU resulted in slightly lower area and better timing performance, while the if–elseif-based ALU exhibited higher logic complexity and marginally increased delay due to sequential decision evaluation. Both designs, however, produced identical functional outputs.
