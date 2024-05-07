---
title: nand2Tetris - Week 1 - Logic Gates
date: 2024-05-07T00:01:57+02:00
draft: false
---

# Logic Gates

- A technique for implementing Boolean function using logic gates
- Logic gates:
  1. Elementary (Nand, And , Or, Not...)
  2. Composite (Mux, Adder,....)


## Elementary Logic Gates

### NAND

Gate Diagram:
![nand gate](nandgate.png "Nand Gate")

Function specification: 
```HDL
if (a==1 and b==1)
then out=0 else out=1
```

Truth Table

<!-- <div style="overflow-x:auto;"> -->
| x   | y   | NAND |
| --- | --- | ---- |
| 0   | 0   | 1    |
| 0   | 1   | 1    |
| 1   | 0   | 1    |
| 1   | 1   | 0    |
<!-- </div> --> 

![elementary gate](elementary.png "and or not gates")
### Circuit implementation

![Circuit implementations](Circuit_implementation.png "Circuit implementation of and or gates")

The following course does not deal with physical implementation of gates 
- Circuits, transistors, relays, etc is part of Electrical Engineering and not computer science.


# Hardware Simulator

Nand give is an elementary gate already provided in the course so no implementation need for this, we will build all other gates using Nand Gates.

Building logic gates and chips in a structured and incremental manner is crucial in a course like nand2tetris, where each component builds upon the functionality of previously constructed ones. Below is a recommended sequence for building the listed gates and chips, starting with the simplest and moving towards the more complex. This order ensures that each component you build can be tested and used in the subsequent, more complex components.

### Recommended Order for Building Gates and Chips:

1. **Not**
    
    - Start with the `Not` gate, as it is the simplest modification of a `Nand` gate and is fundamental to building other logic gates.
2. **And**
    
    - Next, construct the `And` gate using the `Nand` and `Not` gates. The `And` gate forms a basic building block for many other chips.
3. **Or**
    
    - Build the `Or` gate using `Nand` gates, which will also utilize the `Not` gate. The `Or` gate is essential for creating the `Xor` gate and various multiplexers.
4. **Xor**
    
    - With `Nand`, `Not`, and `Or` gates at your disposal, you can now construct the `Xor` gate, which is slightly more complex and used in various computing functions.
5. **Mux**
    
    - The basic `Mux` (Multiplexer) can be built using `And`, `Or`, and `Not` gates. This component is foundational for creating more complex multiplexers.
6. **Dmux**
    
    - Construct the `Dmux` (Demultiplexer) next, using previously built gates like `Not` and `And`. This chip is crucial for distributing signals in circuits.
7. **Not16**
    
    - Construct the `Not16` gate, which extends the functionality of the `Not` gate to 16-bit inputs. This requires simply replicating the `Not` operation across 16 channels.
8. **And16**
    
    - Similarly, build the `And16` gate, which is an extension of the `And` gate to 16-bit inputs.
9. **Or16**
    
    - Follow with `Or16`, which is an extension of the `Or` gate to handle 16-bit inputs.
10. **Or8Way**
    
    - The `Or8Way` takes an 8-input and outputs true if any input is true. This can be built using the `Or` and `Or16` logic.
11. **Mux16**
    
    - Build the `Mux16`, which is a 16-bit version of the `Mux`, using 16 sets of `Mux` gates to handle 16-bit inputs.
12. **Mux4Way16**
    
    - This is a 4-way 16-bit multiplexer, and can be built using multiple `Mux16` gates, controlled by additional logic gates to select among the 4 inputs.
13. **Mux8Way16**
    
    - Construct the `Mux8Way16` using `Mux4Way16` and other necessary logic components to expand the selection capability.
14. **Dmux4Way**
    
    - Build the `Dmux4Way`, a more complex version of the `Dmux`, using additional `Dmux` and logic gates to distribute a single input to one of four outputs.
15. **Dmux8Way**
    
    - Finally, construct the `Dmux8Way`, which extends the `Dmux4Way` functionality to eight outputs. This involves additional layers of demultiplexing.

### Building Approach:

Each gate or chip should be fully tested before proceeding to build more complex components that depend on it. Use the testing scripts provided by nand2tetris to ensure each component works correctly according to the specifications. This order of building ensures a logical progression, making debugging easier and helping solidify your understanding of digital logic as each new component introduces additional complexity.
