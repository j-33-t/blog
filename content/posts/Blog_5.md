---
title: "nand2Tetris - Week 3 - Memory"
date: 2024-05-23T02:39:39+02:00
draft: false
---

# Memory

This week, I focused on building memory components, from basic bits to the RAM16K chip. The transition from combinatorial logic to sequential logic was marked by the introduction of the DFF (Data Flip-Flop) chip, which serves as the fundamental building block for memory in this unit.

## Components Built

1. **Bit**
2. **Register**
3. **RAM8**
4. **RAM64**
5. **RAM512**
6. **RAM4K**
7. **RAM16K**
8. **Program Counter (PC)**

## DFF - The Elementary Memory Chip

In this unit, the DFF chip was provided as an elementary memory chip. Unlike previous units where we focused on combinatorial logic, this unit's focus was on sequential logic. The DFF chip is essential for creating memory circuits that can store and recall values over time. Although in reality, a DFF can be built using NAND gates, this unit provided it as a given to emphasize the learning on how to use sequential logic to build more complex memory structures.

## Bit

![Bit Chip](https://i.sstatic.net/XjmZNm.png "Bit Chip Diagram")

### HDL Code
```HDL
// Bit implementation
CHIP Bit {
    IN in, load;
    OUT out;

    PARTS:
    Mux(a=outLoop,b=in,sel=load,out=dfin);
    DFF(in=dfin,out=out, out=outLoop);
    
}
```

### Explanation
- The Bit chip uses a DFF to store a single bit of data.
- The Mux component selects whether to load a new input or retain the current stored value.

## Register

### Diagram
![Register Diagram](link_to_diagram)

### HDL Code
```HDL
// Register implementation
CHIP Register {
    IN in[16], load;
    OUT out[16];

    PARTS:
    Bit (in=in[0], load=load, out=out[0]);
    Bit (in=in[1], load=load, out=out[1]);
    // ... Repeat for all 16 bits
}
```

### Explanation
- The Register is a 16-bit storage, essentially a collection of 16 Bit chips.
- Each Bit chip stores one bit of the 16-bit input.

## RAM8



### HDL Code
```HDL
// RAM8 implementation
CHIP RAM8 {
    IN in[16], load, address[3];
    OUT out[16];

    PARTS:
    //// Replace this comment with your code.
    DMux8Way(in=load,sel=address,a=reg1,b=reg2,c=reg3,d=reg4,e=reg5,f=reg6,g=reg7,h=reg8);

    Register(in=in ,load=reg1 ,out=regout1 );
    Register(in=in ,load=reg2 ,out=regout2 );
    Register(in=in ,load=reg3 ,out=regout3 );
    Register(in=in ,load=reg4 ,out=regout4 );
    Register(in=in ,load=reg5 ,out=regout5 );
    Register(in=in ,load=reg6 ,out=regout6 );
    Register(in=in ,load=reg7 ,out=regout7 );
    Register(in=in ,load=reg8 ,out=regout8 );

    Mux8Way16(a=regout1 ,b=regout2 ,c=regout3 ,d=regout4 ,e=regout5 ,f=regout6 ,g=regout7 ,h=regout8 ,sel=address ,out=out );
}
```

### Explanation
- RAM8 uses eight 16-bit registers to store data.
- It includes logic to select which register to read from or write to.

## RAM64


### HDL Code
```HDL
// RAM64 implementation
CHIP RAM64 {
    IN in[16], load;
    OUT out[16];
    PARTS:
    // First select MSB from address
    DMux8Way(in=load, sel[0]=address[3], sel[1]=address[4], sel[2]=address[5], a=ram0,b=ram1,c=ram2,d=ram3,e=ram4,f=ram5,g=ram6,h=ram7);

    // ... same logic as previous ram8 but instead of registers we use ram8 here 8 times. 
    
    // Second select LSB from address for Ram8
    RAM8(in=in, load=ram0, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out0);
    RAM8(in=in, load=ram1, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out1);
    RAM8(in=in, load=ram2, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out2);
    RAM8(in=in, load=ram3, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out3);
    RAM8(in=in, load=ram4, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out4);
    RAM8(in=in, load=ram5, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out5);
    RAM8(in=in, load=ram6, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out6);
    RAM8(in=in, load=ram7, address[0]=address[0], address[1]=address[1], address[2]=address[2], out=out7);

    Mux8Way16(a=out0,b=out1,c=out2,d=out3,e=out4,f=out5,g=out6,h=out7,sel[0]=address[3], sel[1]=address[4], sel[2]=address[5], out=out);

}
```

### Explanation
- RAM64 expands on RAM8, using additional logic to manage 64 registers.
- It organizes eight RAM8 units to increase storage capacity.

## RAM512


### HDL Code
```HDL
// RAM512 implementation
CHIP RAM512 {
    IN in[16], load;
    OUT out[16];
    PARTS:
    
    // ... Additional logic to handle 512 registers using 8 ram64 units
}
```

### Explanation
- RAM512 further scales up the memory using RAM64 units.
- It includes more complex addressing logic to manage the larger number of registers.

## RAM4K


### HDL Code
```HDL
// RAM4K implementation
CHIP RAM4K {
    IN in[16], load;
    OUT out[16];
    PARTS:
    
    // ... Additional logic to handle 4K registers
}
```

### Explanation
- RAM4K organizes eight RAM512 units.
- It handles larger storage with more intricate addressing.

## RAM16K



### HDL Code
```HDL
// RAM16K implementation
CHIP RAM16K {
    IN in[16], load;
    OUT out[16];
    PARTS:
    
    // ... Additional logic to manage 16K storage
}
```

### Explanation
- RAM16K is the largest memory chip built in this unit.
- It uses RAM4K units and additional addressing logic to manage a substantial amount of storage.

## Program Counter (PC)



### HDL Code
```HDL
// PC implementation
CHIP PC {
    IN in[16],inc, load, reset;
    OUT out[16];
    
    PARTS:
    
    // Inc Flag
    Inc16(in=regOut, out=incOut);
    Mux16(a=regOut, b=incOut, sel=inc, out=incFinal);

    // Load Flag
    Mux16(a=incFinal, b=in, sel=load, out=loadOut);

    // Reset Zero Input
    Not16(in=in, out=flip);
    And16(a=flip, b=in, out=zero);

    // Reset Flag
    Mux16(a=loadOut, b=zero, sel=reset, out=resetOut);

    
    // One Register Load Input
    Not(in=load, out=flipLoad);
    Or(a=flipLoad,b=load, out=one);

    // Note!! Imporant part, always keep register load to be one, and loop one output back to Inc Flag
    //        This makes sure that the current operation is thrown into output and the output value can 
              can computed on again

    // Register Out, second output back to incrementor 
    Register(in=resetOut, load=one,out=out, out=regOut );

     
}

```

### Explanation
- The Program Counter (PC) was the most challenging chip to design.
- It needed to remember the previous output and compute on it while providing a new output at each step.
- The trick was to output two values but ensure the load was always one in the end register. This allowed one output to be the external output and the other to be used internally for further computation.

## Challenges and Learning Outcomes

Building the PC chip was particularly tricky because it required managing state over time, unlike the purely combinational logic of previous chips. The solution involved using multiple outputs and carefully controlling the load signals to ensure correct operation.

## Conclusion

This week, I delved into sequential logic and memory components. The progression from simple bits to the complex RAM16K chip and the challenging PC chip provided a deep understanding of how memory works in digital systems.


