---
title: "nand2Tetris - Week 1 - Boolean Function"
date: 2024-05-06T22:55:23+02:00
draft: false
---


# Boolean Values

Boolean values can be represented as :
- False, True
- No, Yes
- 0,1

What can be done if we only have 0 and 1, lets take a look few example:

### AND Gate
We have an AND operation which can take either 1 or 0 for two inputs x and Y and only return 0 or 1 as an output. Below is the truth table for this "AND" operation:

<!-- <div style="overflow-x:auto;"> -->
| x   | y   | AND |
| --- | --- | --- |
| 0   | 0   | 0   |
| 0   | 1   | 0   |
| 1   | 0   | 0   |
| 1   | 1   | 1   |
<!-- </div> -->


We can see from the truth table that only when both x and y have input as 1 we have output as 1. 


### OR Gate
In the following operation if either x or y has an input 1 then output is 1.

| x   | y   | OR  |
| --- | --- | --- |
| 0   | 0   | 0   |
| 0   | 1   | 1   |
| 1   | 0   | 1   |
| 1   | 1   | 1   |

### NOT Gate
This one is a unary operation it only takes a single input and produces a single output:

| x   | NOT |
| --- | --- |
| 0   | 1   |
| 1   | 0   |
We can see with the truth table above for NOT gate that this operation flips the input value provided. 

  

## Boolean Expressions

  

Solve following boolean equation: (NOT (0 or (1 AND 1) )


output for 1 and 1 is 1 , hence

=> (NOT (0 or (1))

  

output for 0 or 1 is 1, hence

=> (NOT (1))

  

output for NOT(1) is 0, hence

=> (NOT (0 or (1 AND 1) ) = 0

  

## Boolean Functions

  
**Formula**
f(x,y,z) = (x and y) OR (NOT(x) and z) } 

**Truth Table**

| x   | y   | z   | f(x,y,z) |
| --- | --- | --- | -------- |
| 0   | 0   | 0   | 0        |
| 0   | 0   | 1   | 1        |
| 0   | 1   | 0   | 0        |
| 1   | 0   | 0   | 0        |
| 0   | 1   | 1   | 1        |
| 1   | 0   | 1   | 0        |
| 1   | 1   | 0   | 1        |
| 1   | 1   | 1   | 1        |
  

## Boolean Identities

  

### Commutative Laws

- (x AND y ) = (y and x)

- (x OR y) = (y OR x)


*Whatever the value of x, y is , it is always equal value no matter the operation if the order is changed *

  
## Associative Laws

- (x AND (y and z)) = ((x AND y) AND z)

- (x OR (y OR z)) = ((x OR y) OR z)


*It doesn't matter whether one does y and z and then x or switch it with first x and y and then z, the output will be same , this is associate law, same condition applies for OR operation.


## Distributive Laws

- (x AND (y OR z)) = (x AND y) or (x AND z)

- (x OR (y AND z)) = (x OR y) AND (x OR z)

  

## De Morgan Laws

- NOT(x AND y) = NOT(x) OR NOT(y)

- NOT(x OR y) = NOT(x) AND NOT(y)

## Boolean Function Synthesis

#### Theorem
Any Boolean function can be represented using an expression containing AND and NOT operations.

#### Proof
(x OR y) = NOT(NOT(x) AND NOT (y))

| x   | y   | NOT(NOT(x) AND NOT (y)) |
| --- | --- | ----------------------- |
| 0   | 0   | 0                       |
| 0   | 1   | 1                       |
| 1   | 0   | 1                       |
| 1   | 1   | 1                       |
#### NAND GATE
This is a combined version of AND and NOT.

**Truth Table**

| x   | y   | NAND |
| --- | --- | ---- |
| 0   | 0   | 1    |
| 0   | 1   | 1    |
| 1   | 0   | 1    |
| 1   | 1   | 0    |
NAND Gate only ouputs 0 when both of its input are 1 and every other possibility gives 1. 
Logically the x NAND Y is the negation of x AND y i.e 
$$\LARGE {(x \ NAND \ y) = NOT(x \ AND \ y)}$$








