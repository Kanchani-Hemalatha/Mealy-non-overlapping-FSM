# Mealy-non-overlapping-FSM
The FSM detects a specific sequence of input bits and produces an output accordingly, ensuring that detected sequences do not overlap.  Features
Mealy Non-Overlapping FSM
# Mealy Non-Overlapping FSM

## Overview
This repository contains the Verilog implementation of a **Mealy Non-Overlapping FSM**. The FSM detects a specific sequence of input bits and produces an output accordingly, ensuring that detected sequences do not overlap.

## Features
- **Mealy FSM**: Output depends on both the current state and input.
- **Non-Overlapping Detection**: Ensures that each detected sequence does not overlap with the next.
- **Four-State Design**: Implements four states (S0, S1, S2, S3) for processing input.
- **Asynchronous Reset**: Supports an external reset to initialize the FSM.

## Module Definition
```verilog
module mealy_fsm_nonoverlapping (
    input clk,
    input reset,
    input din,
    output reg dout
);
  
  parameter s0 = 3'b000, s1 = 3'b001, s2 = 3'b010, s3 = 3'b011;
  
  reg [2:0] current_state, next_state;
  
  always @(posedge clk or posedge reset) begin
    if (reset)
      current_state <= s0;
    else
      current_state <= next_state;
  end
  
  always @(*) begin
    case (current_state)
      s0: if (din) begin
            dout <= 1'b0;
            next_state <= s1;
          end else begin
            dout <= 0;
            next_state <= s0;
          end
      
      s1: if (din) begin
            dout <= 1'b0;
            next_state <= s1;
          end else begin
            dout <= 1'b0;
            next_state <= s2;
          end
      
      s2: if (din) begin
            dout <= 1'b0;
            next_state <= s3;
          end else begin
            dout <= 1'b0;
            next_state <= s0;
          end
      
      s3: if (din) begin
            dout <= 1'b0;
            next_state <= s1;
          end else begin
            dout <= 1'b1;
            next_state <= s0;
          end
      
      default: next_state <= s0;
    endcase
  end
  
endmodule
```

## Inputs and Outputs
| Signal | Direction | Description |
|--------|----------|-------------|
| clk    | Input    | Clock signal to drive the FSM |
| reset  | Input    | Asynchronous reset to initialize FSM |
| din    | Input    | Serial input bit stream |
| dout   | Output   | FSM output signal |

## State Transition Table
| Current State | Input (din) | Next State | Output (dout) |
|--------------|------------|------------|--------------|
| S0          | 0          | S0         | 0            |
| S0          | 1          | S1         | 0            |
| S1          | 0          | S2         | 0            |
| S1          | 1          | S1         | 0            |
| S2          | 0          | S0         | 0            |
| S2          | 1          | S3         | 0            |
| S3          | 0          | S0         | 1            |
| S3          | 1          | S1         | 0            | 

## Simulation and Testing
To verify the functionality of the FSM, a testbench should be implemented that:
1. Provides a clock signal.
2. Applies different input sequences.
3. Observes the state transitions and output behavior
   
## edapalyground link
https://www.edaplayground.com/x/rK8_

## simulation output
![image](https://github.com/user-attachments/assets/700ac0a3-16a0-4e4d-a327-144ec4ddf4ed)

## waveform
![image](https://github.com/user-attachments/assets/3699afa9-8cd4-431b-87fe-a3dcb353c63e)

