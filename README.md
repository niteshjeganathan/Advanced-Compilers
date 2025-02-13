# Advanced Compilers

## The m × n Compiler Problem: Managing Multiplicative Complexity in Compiler Development
Each programming language requires a front-end to analyze and transform its syntax and semantics into an intermediate representation (IR). Each target architecture requires a back-end to generate optimized machine code. A direct approach would imply building separate compilers for each language-target pair. The science of compilers hasn't reached to that point yet
where developing compilers suitable for so many languages and targets is easy. Modern compiler design mitigates this challenge by employing intermediate representations, modular compiler infrastructures, and retargetable code generation. 

## Program Representation 
Representing programs effectively is a vital step in a compilation pipeline, since the high-level language we use to write these programs aren't semantically understandable in a compiler's perspective. There are various program representations that are used in different stages of the compiler pipeline. 

### Abstract Syntax Tree (AST) 
It captures the heirarichal structure of the entire program in the form a tree, while exluding various extraneous details such as paranthesis and formatting. This is very useful while parsing or analysing the semantics since the entire structure of the program can be parsed/analysed recursively like we do in any tree. 

### Control Flow Graphs (CFG) 
It is a directed graph representation of the entire program, where each node represent a basic block and the edges represent the control flow between them. This form of representation helps to analyse the reachability of the code and aids in optimization of the code. 

## Basic Block 
A basic block is a set of instructions where the control flow between them is strictly sequential. There are no jump or branch statements within them. If one of these instructions belonging to a single block is going to run, it is safe to assume that all the other instructions are going to run as well. There is only entry point and one exit point to this block, so 
there can't be other blocks which jump to some statement in between another basic block. 

## Compiler Optimizations
Compiler Optimizations aim to improve the efficiency and performance of a working program while preserving the correctness of the code. These optimizations can be classified based on their scope: 

### Local Optimizations
These optimizations are performed under a single basic block without considering the broader aspect of the code. Some examples are: 
* Constant Folding
* Dead Code Elimination (DCE)
* Strength Reduction

### Global Optimizations
These optimizations extend beyond the scope of a single basic block but still remain in a single function. Some examples are: 
* Loop-invariant Code Motion (LICM)
* Common Subexpression Elimiation (CSE)
* Global Constant Propogation

### Intra-procedural Optimizations
These optimizations take place under a single procedure/function. Local and global optimizations come under this classification. Some examples are: 
* Register Allocation
* Dead Code Elimination
* Instruction Scheduling

### Inter-procedural Optimizations 
These optimizations take place across multiple functions, leveraging cross-function data flow analysis. Some examples are: 
* Alias Analysis
* Inlining Functions
* Intraprocdural Constant Propogation

## Dead Code Elimination (DCE)
It is an optimization technique that removes part of code that doesn't affect the code's output in any way. This form of code reduction can save up memory and also unncessary computations, leading to optimized execution. There are many cases where DCE is possible: 

1. Unreachable
```c++
void abc() {
    return 0;
    cout << 5; //unreachable
}
```
2. Unused Variable Assignments
```c++
void abc() {
    int x = 5; //Unused Variable
    int y - 10;
    cout << y;
}
```
3. Dead Function Calls
```c++
void abc() {}
void cde() {
    abc(); //Dead Function Call
    return 5;
}
```
4. Dead Stores
```c++
void abc() {
    int x = 5; //Dead Store
    x = 20;
    cout << x;
```
