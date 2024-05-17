EXP-2

DATE:


SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

## AIM: 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

## APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

## PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.

STEP:2  Select the device family, device, package and speed. 

STEP:3  Select new source in the New Project and select Verilog Module as the Source type.

STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.

STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.

STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.

STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.

STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained
. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.

STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

**LOGIC DIAGRAM**

## ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)

### Verilog code :
```
module encoder(y,a);
input [7:0]y;
output [2:0]a;
or g1(a[0],y[1],y[3],y[5],y[7]);
or g2(a[1],y[2],y[3],y[6],y[7]);
or g3(a[2],y[4],y[5],y[6],y[7]);
endmodule
```

### Output :
![image](https://github.com/SanthoshK265/VLSI-LAB-EXP-2/assets/143738585/fc28cef1-bbfb-43b2-a173-74ef292d5206)

## DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)

### Verilog code :
```
module decoder(a,y);
input [2:0]a;
output [7:0]y;
and g4(y[0],~a[2],~a[1],~a[0]);
and g5(y[1],~a[2],~a[1],a[0]);
and g6(y[2],~a[2],a[1],~a[0]);
and g7(y[3],~a[2],a[1],a[0]);
and g8(y[4],a[2],~a[1],~a[0]);
and g9(y[5],a[2],~a[1],a[0]);
and g10(y[6],a[2],a[1],~a[0]);
and g11(y[7],a[2],a[1],a[0]);
endmodule
```

### Output :
![image](https://github.com/SanthoshK265/VLSI-LAB-EXP-2/assets/143738585/0e410e06-5849-4d19-9f40-59835f2f6bec)

## MULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)

### Verilog code :
```
module multiplexer(d,s,y);
input [7:0]d;
input [2:0]s;
output y;
wire w0,w1,w2;
wire x0,x1,x2,x3,x4,x5,x6,x7;
not g1(w0,s[0]);
not g2(w1,s[1]);
not g3(w2,s[2]);
and g4(x0,d[0],w0,w1,w2);
and g5(x1,d[1],w0,w1,s[2]);
and g6(x2,d[2],w0,s[1],w2);
and g7(x3,d[3],w0,s[1],s[2]);
and g8(x4,d[4],s[0],w1,w2);
and g9(x5,d[5],s[0],w1,s[2]);
and g10(x6,d[6],s[0],s[1],w2);
and g11(x7,d[7],s[0],s[1],s[2]);
or g12(y,x0,x1,x2,x3,x4,x5,x6,x7);
endmodule
```

### Output :
![image](https://github.com/SanthoshK265/VLSI-LAB-EXP-2/assets/143738585/eb125e53-3a67-4dd4-a423-cbc042e02af0)

## DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)

### Verilog code :
```
module demux(d,s,y);
input d;
input [2:0]s;
output [7:0]y;
wire w0,w1,w2;
not g1(w0,s[0]);
not g2(w1,s[1]);
not g3(w2,s[2]);
and g4(y[0],d,w0,w1,w2);
and g5(y[1],d,s[0],w1,w2);
and g6(y[2],d,w0,s[1],w2);
and g7(y[3],d,s[0],s[1],w2);
and g8(y[4],d,w0,w1,s[2]);
and g9(y[5],d,s[0],w1,s[2]);
and g10(y[6],d,w0,s[1],s[2]);
and g11(y[7],d,s[0],s[1],s[2]);
endmodule
```

### Output :
![image](https://github.com/SanthoshK265/VLSI-LAB-EXP-2/assets/143738585/120bddbf-92bd-4b11-aff4-c78dd588d6c7)

## MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)

### Verilog code :
```

module comparator(a,b,gr,lt,eq);
input [1:0]a,b;
output reg gr,lt,eq;
always @(*)
begin
if (a>b)
begin
gr=1'b1;
lt=1'b0;
eq=1'b0;
end
else if(a<b)
begin
gr=1'b0;
lt=1'b1;
eq=1'b0;
end
else
begin
gr=1'b0;
lt=1'b0;
eq=1'b1;
end
end
endmodule
```

### Output :
![image](https://github.com/SanthoshK265/VLSI-LAB-EXP-2/assets/143738585/05ef4834-85c7-46fd-8edd-0120132ab8c5)

## RESULT
Thus the Encoder, Decoder, Multiplexer, Demultiplexer and Magnitude Comparator are Synthesis and stimulated Successfully Using Xilinx ISE.
