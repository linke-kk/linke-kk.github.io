---
layout: default
title: Data Science:Mining Patterns
---
# Mining Patterns
## Terminologies
- Alphabet: a set of items
- Transaction: a set of items involved in an activity

## Proofs
### For every frequent itemset, its subset is also frequent.
Definitions: \
$$Def_p$$:$$P(A)=\frac{count(D_A)}{count(D)}$$, where $$D$$ is a set of all the transactions in the databse, $$D_A$$ is a set of all the transactions in the database that contain $$A$$   
$$Def_{frequent}$$:$$frequent(I)$$ means: $$P(I)\ge min\_sup$$  

Lemmas+Axioms: What does this mean? \
Proof Goal:  
$$\forall A \subseteq I. frequent(I) \Rightarrow frequent(A)$$  
Steps:  
1. $$\forall A \subseteq I. frequent(I) \Rightarrow frequent(A)$$  
   Pick any itemset $$A, I$$, where $$A \subseteq I$$, and...  
   1.1 $$frequent(I) \Rightarrow frequent(A)$$  
       Assume $$frequent(I)$$, and...  
       1.1.1 $$count(D_A) \le count(D_I)$$  
           1.1.1.1 $$D_I \subseteq D_A$$  
               1.1.1.1.1 $$\forall T \in D_I, T \in D_A$$  
                   Pick any transaction $$T \in D_I$$, and...  
                   1.1.1.1.1.1 $$I \subseteq T$$  
                   1.1.1.1.1.2 $$A \subseteq T$$  
                       $$Transitivity_{\subseteq}$$, 1.1.1.1.1.1, and 1  
                   1.1.1.1.1.3 $$T \in D_A$$  
           1.1.1.2 $$count(D_A) \ge count(D_I)$$  
                   subset property(which?) and 1.1.1.1  
        1.1.2 $$P(A) \ge P(I)$$  
            $$Def_p$$ and 1.1.1  
        1.1.3 $$P(I) \ge min\_sup$$  
            $$Def_{frequent}$$ on the assumption of 1.1  
        1.1.4 $$P(A) \ge min\_sup$$  
            $$Transitivity_{\geq}$$, 1.1.2, and 1.1.3  
        1.1.5 $$frequent(A)$$  
            $$Def_{frequent}$$ with 1.1.4  



