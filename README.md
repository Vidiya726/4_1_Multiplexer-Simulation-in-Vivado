# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
//Gate-Level Modelling - Skeleton
`timescale 1ns / 1ps

module mux(I,S,Y);
input [3:0]I;
input [1:0]S;
output Y;
wire [3:0]w;
and g1 (w[0],I[0],~S[1],~S[0]);
and g2 (w[1],I[1],~S[1],S[0]);
and g3 (w[2],I[2],S[1],~S[0]);
and g4 (w[3],I[3],S[1],S[0]);
or g5 (Y,w[0],w[1],w[2],w[3]);
endmodule

```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
//Testbench Skeleton
`timescale 1ns / 1ps

module mux_4_1_tb;
reg [3:0]I;
reg[1:0]S;
wire Y;
mux uut(I,S,Y);
initial
begin
I=4'b1101;
S=2'b00;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b01;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b10;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b11;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
$finish;
end
endmodule
```
## Simulated Output Gate Level Modelling

<img width="1919" height="1079" alt="Screenshot 2025-08-26 215610" src="https://github.com/user-attachments/assets/861e4568-1475-4c57-95a8-0440ae8b28a9" />


---
### 4:1 MUX Data flow Modelling
```verilog
// Dataflow Modelling - Skeleton
`timescale 1ns / 1ps

module mux41(I,S,Y);
input [3:0]I;
input[1:0]S;
output Y;
wire [4:1]W;
assign W[1]= I[0] & (~S[1]) & (~S[0]);
assign W[2]= I[0] & (~S[1]) & S[0];
assign W[3]= I[0] & S[1] & (~S[0]);
assign W[4]= I[0] & S[1] & S[0];
assign Y= W[1] | W[2] | W[3] | W[4];
endmodule

```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps

module mux4_1_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
mux41 uut(I,S,Y);
initial
begin
I=4'B0110;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end 
endmodule

```
## Simulated Output Dataflow Modelling


<img width="1919" height="1079" alt="Screenshot 2025-08-26 213811" src="https://github.com/user-attachments/assets/71ec469f-1860-4106-b6cf-83c6735cd8a7" />


---
### 4:1 MUX Behavioral Implementation
```verilog
// Behavioral Implementation - Skeleton
`timescale 1ns / 1ps

module MUX_4_1( I,S,Y);
input [3:0]I;
input [1:0]S;
output reg Y;
always @(I,S)
    begin
        case(S)
        2'b00:Y=I[0];
        2'b01:Y=I[1];
        2'b10:Y=I[2];
        2'b11:Y=I[3];
        endcase
    end
endmodule

```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps

module mux_4_1_tb;
reg [3:0]I;
reg[1:0]S;
wire Y;
MUX_4_1 uut(I,S,Y);
initial
begin
I=4'b1001;
S=2'b00;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b01;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b10;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
S=2'b11;
#10;
$display("Selection is %b %b , Output : %b",S[1],S[0],Y);
$finish;
end
endmodule

```
## Simulated Output Behavioral Modelling

<img width="1919" height="1079" alt="Screenshot 2025-08-26 215059" src="https://github.com/user-attachments/assets/31981bb1-be31-4b74-bf73-6fdd59c0204b" />



### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
`timescale 1ns / 1ps

module mux41(a,b,s,z);
input a,b,s;
output z;
wire w1,w2;
and g1(w1,a,~s);
and 2(w2,b,s);
or g3(z,w1,w2);
endmodule

module MUX_41(i,s,y);
input [3:0]i;
input [1:0]s;
output y;
wiге [2:1]w;
MUX41 M1(w[1],i[0],i[1],s[1]);
MJX41 M2(w[2],i[2],i[3]),s[1]);
MUX41 M3(у,w[1],w[2], s[0]);
endmodule


```
### Testbench Implementation
```verilog
`timescale 1ns / 1ps

module MUX_41_tb; 
reg [3:0]i; 
reg [1:0]s; 
wire y; 
MUX_41 uut(i,s,y); 
initial 
begin 
i=4'B1011; 
s=2'b00; 
#10 
$display("Selection is %b %b , output : %b ", s[1],s[0],y); 
s=2'b01; 
#10 
$display("Selection is %b %b , output : %b ", s[1],s[0],y); 
s=2'b10; 
#10 
$display("Selection is %b %b , output : %b ", s[1],s[0],y); 
s=2'b11; 
#10 
$display("Selection is %b %b , output : %b ", s[1],s[0],y); 
$finish;
end
endmodule
```
## Simulated Output Structural Modelling

<img width="1919" height="1078" alt="Screenshot 2025-08-29 135533" src="https://github.com/user-attachments/assets/09b64c58-7f85-405f-8c42-bad0ce285dc2" />

---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

