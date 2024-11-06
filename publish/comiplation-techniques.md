---
title: Compilation Techniques
---
- [ ] ALYS
- [ ] RAZIEL
- [ ] RESPONSI RAFI
- [ ] RESPONSI GC
- [ ] PRACTICE QUESTIONS CLASS
	- [ ] QUIZ
	- [ ] ASSIGNMENTS

## top down parsing
rules
1. no left recursive and left factoring
2. find [[First]] values (as many grammars that we have)
3. find [[Follow]] value (as many grammars that we have)

Example: 
1. $E$ -> $TE'$
2. $E'$ -> $+TE'$ | $\varepsilon$
3. $T$ -> $FT'$
4. $T'$ -> $* FT'$ | $\varepsilon$
5. $F$ -> $(E)$ | $id$

[[First]] Values:
1. [[First]] E = \(, id (this is from E -> T -> F) 
> why only use T??
2. [[First]] E' =  +, $\varepsilon$
3. [[First]] T = (, id
4. [[First]] T' = \*, $\varepsilon$
5. [[First]] F = (, id

[[Follow]] Values:

1. [[Follow]] E = $, )
2. [[Follow]] E' = 




