# Mealy FSM Non-Overlapping Sequence Detector(1010)

## Overview
This Verilog module implements a **Mealy finite state machine (FSM) with non-overlapping sequence detection**. Unlike the Moore FSM, the **Mealy FSM determines its output based on both the current state and input**. The **non-overlapping** nature ensures that each detected sequence is counted separately.

## Features
- **Mealy FSM**: Output depends on both the current state and input (`din`).
- **Non-Overlapping Sequence Detection**: Ensures strict pattern detection.
- **Four-State Implementation**: Uses states `s0` to `s3`.
- **Clock Synchronous**: State transitions occur on the rising edge of `clk`.
- **Asynchronous Reset**: FSM resets to `s0` when `reset` is high.

## State Diagram
The FSM transitions through four states:

- `s0` (Idle state)
- `s1`, `s2` (Intermediate states for pattern detection)
- `s3` (Final state where `dout = 1` is asserted, completing the sequence)

## State Transition Table

| Current State | `din = 0` Next State | `din = 1` Next State | Output `dout` |
|--------------|--------------------|--------------------|------------|
| `s0`        | `s0`               | `s1`               | `0`        |
| `s1`        | `s2`               | `s1`               | `0`        |
| `s2`        | `s0`               | `s3`               | `0`        |
| `s3`        | `s0`               | `s1`               | `1`        |

## Inputs & Outputs
### Inputs:
- `clk`: Clock signal for synchronous state transitions.
- `reset`: Asynchronous reset to initialize FSM.
- `din`: Serial input bit stream.

### Output:
- `dout`: Output signal, set to `1` when the FSM reaches the final state **`s3` with `din = 0`**.
   
## edapalyground link
https://www.edaplayground.com/x/rK8_

## simulation output
![image](https://github.com/user-attachments/assets/700ac0a3-16a0-4e4d-a327-144ec4ddf4ed)

## waveform
![image](https://github.com/user-attachments/assets/50ea9bab-3d35-4918-bc95-f09c44cb62a4)

