---
date: 2024-12-29
---
similar to [[Intermediate Code Generator]]

> Expressed as: `Opr Arg1, Store/result`

> No arg2

> Use # for numbers

> If there is a `while` or `if`, add `jmpf` right away only

> `do while` uses `jmpt` only

> `jmpf` always come first

> ex: a = a \* a
> mov a, R0
> mul a, R0
> mov R0, a

[[Intermediate Code Generator Operators]]
### Example [Kenny Jingga Responsi 2024 (for)](https://youtu.be/6yRB6dszSUo?si=17tSLpRuHHSIfWLg&t=7108)  

![[Screenshot 2024-12-28 at 2.36.55 PM.png]]

1. mov #0, a `(int a = 0)`
2. mov #1, i `(i = 0)`
3. move i, R0 `(prep for operation, beginning of for loop) [R0 = i = 0]`
4. lt #10, R0 `(i < 10) [R0 = R0 < 10 = T/F]`
5. jmpf R0, [17] `(for loop condition is fale)`
6. mov i, R0 `(prep for operation, beginning of if statement) [R0 = i]`
7. mod #2, R0 `(i % 2) [R0 = R0 % 2]`
8. eq #0, R0 `(... == 0) [R0 = R0 == 0 = T/F]`
9. jmpf R0, [13] `if condition is false, go to increment in loop`
10. mov a, R0 `(prep for operation) [R0 = a]`
11. add i, R0 `(a + i) [R0 = a + i]`
12. mov R0, a `(a = a + i)`
13. mov i, R0  `(prep for operation) [R0 = a]`
14. 11. add #1, R0 `(i + 1) [R0 = i + 1]`
15. mov R0, i `(i = i + 1)`
16. jmp , [3] `(looping)`
17. ...

Status: #idea  
Tags:  [[compilation-techniques#Final Exam]]

---
# References