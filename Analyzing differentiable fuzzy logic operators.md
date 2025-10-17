---
aliases:
  - VANKRIEKEN2022103602
  - differentiable fuzzy logic
  - DFL
  - Sigmoidal implication
  - differentiable logic
year: 2022
hasTopic:
  - "[[fuzzy logic]]"
  - "[[neurosymbolic learning]]"
author:
  - "[[Emile van Krieken]]"
  - "[[Erman Acar]]"
  - "[[Frank van Harmelen]]"
project:
  - "[[How to properly use fuzzy logics in Neurosymbolic AI]]"
publishedIn: "[[AI Journal]]"
citeKey: VANKRIEKEN2022103602
zoteroUri: zotero://select/items/@VANKRIEKEN2022103602
url: https://www.sciencedirect.com/science/article/pii/S0004370221001533
---

> [!abstract]-
> The AI community is increasingly putting its attention towards combining symbolic and neural approaches, as it is often argued that the strengths and weaknesses of these approaches are complementary. One recent trend in the literature is weakly supervised learning techniques that employ operators from fuzzy logics. In particular, these use prior background knowledge described in such logics to help the training of a neural network from unlabeled and noisy data. By interpreting logical symbols using neural networks, this background knowledge can be added to regular loss functions, hence making reasoning a part of learning. We study, both formally and empirically, how a large collection of logical operators from the fuzzy logic literature behave in a differentiable learning setting. We find that many of these operators, including some of the most well-known, are highly unsuitable in this setting. A further finding concerns the treatment of implication in these fuzzy logics, and shows a strong imbalance between gradients driven by the antecedent and the consequent of the implication. Furthermore, we introduce a new family of fuzzy implications (called sigmoidal implications) to tackle this phenomenon. Finally, we empirically show that it is possible to use Differentiable Fuzzy Logics for semi-supervised learning, and compare how different operators behave in practice. We find that, to achieve the largest performance improvement over a supervised baseline, we have to resort to non-standard combinations of logical operators which perform well in learning, but no longer satisfy the usual logical laws.

Studies the properties and performance of several fuzzy logics, such as the [[product t-norm]] and the [[Lukasiewicz t-norm]].

In this paper, I introduced the concept of a **differentiable (fuzzy) logic**, and also introduced **sigmoidal implications**, which use a [[sigmoid]] transformation to ensure a smoothened, not-quite-fuzzy implication remains in $[0, 1]$. 

The work introduces useful theory, but could use more extensive (and modernised) experiments. 

--- 
#source/paper