---
excerpt: how to do parsing search
---
> The first stack is the start symbol and add $ before it

> Input will be given

How to determine the output?
- By comparing the right most of the stack and the left most of the input 

##### rules
- Stack gets replaced by the production values or the thing that comes after the `->` but reverse it
- If `stack == input` POP STACK AND INPUT
- if there is ε after -> POP STACK
- if `stack == $` and `input == $` ACCEPT
- if stack `≠` input REJECT

Status: #idea  
Tags: [[compilation-techniques]]  
  
---
# References
