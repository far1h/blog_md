---
excerpt: rules for finding follow values
---
> cheat: terminal or symbol after the variable
## Algorithm
1. If *S* is the start symbol, 
   ex: *S* -> *Ab* | *c*, then $ is the Follow value of *S*
2. If *A* -> α*B*β, then all **First of β** is the <u>Follow of *B*</u> except ε
3. a. *A* -> α*B*, then all **Follow of *A*** is the <u>Follow of *B*</u>
3. b. *A* -> α*B*β <u>and</u> First of β is ε, then all **Follow of *A*** is the <u>Follow of *B*</u>

Special case
> If *A* -> α, i.e production result contains only 1 variable, add ε in front of the variable to conform to rule 3.a. *A* -> α*B

> You can only find the follow values of the variable on the lines before it

> The number of follow values is equivalent to the number of producer variables in our grammar
## Cheat
Ex: 
<u>A</u>bc = b   
A + b = +  

Status: #idea  
Tags:  [[compilation-techniques#Final Exam]], [[compilation-techniques#Mid Exam]], [[Bottom Up Parsing]], [[Top down parsing]]

---
# References
