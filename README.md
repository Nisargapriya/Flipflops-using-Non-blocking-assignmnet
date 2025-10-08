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
```verilog
module sr_ff (
    input wire S, R, clk,
    output reg Q
);
    always @(posedge clk) begin
        // Use non-blocking assignments for sequential logic
        case ({S, R})
            2'b00: Q <= Q;
            2'b01: Q <= 1'b0;
            2'b10: Q <= 1'b1;
            2'b11: Q <= 1'bx;
        endcase
    end
endmodule

```
### SR Flip-Flop Test bench 
```verilog
module sr_ff_tb;
    reg S, R, clk;
    wire Q;
    sr_ff uut (
        .S(S), 
        .R(R), 
        .clk(clk), 
        .Q(Q)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end
    initial begin
        S = 0; R = 0;
        #10;
        S = 0; R = 1;
        #10;
        S = 0; R = 0;
        #10;
        S = 1; R = 0;
        #10;
        S = 0; R = 0;
        #10;
        S = 1; R = 1;
        #10;
        $finish;
    end
endmodule


```
#### SIMULATION OUTPUT

------- paste the output here -------
---

### JK Flip-Flop (Non Blocking)
```verilog
module jk_ff (
    input wire J, K, clk,
    output reg Q
);
    always @(posedge clk) begin



endmodule
```
### JK Flip-Flop Test bench 
```verilog



```
#### SIMULATION OUTPUT

------- paste the output here -------
---
### D Flip-Flop (Non Blocking)
```verilog
module d_ff (
    input wire d,clk,
    output reg Q
);
    always @(posedge clk) begin



endmodule
```
### D Flip-Flop Test bench 
```verilog



```

#### SIMULATION OUTPUT

------- paste the output here -------
---
### T Flip-Flop (Non Blocking)
```verilog
module d_ff (
    input wire d,clk,
    output reg Q
);
    always @(posedge clk) begin



endmodule
```
### T Flip-Flop Test bench 
```verilog



```

#### SIMULATION OUTPUT

------- paste the output here -------

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
