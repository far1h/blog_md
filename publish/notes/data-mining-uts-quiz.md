---
title: Pre UTS quiz for Data Mining
excerpt: question and answer for Henry Lucky DM UTS Quiz
---
![[quiz1-2.png|300]]

```
2. Operational databases are the perfect example for OLTP (Online Transaction Processing) and data warehouses are for OLAP (Online Analytical Processing). This means that while operational databases handles day-to-day operations and are optimized for frequent updates, data warehouses are only limited to the storing large amounts of historical data, are optimized for complex queries, and are used for analysis instead of updates. The data warehouses will store the day-to-day updating data collected from the operational databases, and then proceeds on analyzing for patterns.
```

![[quiz3.png|300]]

```

```

```
approval range
```

![[quiz4.png|300]]

```
4a.
region: nominal its categorical and has no ordering
phLevel & temp: interval since no true zero point, diff between value makes sence but ratio doesnt
contaminat: ratio since tehre is a true zero point, diff between value and ratio makes sense
```

```
4b. 
if not too many outliers, drop row
else
	replace with mode
	replace with mean or median
	replace with ML predicted values
```

![[quiz5.png|300]]

```
5a. 
Apples = 3
Bananas = 3
Bread = 2
Oranges = 2
Milk = 2

Apple, Bananas = 2 ✅
Apple, Bread = 1
Apple, Organges = 1 
Apple, Milk = 1
Bananas, Bread = 0
Bananas, Oranges = 1
Bananas, Milk = 1
Bread, Oranges = 1
Bread, Milk = 1
Oranges, Milk = 0

Therefore, the frequent pattern in grocery transaction :
{(Apple, Bananas)}
```

```
5b.
Apples -> Bananas = supp(Apples, Bananas) / supp(Apples)
									= 2/3 * 100%
									= 66%
									
Bananas -> Apples = supp(Bananas, Apples) / supp(Bananas)
									= 2/3 * 100%
									= 66%

The strong association rules based on the frequent patterns found in a.
are Apples -> Bananas and Bananas -> Apples.
```

Status: #idea
Tags: [[data-mining]]

---
# References
