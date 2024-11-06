character after the first character in the **non terminal values**

Ex: 
<u>A</u>bc = b 
A + b = +
ADE = ...

## Algorithm
1. If *S* is the start symbol, 
   ex: *S* -> *Ab* | *c*, then $ is the Follow value of *S*
2. If *A* -> $\alpha$*B*$\beta$, then all **First of $\beta$** is the <u>Follow of *B*</u> except $\varepsilon$
3. a. *A* -> $\alpha$*B*, then all **Follow of *A*** is the <u>Follow of *B*</u>
3. b. *A* -> $\alpha$*B*$\beta$ <u>and</u> First of $\beta$ is $\varepsilon$, then all **Follow of *A*** is the <u>Follow of *B*</u>
> You can use this algorithm or a cheat method by looking at the result of the production, and find the non terminal value after the terminal 

>When to use the cheat method?

> You can only find the follow values of the terminal on the lines before it