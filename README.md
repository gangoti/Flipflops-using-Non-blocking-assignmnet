# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```timescale 1ns/1ps
module S_FFN(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
    if(rst==1)
        q<=0;
    else if(s==0 && r==0)
        q<=q;
    else if(s==0 && r==1)
        q<=1'b0;                                                                                        
    else if(s==1 && r==0)
        q<=1'b1;
    else 
        q<=1'bx; 
        
end       
endmodule
```
### SR Flip-Flop Test bench 
```
module tb_S_FFN;
reg s,r,clk,rst;
wire q;
S_FFN uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial 
begin
clk=0;s=0;r=0;rst=1;
#10 rst=0;
#10 s=0;r=0;
#10 s=0;r=1;
#10 s=1;r=0;
#10 s=1;r=1;
#10 s=0;r=0;
#20 $finish;
end 
endmodule




```
#### SIMULATION OUTPUT
<img width="1448" height="802" alt="image" src="https://github.com/user-attachments/assets/2dbf0bba-f852-4781-a9c0-d3683ebbcce6" />




## JK Flip-Flop (Non Blocking)
```

module JK_FFN(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk)
begin
   if(rst==1)
      q<=1'b0;
   else if(j==0&&k==0)
      q<=q;
   else if(j==0&&k==1)
      q<=1'b0;
   else if(j==1&&k==0)
      q<=1'b1;
   else
      q<=~q;
end
endmodule

```
##  JK Flip-Flop Test bench 
```
module tb_JK_FFN;
reg j,k,clk,rst;
wire q;
JK_FFN uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
  clk=0;j=0;k=0;rst=1;
  #10 rst=0;
  #10 j=0;k=0;
  #10 j=0;k=1;
  #10 j=1;k=0;
  #10 j=1;k=1;
  #10 j=0;k=0;
  #20 $finish;
end 
endmodule

```
#### SIMULATION OUTPUT

<img width="1455" height="802" alt="image" src="https://github.com/user-attachments/assets/765e2949-6578-4045-949d-42fc6d8fe5cd" />

### D Flip-Flop (Non Blocking)
```
`timescale 1ns/1ps
module D_FF (clk,reset,D,Q);
input clk, reset, D;
output reg Q;
always @(posedge clk) 
begin
   if (reset)
     Q <= 0;
   else
     Q <= D;
end
endmodule

```
### D Flip-Flop Test bench 
```

module D_FF_tb;
    reg clk, reset, D;
    wire Q;
    D_FF uut (clk,reset,D,Q);
    always #5 clk = ~clk;
    initial 
    begin
       clk=0;
       D=0;
       reset=1;#10;
       reset=0;
       D=0;#10;
       D=1;
    end
endmodule

```

#### SIMULATION OUTPUT

<img width="1437" height="793" alt="image" src="https://github.com/user-attachments/assets/202fe00d-3344-4b00-bb07-757c7a5a32b4" />


### T Flip-Flop (Non Blocking)
```
`timescale 1ns / 1ps
module T_FFN(clk,rst,T,Q);
input clk,rst,T;
output reg Q;
always @ (posedge clk)
begin
  if (rst==1)
     Q<=0;
  else if (T==0)
     Q<=Q;
  else
     Q<=~Q;
end
endmodule

```
### T Flip-Flop Test bench 
```
`timescale 1ns / 1ps
module tb_T_FFN;
  reg clk,rst,T;
  wire Q;
  T_FFN uut(clk,rst,T,Q);
  always #5 clk=~clk;
  initial
  begin
    clk=0;
    T=0;
    rst=1;#10;
    rst=0;
    T=0; #10;
    T=1;
  end
endmodule


```

#### SIMULATION OUTPUT

<img width="1446" height="795" alt="image" src="https://github.com/user-attachments/assets/9c33485c-f280-4fda-9981-c75dd43600e8" />

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
