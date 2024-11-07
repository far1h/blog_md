---
title: Compilation Techniques
excerpt: Stupid Course about Compilers taken @BINUS
---
- [ ] ALVINA AULIA
- [ ] AS
	- [ ] 5
	- [ ] 4
	- [ ] 2
	- [ ] 1
- [ ] RAZ
- [ ] RESPONSI REG
- [x] RESPONSI GC
- [ ] PRACTICE QUESTIONS CLASS
	- [ ] QUIZ
	- [ ] ASSIGNMENTS
- [ ] pick up transcripts

## top down parsing
reference: [Alvina Aulia Top Down Parsing](https://www.youtube.com/watch?v=WpXMlZ5WipI&t=650s&ab_channel=AlvinaAulia)  

![[cfg.png|200]]
##### rules
1. no left recursive and left factoring
2. find [[First]] values (as many grammars that we have)  
3. find [[Follow]] value (as many grammars that we have)  
4. make parsing table  
5. search through the parsing  
### Example 1: 
1. _E_ -> *TE'*
2. E' -> *+TE'* | ε
3. *T* -> *FT'*
4. *T'* -> *\*FT'* | ε
5. *F* -> *(E)* | *id*
#### [[First]] Values:
1. [[First]] E = \(, id `(this is from E -> T -> F)`
2. [[First]] E' =  +, ε
3. [[First]] T = (, id
4. [[First]] T' = \*, ε
5. [[First]] F = (, id

#### [[Follow]] Values:

1. [[Follow]] E = $, ) `() comes after E in F)`  
2. [[Follow]] E' = $, )  
   *E* -> *T**E'***  
   *A* -> α *B*  
3. [[Follow]] T = +, $, ) 
   > use algorithm 2 and 3b because there is an ε  

   _E_ -> *TE'*  
   *A* -> α *B*  `(T is at position α so can't use this grammar)`  
   E' -> *+TE'* `(we dont write ε because it doesn't contain T)`  
   *A* -> α*B*β  
4. [[Follow]] T' =   +, $, ) 
   *T* -> *FT'*  
   *A* -> α *B*  
5. [[Follow]] F = \*, +, $, )  
   *T'* -> *\*FT'*  
   *A* -> α*B*β   

#### Parsing Table
> Rows: Variables  
> Columns: Terminals, and Values

How to fill the table?  
1. Look at the first of each variable, and fill where we got the first values  
2. If there is an ε at the first, then look at follow value of the variable and write the variable -> ε  for the follow values  

> notice theres no `| (or)`   

|     | id           | +            | *               | (            | )        | $         |
| --- | ------------ | ------------ | --------------- | ------------ | -------- | --------- |
| E   | _E_ -> *TE'* |              |                 | _E_ -> *TE'* |          |           |
| E'  |              | E' -> *+TE'* |                 |              | E' -> ε  | E' -> ε   |
| T   | *T* -> *FT'* |              |                 | *T* -> *FT'* |          |           |
| T'  |              | *T'* ->ε     | *T'* -> *\*FT'* |              | *T'* ->ε | *T'* -> ε |
| F   | *F* -> *id*  |              |                 | *F* -> *(E)* |          |           |

Notes:  
E id = `(we started from the this and later found id)`  
E' + = `(we got this from it's own production values)`  
E ( =`(we started from this and later found ()`  

   #### Parsing Search

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

| stack       | input      | output               |
| ----------- | ---------- | -------------------- |
| $E          | id+id$     | _E_ -> *TE'*         |
| $E'T        | id+id$     | *T* -> *FT'*         |
| $E'T'F      | id+id$     | *F* -> *id*          |
| $E'T'~~id~~ | ~~id~~+id$ | pop id               |
| $E'T        | +id$       | *T'* ->ε |
| $E'         | +id$       | E' -> *+TE'*         |
| $E'T~~+~~   | ~~+~~id$   | pop +                |
| $E'T        | id$        | *T* -> *FT'*         |
| $E'T'F      | id$        | *F* -> *id*          |
| $E'T'~~id~~ | ~~id~~$    | pop Id               |
| $E'T'       | $          | *T'* ->ε |
| $E'         | $          | E' -> ε  |
| ~~$~~       | ~~$~~      | accept               |

