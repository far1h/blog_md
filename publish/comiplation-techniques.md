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
- [ ] Accept housin offer
- [ ] Pick up transcript
- [ ] comvis exam

![[cfg.png|200]]

[[Context Free Grammar]]
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
P -> S P | ε  
S -> A | C | E  
A -> sigma = E ;  
C -> if (E) {S} else {S}  
E -> E + T | E - T | T  
T -> T * F | T / F | F  
F -> (E) | sigma | mewing | rizz  

> check for [[left factoring]] and [[left recursive]] needed  

#### [[Left Factoring]]:
E -> E + T | E - T | T  
**E -> EX | T**  
**X -> +T|-T**  

T -> T * F | T / F | F  
**T -> TY | F**  
**Y -> \*F | / F**  

#### [[Left Recursive]]:
E -> EX | T  
**E -> TE'**  
E' -> XE' | ε  
**E' -> +TE' | -TE' | ε**  

T -> TY | F  
**T -> FT'**  
T' -> YT' | ε  
**T' -> \*FT' | /FT' | ε**  

#### [[First]] Values: 
P -> S P | ε  
S -> A | C | E  
A -> sigma = E ;  
C -> if (E) {S} else {S}  
E -> TE'  
E' -> +TE' | -TE' | ε  
T -> FT'  
T' -> \*FT' | /FT' | ε  
F -> (E) | sigma | mewing | rizz  

P: sigma `from S -> A`,  if `from S -> C` , ( , mewing, rizz `these from S -> E`,  ε  
P: sigma,  if , ( , mewing, rizz,  ε  
S: sigma,  if , ( , mewing, rizz    
A: sigma  
C: if  
E: ( , sigma, mewing, rizz  
E': + , - , ε  
T: ( , sigma, mewing, rizz  
T': \*, / , ε  
F: ( , sigma, mewing, rizz  

#### [[Follow]] Values: 
P -> S P | ε  
S -> A | C | E  
A -> sigma = E ;  
C -> if (E) {S} else {S}  
E -> TE'  
E' -> +TE' | -TE' | ε  
T -> FT'  
T' -> \*FT' | /FT' | ε  
F -> (E) | sigma | mewing | rizz  

==P: $== `because of start symbol`  
> nothing else in the grammars have terminal that follows P   

S: `First(P)`, `Follow(P)`, }  `from C grammar {S}`  
==S: sigma,  if , ( , mewing, rizz,  $, }==  
P -> S P | ε   
*A* -> α*B*β | ε  `2nd and 3b rule`  

A: `Follow(S)`  
==A: sigma,  if , ( , mewing, rizz,  $, }==  
S -> A | C | E  
*A* -> α*B* `3a rule`  

C: `Follow(S)`  
==C:  sigma,  if , ( , mewing, rizz,  $, }==  
S -> A | C | E  
*A* -> α*B* `3a rule`  

E: `Follow(S)`, ; `from A grammar`, ) `from C & F grammar`  
==E:   sigma,  if , ( , mewing, rizz,  $, }, ;, )==  
S -> A | C | E  
*A* -> α*B* `3a rule`  

E': `Follow(E)`  
==E':   sigma,  if , ( , mewing, rizz,  $, }, ;, )==  
E -> TE'  
*A* -> α*B* `3a rule`  

T: `First(E')`, `Follow(E')`  
==T: + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )==  
E' -> +TE' | -TE' | ε  
*A* -> α*B*β `2nd and 3b rule`  

T': `Follow(T)`  
==T': + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )==  
T -> FT'  
*A* -> α*B* `3a rule`  

F: `First(T')`, `Follow(T')`  
==F: \*, / , + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )==  
T' -> \*FT' | /FT' | ε  
*A* -> α*B*β `2nd and 3b rule`  

#### [[Parsing Table]]  
P -> S P | ε  
S -> A | C | E  
A -> sigma = E ;  
C -> if (E) {S} else {S}  
E -> TE'  
E' -> +TE' | -TE' | ε  
T -> FT'  
T' -> \*FT' | /FT' | ε  
F -> (E) | sigma | mewing | rizz  

[[First]]:  
P: sigma,  if , ( , mewing, rizz,  ε  
S: sigma,  if , ( , mewing, rizz    
A: sigma  
C: if  
E: ( , sigma, mewing, rizz  
E': + , - , ε  
T: ( , sigma, mewing, rizz  
T': \*, / , ε  
F: ( , sigma, mewing, rizz  

[[Follow]]:   
P: $  
S: sigma,  if , ( , mewing, rizz,  $, }    
A: sigma,  if , ( , mewing, rizz,  $, }  
C:  sigma,  if , ( , mewing, rizz,  $, }  
E:   sigma,  if , ( , mewing, rizz,  $, }, ;, )  
E':   sigma,  if , ( , mewing, rizz,  $, }, ;, )  
T: + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )  
T': + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )  
F: \*, / , + , - ,  sigma,  if , ( , mewing, rizz,  $, }, ;, )  

|     | *   | /   | +   | -   | sigma     | if       | (        | )   | mewing    | rizz     | $      | }   | ;   |
| --- | --- | --- | --- | --- | --------- | -------- | -------- | --- | --------- | -------- | ------ | --- | --- |
| P   |     |     |     |     | P -> S P  | P -> S P | P -> S P |     | P -> S P  | P -> S P | P -> $ |     |     |
| S   |     |     |     |     | S ->sigma | S->C     | S->(E)   |     | S->mewing | S->rizz  |        |     |     |
| A   |     |     |     |     |           |          |          |     |           |          |        |     |     |
| C   |     |     |     |     |           |          |          |     |           |          |        |     |     |
| E   |     |     |     |     |           |          |          |     |           |          |        |     |     |
| E'  |     |     |     |     |           |          |          |     |           |          |        |     |     |
| T   |     |     |     |     |           |          |          |     |           |          |        |     |     |
| T'  |     |     |     |     |           |          |          |     |           |          |        |     |     |
| F   |     |     |     |     |           |          |          |     |           |          |        |     |     |
i gave up lol

### Example 3 Ivan Sebastian CT UTS Quiz

Example 4 Sam Philip CT UTS Quiz

Example 5 Class Session 12 Exercise