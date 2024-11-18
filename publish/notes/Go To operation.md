Steps:
1. Make sure that one grammar has only 1 production result by removing the `OR` (essentially splitting the grammar)
2. Add augmented grammar (added grammar than can result a start symbol) `?????`
3. Add numbers to each grammar except augmented grammar
4. Add `.` at the front of each production result (used for kernel method)
5. Use the kernel method starting from the top most grammar
	1. Group the grammars
	2. Input the thing after the `.` to each grammar and group them
	3. If the result has a `.` before a variable, copy paste the variable producers from i0 and continue to check the grammars of the new group if there is a `.` before a variable
	4. If the group contains same exact grammars as previous groups label as the same group

> the goal is to make the `.`  at the front move to the back 



Status: #idea  
Tags:  [[compilation-techniques#Final Exam]], [[Bottom Up Parsing]]  

---
# References
