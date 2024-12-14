##### steps
1. Look for [[Three Address Code (TAC)]]
2. Create [[Directed Acyclic Graph|DAG]] based on [[Three Address Code (TAC)|TAC]]

> From left to right  

> Don't repeat any nodes
### Example [Alvina Aulia Directed Acyclic Graph](https://www.youtube.com/watch?v=Kp7ZWn-G1X8&ab_channel=AlvinaAulia)  
1. x = a + a \* <u>(b - c)</u> + <u>(b - c)</u> \* d
			 T1          T1

2. x = a + <u>a * T1</u> +T1 \* d
		  T2

3.  x = a + T2 + <u>T1 * d</u>
				T3
	
4. x = <u>a + T2</u> + T3
	    T4  

5. x = <u>T4 + T3</u>
	    T5  

6. x = T5  

T1 = b - c  
T2 = a \* T1  
T3 = T1 \* d  
T4 = a + T2  
T5 = T4 + T3  
x = T5  

![[Screenshot 2024-12-09 at 1.06.21 PM.png]]
Status: #idea  
Tags:  [[compilation-techniques#Final Exam]]

---
# References