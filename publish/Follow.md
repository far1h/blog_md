character after the first character in the **terminal values**

Ex: 
<u>A</u>bc = b 
A + b = +
ADE = ...

## Algorithm
get the terminal after the variable
1. If *S* is the start symbol, 
   ex: *S* -> *Ab* | *c*, then $ is the Follow value of *S*
2. If *A* -> α*B*β, then all **First of β** is the <u>Follow of *B*</u> except ε
3. a. *A* -> α*B*, then all **Follow of *A*** is the <u>Follow of *B*</u>
3. b. *A* -> α*B*β <u>and</u> First of β is ε, then all **Follow of *A*** is the <u>Follow of *B*</u>
> You can use this algorithm or a cheat method by looking at the result of the production, and find the terminal value after the terminal 

>When to use the cheat method?

> You can only find the follow values of the terminal on the lines before it