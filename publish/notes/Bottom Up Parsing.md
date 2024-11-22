---
excerpt: steps for bottom up parsing and exercises
date: 2024-11-17
---
##### steps
1. Perform [[Go To operation]]
2. Find [[Follow]] value
3. Create [[SLR Table]]
4. [[Parsing Search for Bottom Up|Search]] through parsing

> no need to remove [[Left Recursive]]

### Example [Alvina Aulia Bottom Up Parsing](https://www.youtube.com/watch?v=X6RaKj53oGo&ab_channel=AlvinaAulia)  
1. _E_ -> *E + T | T*
2. *T* -> *T * F | F*
5. *F* -> *(E)* | *id*
## Perform [[Go To operation]]:
i0:  
*E'* -> *.E*   
1. _E_ -> *.E + T*
2.  _E_ -> *.T*
3. *T* -> *.T * F*
4. *T* -> *.F*
5. *F* -> *.(E)*
6. *F* -> *.id*

(Input E to i0)

i1:  
*E'* -> *E.*  
1. _E_ -> *E. + T*

(Input T to i0)  

i2:
2.  _E_ -> *T.*
3. *T* -> *T. * F*

(Input F to i0)  

i3:
4. *T* -> *F.*

![[Screenshot 2024-11-17 at 9.39.19 PM.png]]

## Find [[Follow]] value:

![[Screenshot 2024-11-18 at 12.40.57 PM.png]]
## Creating [[SLR Table]] :

![[Screenshot 2024-11-18 at 1.00.50 PM.png]]

## [[Parsing Search for Bottom Up|Search]] through parsing

![[Screenshot 2024-11-18 at 1.25.10 PM.png]]
## GSLC
S'-> .S
1. S -> .if C then S else S 
2. S -> .if  C  then  S
3. S -> .while  C  do  S
4. S -> .id = E
5. S -> .print(E)
6. C -> .E  R  E
7. E -> .E + T 
8. E -> .E−T 
9. E -> .T
10. T -> .T ∗ F
11. T ->  .T / F 
12. T -> .F
13. F -> .(E) 
14. F -> .id
15. F -> .num
16. R -> .> 
17. R ->  .< 
18. R ->  .>=  
19. R -> .<=
20. R -> .==
21. R -> .!=

 Steps:
5. Use the kernel method starting from the top most grammar
	1. Group the grammars
	2. Input the thing after the `.` to each grammar and group them
	3. If the result has a `.` before a variable, copy paste the variable producers from i0 and continue to check the grammars of the new group if there is a `.` before a variable
	4. If the group contains same exact grammars as previous groups label as the same group

Status: #idea  
Tags:  [[compilation-techniques#Final Exam]]

---
# References