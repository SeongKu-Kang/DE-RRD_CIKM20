# DE-RRD: A Knowledge Distillation Framework for Recommender System

## 1. Overview
This repository provides the source code of our paper: DE-RRD: A Knowledge Distillation Framework for Recommender System, accepted in CIKM'20 as a full research paper.


In the paper, we propose two distillation methods:
1. Distillation Experts (DE) that distills the teacher's latent knowledge.

2. Relaxed Ranking Distillation (RRD) that distills ranking information from the teacher's predictions.

![oveview](https://user-images.githubusercontent.com/68782810/94357694-06ae0000-00d6-11eb-8ad4-9a389f99ee02.png)


## 2. Evaluation
### 2.1. Leave-One-Out (LOO) protocol
We provide the leave-one-out evaluation protocol used in the paper.
The protocol is as follows:
* For each test user
	1. randomly sample two positive (observed) items 
		- each of them is used for test/validation purpose.
	2. randomly sample 499 negative (unobserved) items
	3. evaluate how well each method can rank the test item higher than these sampled negative items.

### 2.2. Metrics
We provide three ranking metrics broadly adopted in the recent papers:  HR@N, NDCG@N, MRR@N.
The hit ratio simply measures whether the test item is present in the top-N list, which is defined as follows:

![Large](https://latex.codecogs.com/svg.latex?\text{H}%20@%20N%20=%20\frac%20{%201%20}%20{%20|%20\mathcal%20{%20U%20}_{test}%20|%20}%20\sum%20_%20{%20u%20\in%20\mathcal%20{%20U}%20_{test}%20}%20\delta%20\left(%20p%20_%20{%20u%20}%20\leq%20\text%20{%20top%20}%20N%20\right) )
 

where &delta; is the indicator function, U<sub>test</sub> is the set of the test users, p<sub>u</sub> is the hit ranking position of the test item for the user u. 
On the other hand, the normalized discounted cumulative gain and the mean reciprocal rank are ranking position-aware metrics that put higher scores to the hits at upper ranks.
N@N and M@N are defined as follows:

![Large](https://latex.codecogs.com/svg.latex?\text{N}%20@%20N%20=%20\frac%20{%201%20}%20{%20|%20\mathcal%20{%20U%20}%20_{test}%20|%20}%20\sum%20_%20{%20u%20\in%20\mathcal%20{%20U%20}_{test}%20}%20\frac%20{%20\log%202%20}%20{%20\log%20\left(%20p%20_%20{%20u%20}%20+%201%20\right)%20}\text{,%20M}%20@%20N%20=%20\frac%20{%201%20}%20{%20|%20\mathcal%20{%20U%20}_{test}%20|%20}%20\sum%20_%20{%20u%20\in%20\mathcal%20{%20U%20}%20_{test}%20}%20\frac%20{%201%20}%20{%20p%20_%20{%20u%20}%20})


## 3. Usage
A. For DE, run "main_DE.py"

B. For RRD, run "main_URRD.py"

We also provide the training log and the learning curve of each method. You can find them in /logs folder and the attached jupyter notebook.


## 4. Other Work
Please note that *Topology Distillation (KDD'21)*, which is a follow-up study of DE, is available in https://github.com/SeongKu-Kang/Topology_Distillation_KDD21.

Also, *IR-RRD (Information Sciences'21)*, which is a follow-up study of RRD, is available in https://github.com/SeongKu-Kang/IR-RRD_INS21.


## 5. Update
We found that the sampling processes for top-ranked unobserved items are unnecessary, and removing the processes gave considerable performance improvements for the ranking matching KD methods including RRD [CIKM'20], DCD [CIKM'21]. We provide more detailed explanation and experiment results on our new paper: Distillation from Heterogeneous Models for Top-K Recommendation [WWW'23].
