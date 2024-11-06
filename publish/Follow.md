character after the first character in the **non terminal values**

Ex: 
<u>A</u>bc = b 
A + b = +
ADE = ...

## Algorithm
1. If $S$ is the start symbol, 
   ex: $S$ -> $Ab$ | $c$, then $ is the Follow value of $S$
2. If $A$ -> $\alpha B\beta$, then all First of $\beta$ is the First of $B$
3. a. $A$ -> $\alpha B$, then all follow $A$ is the Follow of $B$
3. b. $A$ -> $\alpha B\beta$ <u>and</u> first of $\beta$ is $\varepsilon$, then all Follow of A is the Follow of $B$