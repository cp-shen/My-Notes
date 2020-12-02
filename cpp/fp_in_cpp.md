## Chap 1 Intro to FP

### 1.1 What is FP？

> People tend to define FP through related concepts including **pure functions**, **lazy evaluation**, **pattern matching**, and such.

> Functional programming is a style of programming that **emphasizes the evaluation of expressions**, rather than execution of commands. The expressions in these languages are formed by using functions to combine basic values. A functional language is a language that supports and encourages programming in a functional style. —FAQ for comp.lang.functional 

> Broadly speaking, FP is a style of programming in which the main program building
> blocks are **functions as opposed to objects and procedures**. A program written in the functional style doesn’t specify the commands that should be performed to achieve the result, but rather **defines what the result is**.

> This difference is the origin of the terms **imperative** and **declarative** programming. Imperative means you command the computer to do something by explicitly stating each step it needs to perform in order to calculate the result. Declarative means you state what should be done, and the programming language has the task of figuring out how to do it.

### 1.2 Pure Functions
> One of FP’s most powerful ideas is pure functions: **functions that only use (but don’t modify) the arguments passed to them in order to calculate the result**. If a pure function is called multiple times with the same arguments, it must return the same result every time and leave no trace that it was ever invoked (**no side effects**). This all implies that pure functions are **unable to alter the state of the program**.

> a pure function is any function that **doesn’t have observable (at a higher level) side effects**. The function caller shouldn’t be able to see any trace that the function was executed, other than getting the result of the call