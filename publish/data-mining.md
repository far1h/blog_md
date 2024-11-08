---
title: Data Mining
---
- [ ] [[data-mining-uts-quiz]]

[[kdd| knowdledge discovery in databases]]

[[data-warehousing]]

[[schema]]
![[dm-1.png|400]]  
![[dm-2.png|400]]  
![[dm-3.png|400]]  

## Apriori Algorithm 
![[associationrulesmetrics.png|400]]  

### Step 1: Count Distinct Items
![[apriori1.png|400]]  
![[apriori2.png|400]]  
![[apriori3.png|400]]  
![[apriori4.png|400]]  
### Step 2: Identify Association Rules
![[apriorisubset.png|400]]  
![[apriorirule1.png|400]]  
![[apriorirule2.png|400]]  
![[apriorirule3.png|400]]  
## FP Growth Algorithm
### Step 1: Count Distinct Items
![[fpgrowth1.png|400]]  
### Step 2: Rearrange Items based count in descending order
![[fpgrowth2.png|400]]  

### Step 3: Make FP Growth Tree
1. Make Null Root Node 
2. And make children sequentially
![[fpgrowth3.png|400]]    
![[fpgrowth4.png|400]]  
![[fpgrowth5.png|400]]    
![[fpgrowth6.png|400]]   
![[fpgrowth7.png|400]]  
![[fpgrowth8.png|400]]  
![[fpgrowth9.png|400]]  
![[fpgrowth10.png|400]]  
![[fpgrowth11.png|400]]  
![[fpgrowth12.png|400]]  

### Step 4: Make Table 


| Ending with | Paths | Count of each item in path | Candidate itemset with count | Frequent itemset |
| ----------- | ----- | -------------------------- | ---------------------------- | ---------------- |
|             |       |                            |                              |                  |
  

#### Examples:

![[fptable.png|400]]  
![[fptable2.png|400]]  
![[fptable3.png|400]]  
![[fptable4.png|400]]  

### Step 5: Make association rules
![[fptable5.png|400]]  

hmm