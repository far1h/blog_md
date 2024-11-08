---
title: Data Mining
---
- [ ] quiz

![[dm-1.png]]
![[dm-2.png]]
![[dm-3.png]]

## FP Growth
## Step 1: Count Distinct Items
![[fpgrowth1.png]]
## Step 2: Rearrange Items based count in descending order
![[fpgrowth2.png]]

## Step 3: Make FP Growth Tree
1. Make Null Root Node 
2. And make children sequentially
![[fpgrowth3.png]]![[fpgrowth4.png]]![[fpgrowth5.png]]![[fpgrowth6.png]]![[fpgrowth7.png]]![[fpgrowth8.png]]![[fpgrowth9.png]]![[fpgrowth10.png]]![[fpgrowth11.png]]![[fpgrowth12.png]]

## Make Table 


| Ending with | Paths | Count of each item in path | Candidate itemset with count of each w. r. t. transaction table | Frequent itemset |
| ----------- | ----- | -------------------------- | --------------------------------------------------------------- | ---------------- |
|             |       |                            |                                                                 |                  |
![[fptable.png]]![[fptable2.png]]![[fptable3.png]]![[fptable4.png]]![[fptable5.png]]