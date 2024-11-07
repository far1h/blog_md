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

![[cfg.png|200]]


## [[Top down parsing]]

### Example 1 [Alvina Aulia Top Down Parsing](https://www.youtube.com/watch?v=WpXMlZ5WipI&t=650s&ab_channel=AlvinaAulia)  : 
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

#### [[Parsing Table]]  

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

   #### [[Parsing Search]]

| stack       | input      | output       |
| ----------- | ---------- | ------------ |
| $E          | id+id$     | _E_ -> *TE'* |
| $E'T        | id+id$     | *T* -> *FT'* |
| $E'T'F      | id+id$     | *F* -> *id*  |
| $E'T'~~id~~ | ~~id~~+id$ | pop id       |
| $E'T        | +id$       | *T'* ->ε     |
| $E'         | +id$       | E' -> *+TE'* |
| $E'T~~+~~   | ~~+~~id$   | pop +        |
| $E'T        | id$        | *T* -> *FT'* |
| $E'T'F      | id$        | *F* -> *id*  |
| $E'T'~~id~~ | ~~id~~$    | pop Id       |
| $E'T'       | $          | *T'* ->ε     |
| $E'         | $          | E' -> ε      |
| ~~$~~       | ~~$~~      | accept       |

### Example 2 [[Kenny Jingga CT UTS Quiz]]:

Example 3 Ivan Sebastian CT UTS Quiz

Example 4 Sam Philip CT UTS Quiz

Example 5 Class Session 12 Exercise