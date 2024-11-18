---
title: rules for creating SLR Table
---
> Rows are the number of groups that have ex:  i0-ix

> Columns are all the symbols, terminals, and variables  

> If the input is a **variable**, input the number of the group it results to 

> If input is a **terminal or symbol**, do the same as variable but add `S` before the number

> If there is a **grammar that is completed** (`.` is at the end) and is **an augmented grammar**, put accepted in the dollar column   

> If its **complete and NOT augmented grammar** , check i0 which line does it correspond to, and use `R + line number` as the value for the [[Follow]] values of the producer variable 

> If [[Go To operation]] is wrong, table is wrong

how to check?? 

Status: #idea  
Tags:  [[compilation-techniques#Final Exam]], [[Bottom Up Parsing]]  

---
# References
