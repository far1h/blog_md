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

Example: 
1. E -> TE'
2. E' -> +TE' | $\varepsilon$
3. T -> FT'
4. T' -> \*FT' | $\varepsilon$
5. F -> (E) | id

[[First]] E = \(, id (this is from E -> T -> F) 
> why only use T??

[[First]] E' =  +, $\varepsilon$
[[First]] T = (, id
[[First]] T' = \*, $\varepsilon$
[[First]] F = (, id



