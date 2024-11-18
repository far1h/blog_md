---
title: how to do parsing search for bottom up
---
> The first stack is the first group 0 and add $ AFTER it

> Input will be given and add $ AFTER it

How to determine the output?
- By comparing the **left** most of the stack and the **left** most of the input 

##### rules
- if the output is SX then append number X as the left most of the stack, followed by the input that resulted the output and the stack from the previous operation
> when input is moved to the stack, it gets removed from the input 
- If the output is RX then replace the production result of  the line X with the producer variable (replace the number before the production result as well )
-  if the left most of the stack has no number, compare with the number beside it and append to the left 
- if the output has a production result that is long reverse it  and replace with the numbers until the last letter 

Status: #idea  
Tags: [[compilation-techniques]]  
  
---
# References
