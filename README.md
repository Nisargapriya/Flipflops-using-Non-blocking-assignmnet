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
### SR Flip-Flop Test bench 
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
#### SIMULATION OUTPUT
<img width="1671" height="843" alt="image" src="https://github.com/user-attachments/assets/7b1536f8-9dd9-4e7e-aae5-521ef936a30a" />

### JK Flip-Flop (Non Blocking)
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
### JK Flip-Flop Test bench 
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
#### SIMULATION OUTPUT
<img width="1635" height="895" alt="image" src="https://github.com/user-attachments/assets/b1fcbbca-5a8b-4400-8e12-975534d0c755" />

### D Flip-Flop (Non Blocking)
module d_ff (
    input wire d, clk,
    output reg Q
);
    always @(posedge clk) begin
        Q <= d;
    end
endmodule
### D Flip-Flop Test bench 
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
#### SIMULATION OUTPUT
<img width="1631" height="909" alt="image" src="https://github.com/user-attachments/assets/35afeaed-3bc7-4676-8395-e3585518fe15" />

### T Flip-Flop (Non Blocking)
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
### T Flip-Flop Test bench 
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
#### SIMULATION OUTPUT

<img width="1414" height="894" alt="image" src="https://github.com/user-attachments/assets/9c40a6a4-d6f3-4e4d-ba7b-1390b58f781d" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
