---
excerpt: steps for bottom up parsing and exercises
date: 2024-11-17
---
##### steps
1. [[Go To operation]]
2. Find [[Follow]] value
3. Create [[SLR Table]]
4. [[Parsing Search for Bottom Up|Search]] through parsing

> no need to remove [[Left Recursive]]

### Example [Alvina Aulia Bottom Up Parsing](https://www.youtube.com/watch?v=X6RaKj53oGo&ab_channel=AlvinaAulia)  
1. _E_ -> *E + T | T*
2. *T* -> *T * F | F*
5. *F* -> *(E)* | *id*
#### [[Go To operation]]:
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

(Input ( to i0)  

![[Screenshot 2024-11-17 at 9.39.19 PM.png]]

## Find [[Follow]] value:

![[Screenshot 2024-11-18 at 12.40.57 PM.png]]
## Creating [[SLR Table]] :

![[Screenshot 2024-11-18 at 1.00.50 PM.png]]

## [[Parsing Search for Bottom Up|Search]] through parsing

![[Screenshot 2024-11-18 at 1.25.10 PM.png]]

Status: #idea  
Tags:  [[compilation-techniques]]

---
# References