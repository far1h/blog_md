---
title: Compilation Techniques
excerpt: Stupid Course about Compilers taken @BINUS
---
- [ ] ALVINA AULIA
- [ ] AS
- [ ] RAZ
- [ ] RESPONSI REG
- [x] RESPONSI GC
- [ ] PRACTICE QUESTIONS CLASS
	- [ ] QUIZ
	- [ ] ASSIGNMENTS
- [ ] pick up transcripts

## top down parsing
reference: [Alvina Aulia Top Down Parsing](https://www.youtube.com/watch?v=WpXMlZ5WipI&t=650s&ab_channel=AlvinaAulia)  

#### rules
1. no left recursive and left factoring
2. find [[First]] values (as many grammars that we have)
3. find [[Follow]] value (as many grammars that we have)
4. make parsing table

#### Example: 
1. _E_ -> *TE'*
2. E' -> *+TE'* | $\varepsilon$
3. *T* -> *FT'*
4. *T'* -> *\*FT'* | $\varepsilon$
5. *F* -> *(E)* | *id*


### [[First]] Values:
1. [[First]] E = \(, id `(this is from E -> T -> F)`
> why only use T?? i guess because its the first terminal
2. [[First]] E' =  +, $\varepsilon$
3. [[First]] T = (, id
4. [[First]] T' = \*, $\varepsilon$
5. [[First]] F = (, id

### [[Follow]] Values:

1. [[Follow]] E = $, )  
2. [[Follow]] E' = $, )  
   *E* -> *T**E'***  
   *A* -> $\alpha$ *B*  
3. [[Follow]] T = +, $, ) 
   > use algorithm 2 and 3b because there is an $\varepsilon$  

   _E_ -> *TE'*  
   *A* -> $\alpha$ *B*  `(T is at position $\alpha$ so can't use this grammar)`  
   E' -> *+TE'* `(we dont write $\varepsilon$ because it doesn't contain T)`  
   *A* -> $\alpha$*B*$\beta$  
4. [[Follow]] T' =   +, $, ) 
   *T* -> *FT'*  
   *A* -> $\alpha$ *B*  
5. [[Follow]] F = \*, +, $, )  
   *T'* -> *\*FT'*  
   *A* -> $\alpha$*B*$\beta$   

### Parsing Table
> Rows: Terminals  
> Columns: Symbols, and Values

How to fill the table?  
1. Look at the first, and fill where we got the first values  
2. If there is an $\varepsilon$ at the first, then look at follow and write the terminal -> $\varepsilon$  for the follow values  
> notice how theres no `| (or)`   

|     | id                                                          | +                                                            | *               | (                                                       | )                    | $                    |
| --- | ----------------------------------------------------------- | ------------------------------------------------------------ | --------------- | ------------------------------------------------------- | -------------------- | -------------------- |
| E   | _E_ -> *TE'*`(we started from the this and later found id)` |                                                              |                 | _E_ -> *TE'* `(we started from this and later found ()` |                      |                      |
| E'  |                                                             | E' -> *+TE'* `(we got this from it's own production values)` |                 |                                                         | E' -> $\varepsilon$  | E' -> $\varepsilon$  |
| T   | *T* -> *FT'*                                                |                                                              |                 | *T* -> *FT'*                                            |                      |                      |
| T'  |                                                             | *T'* ->$\varepsilon$                                         | *T'* -> *\*FT'* |                                                         | *T'* ->$\varepsilon$ | *T'* ->$\varepsilon$ |
| F   | *F* -> *(E)*                                                |                                                              |                 |                                                         |                      |                      |

   

