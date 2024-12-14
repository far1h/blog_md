> Expressed as quadruples: `Opr Arg1, Arg2, Store/result`

> If there is a while, add `jmpf` right away only

> `jmpf` always come first

[[Intermediate Code Generator Operators]]
### Example [Alvina Aulia Intermediate Code Generator](https://www.youtube.com/watch?v=2kNVq9TxEg0&ab_channel=AlvinaAulia)  

```
x := 1;
y := x + 10;
while (x<y) {
	x := x + 1;
	if (x % 2 == 1) then
		y := y + 1;
	else y := y - 2;
}
```

1. mov 1, , x `(x := 1)`
2. add x, 10, t1 `(x + 10)`
3. mov t1, , y `(y := ...)`
4. lt x, y, t2 `(x < y)`
5. jmpf t2, , [17] `(while ...)`
6. add x, 1, t3 `(x + 1)`
7. mov x, , t3 `(x := ...)`
8. mod x, 2, t4  `(x % 2)`
9. eq t4, 1, t5 `(... == 1)`
10. jmpf t5, , [14] `(if ...)`
11. add y, 1, t6  `(y + 1)`
12. mov t6, , y `(y := ...)`
13. jmp , , [17] `break`
14. sub y, 1, t7 `(y - 2)`
15. mov t7, , y `(y := ...)`
16. jmp , , [17] `break`
17. ... `remaining code`

Status: #idea  
Tags:  [[compilation-techniques#Final Exam]]

---
# References