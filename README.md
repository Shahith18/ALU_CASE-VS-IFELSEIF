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
module alu_32bit_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;	//AND Operation
3'b001:y=a|b;	//OR Operation
3'b010:y=~(a&b);//NAND Operation
3'b011:y=~(a|b);//NOR Operation
3'b100:y=a+b;	//Addition
3'b101:y=a-b;	//Subtraction
3'b110:y=a*b;   //Multiply
3'b111:y=a^b;	// XOR Operation
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
module alu_32bit_tb_case; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_32bit_case DUT(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00100001; 
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
#150 $finish; 
endmodule
```
Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using ifelseif Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;	               //AND Operation 
else if (f==3'b001)
y=a|b;	              //OR Operation
else if (f==3'b010)
y=~(a&b);	      //NAND Operation
else if (f==3'b011)
y=~(a|b);	      //NOR Operation
else if (f==3'b100)
y=~(a^b);	      //XOR Operation
 else if (f==3'b101)
y=a+b;                //Addition
 else if (f==3'b110)
y=a-b;	              //Subtraction 
else if (f==3'b111)
y=a*b;	              //Multiply 
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
begin a=32'h00000000; b=32'h00100001; 
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
<img width="1920" height="1080" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/e4de0b45-30dd-4ae3-8e0c-2fc6099c423b" />



#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.


Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.
<img width="1920" height="1080" alt="Screenshot (46)" src="https://github.com/user-attachments/assets/9b00d8f6-06ba-4701-9322-4b18807cb2cf" />

<img width="1920" height="1080" alt="Screenshot (47)" src="https://github.com/user-attachments/assets/fe29137e-6250-4af7-b20c-4b645f6a3ad5" />


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

#### case
<img width="1920" height="1080" alt="Screenshot (48)" src="https://github.com/user-attachments/assets/e434054d-a9ec-420f-b22e-ff9301ee3d55" />
#### ifelseif
<img width="1920" height="1080" alt="Screenshot (56)" src="https://github.com/user-attachments/assets/150432d9-caa3-41cd-8ea0-0958bf1a076f" />



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
#### case
<img width="1920" height="1080" alt="Screenshot (49)" src="https://github.com/user-attachments/assets/2fa46ac5-e1a0-47ce-ad21-95f9e739f75e" />
#### ifelseif
<img width="1920" height="1080" alt="Screenshot (57)" src="https://github.com/user-attachments/assets/902121d4-f201-4e5d-831c-6447821912d0" />


#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options
#### case
<img width="1920" height="1080" alt="Screenshot (50)" src="https://github.com/user-attachments/assets/bc5bef00-b3c0-4543-ad57-948915065629" />
#### ifelseif

<img width="1920" height="1080" alt="Screenshot (58)" src="https://github.com/user-attachments/assets/28550a2d-f550-4037-a8ac-fbb14bc3b535" />

#### Fig 6: Design Browser window for simulation
#### case

<img width="1920" height="1080" alt="Screenshot (51)" src="https://github.com/user-attachments/assets/e47a8958-5dfd-4661-b904-90f02fcdde82" />

####  ifelseif

<img width="1920" height="1080" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/a8178fd2-de69-4f26-a909-4838c374754a" />



#### Fig 7: Simulation Waveform Window
Synthesis requires three files as follows,

◦ Liberty Files (.lib)
◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
#### For case statement
<img width="1920" height="1080" alt="Screenshot (88)" src="https://github.com/user-attachments/assets/3d33b4f8-e08a-4931-af3e-a36f78ac9272" />


#### For ifelseif statement
<img width="1920" height="1080" alt="Screenshot (89)" src="https://github.com/user-attachments/assets/93a35592-e0a0-4fa3-b285-8d0fa3f6b53c" />



##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct
#### case
<img width="1920" height="1080" alt="Screenshot (83)" src="https://github.com/user-attachments/assets/c22c5c57-dcf9-4837-a7e3-054b603834c7" />


#### ifelseif

<img width="1920" height="1080" alt="Screenshot (87)" src="https://github.com/user-attachments/assets/191f18a5-a3ce-498a-9779-28fe1561ef55" />


#### Fig 9: Area report of case and ifelseif construct
#### case
<img width="1920" height="1080" alt="Screenshot (84)" src="https://github.com/user-attachments/assets/3126182b-8e06-47f9-84ac-0555285e0820" />

#### ifelsif
<img width="1920" height="1080" alt="Screenshot (90)" src="https://github.com/user-attachments/assets/c460c30e-6df4-4c0d-8e61-34bbf77fff5a" />


#### Fig 10: Power Report of case and ifelseif construct

#### case
<img width="1920" height="1080" alt="Screenshot (85)" src="https://github.com/user-attachments/assets/1397c54d-7a6d-49ca-8cbb-e60709dff8c2" />

#### ifelseif
<img width="1920" height="1080" alt="Screenshot (91)" src="https://github.com/user-attachments/assets/eb2cb753-48e6-47ee-8be0-d50c235bb129" />


#### Fig 11: Timing Report of case and ifelseif construct

#### case
<img width="1920" height="1080" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/707e40cc-a972-49ad-bb78-57294aeb48a7" />

#### ifelseif
<img width="1920" height="1080" alt="Screenshot (92)" src="https://github.com/user-attachments/assets/b3b61065-85f0-462c-97a8-d8a574e9bf99" />


#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

![WhatsApp Image 2025-10-17 at 17 47 13_d6496759](https://github.com/user-attachments/assets/b71e3b5b-98f5-452a-8d86-d1592c71c5a8)


## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors. Both implementations were functionally correct and synthesizable. Synthesis using Cadence Genus generated gate-level netlists along with area, timing, and power reports.
A comparative analysis revealed that the case-statement-based ALU resulted in slightly lower area and better timing performance, while the if–elseif-based ALU exhibited higher logic complexity and marginally increased delay due to sequential decision evaluation. Both designs, however, produced identical functional outputs.
