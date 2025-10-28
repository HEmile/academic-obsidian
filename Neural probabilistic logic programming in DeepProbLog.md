---
aliases:
  - MANHAEVE2021103504
  - DeepProbLog
year: 2021
hasTopic:
  - "[[neurosymbolic learning]]"
  - "[[probabilistic circuits]]"
  - "[[probabilistic logics]]"
author:
  - "[[Robin Manhaeve]]"
  - "[[Sebastijan Dumančić]]"
  - "[[Angelika Kimmig]]"
  - "[[Thomas Demeester]]"
  - "[[Luc De Raedt]]"
project: []
publishedIn: "[[AI Journal]]"
citeKey: MANHAEVE2021103504
zoteroUri: zotero://select/items/@MANHAEVE2021103504
url: https://www.sciencedirect.com/science/article/pii/S0004370221000552
---

> [!abstract]-
> We introduce DeepProbLog, a neural probabilistic logic programming language that incorporates deep learning by means of neural predicates. We show how existing inference and learning techniques of the underlying probabilistic logic programming language ProbLog can be adapted for the new language. We theoretically and experimentally demonstrate that DeepProbLog supports (i) both symbolic and subsymbolic representations and inference, (ii) program induction, (iii) probabilistic (logic) programming, and (iv) (deep) learning from examples. To the best of our knowledge, this work is the first to propose a framework where general-purpose neural networks and expressive probabilistic-logical modeling and reasoning are integrated in a way that exploits the full expressiveness and strengths of both worlds and can be trained end-to-end based on examples.

Uses a [[logic program]] annotated with probabilities (that can also come from neural networks). The proofs of a query from a logic program are then compiled into [[probabilistic circuits]] for exact inference. 
![[Pasted image 20251028163856.png]]
![[Pasted image 20251028164004.png]]

--- 
#source/paper