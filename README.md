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
<img width="703" height="337" alt="image" src="https://github.com/user-attachments/assets/442fc9df-e7ad-465c-8e30-5a46ca3c0ac6" />

### JK Flip-Flop (Non Blocking)
```verilog
module jk_ff (
    input wire J, K, clk,
    output reg Q
);
    initial Q = 1'b0;

    always @(posedge clk) begin
        case ({J, K})
            2'b00: Q <= Q;      
            2'b01: Q <= 1'b0;   
            2'b10: Q <= 1'b1;   
            2'b11: Q <= ~Q;     
        endcase
    end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
module jk_ff_tb;
    reg J, K, clk;
    wire Q;

    jk_ff uut (
        .J(J), 
        .K(K), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        J = 1; K = 0; 
        #10;
        J = 0; K = 0;
        #10;
        J = 0; K = 1; 
        #10;
        J = 1; K = 1;
        #10;
        J = 1; K = 1;
        #10;
        $finish;
    end
endmodule

```
#### SIMULATION OUTPUT
<img width="705" height="383" alt="image" src="https://github.com/user-attachments/assets/911ed51f-37a4-42d9-9450-9f0c3e094849" />

### D Flip-Flop (Non Blocking)
```verilog
module d_ff (
    input wire d, clk,
    output reg Q
);
    always @(posedge clk) begin
        Q <= d;
    end
endmodule
```
### D Flip-Flop Test bench 
```verilog
module d_ff_tb;
    reg d, clk;
    wire Q;

    d_ff uut (
        .d(d), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        d = 0;
        #10;
        d = 1;
        #10;
        d = 0;
        #10;
        d = 1;
        #10;
        $finish;
    end
endmodule
```

#### SIMULATION OUTPUT
<img width="698" height="385" alt="image" src="https://github.com/user-attachments/assets/e537d3f0-c1ba-408b-99e4-13e9d9379d23" />

### T Flip-Flop (Non Blocking)
```verilog
module t_ff (
    input wire T, clk,
    output reg Q
);
    initial Q = 1'b0;

    
    always @(posedge clk) begin
        if (T == 1)
            Q <= ~Q;
        else
            Q <= Q;
    end
endmodule

```
### T Flip-Flop Test bench 
```verilog
module t_ff_tb;
    reg T, clk;
    wire Q;

    t_ff uut (
        .T(T), 
        .clk(clk), 
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        T = 0; 
        #10;
        T = 1; 
        #10;
        T = 1; 
        #10;
        T = 0; 
        #10;
        $finish;
    end
endmodule


```

#### SIMULATION OUTPUT
<img width="701" height="430" alt="image" src="https://github.com/user-attachments/assets/d8e61db0-7c0b-43bd-9dc3-54fe2c040211" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
