[TOC]


## Decision tree
[Main idea](https://blog.clairvoyantsoft.com/entropy-information-gain-and-gini-index-the-crux-of-a-decision-tree-99d0cdc699f4)
- information regarding the target feature
- making the resultant node as pure as possible

### The measure of informativeness (for categorical decision tree)
"A feature that best separates the uncertainty from information about the target feature is said to be the most informative feature. "

#### Entropy and Information gain
Entropy is used to measure the impurity or randomness of a dataset.

$$
Entropy(x) = -\sum \underbrace{P(x=k)}_{\text{``weight''}} \underbrace{\log_2 P(x=k)}_\text{Shannon Entropy}
$$

- $P(x=k)$: The probability that a target feature takes a specific value, $k$.
- $\log_2 P(x=k)$: The entropy of each possible target value.

Information Gain:

$$
\text{InformationGain(feature) = Entropy(Dataset) - Entropy(feature)}
$$

- "Then, we subtract this value from the originally calculated entropy of the dataset to see how much this feature splitting reduces the original entropy"
- "The feature with the largest information gain should be used as the root node to start building the decision tree."
- "ID3 algorithm uses information gain for constructing the decision tree."

### (for regression decision tree)
 [For continuous features the mean of each two consecutive values (ordered from lowest to highest) of the training data are used as possible thresholds.](https://towardsdatascience.com/decision-trees-explained-3ec41632ceb6)


### Stop conditions
- [maximum depth of the tree, minimum samples in leaf nodes, or minimum reduction in the error metric](https://towardsdatascience.com/decision-trees-explained-3ec41632ceb6)

## General Introduction
Now reading: 
https://wiki.pathmind.com/neural-network



## 決策樹簡述
相對於多數的機器學習與深度學習演算法，決策樹的樹狀結構令其具有較高的可解釋性（過深的決策樹可能仍難以進行解釋），且決策樹具有運行速度快、可處理連續的優點。


**決策樹的樹狀結構**
- 根節點 (root node)
- 內部節點 (internal node)
- 葉節點 (leaf node)

**分類樹**
- ID3 (Iterative Dichotomiser 3) (Quinlan 1986)
- C4.5 (successor of ID3) (Quinlan 1993)
- CART (Classification And Regression Tree) (Breiman et al. 1984)
- Conditional Inference Trees (CTree) (Hothorn et al. 2006)

**回歸樹**
- Chi-square automatic interaction detection (CHAID)
- CART (Classification And Regression Tree) (Breiman et al. 1984)
- Multivariate adaptive regression spline (MARS) (Friedman 1991)
- Conditional Inference Trees (CTree) (Hothorn et al. 2006)



## 分類和回歸樹(Classification And Regression Tree, CART)說明
分類和回歸樹的分支過程最多產生兩個分支，因此當樹的深度為n層時，決策樹最多具有$2^n$個的葉節點。

實作上用於評估切分的準則，分類任務可以使用gini index(又稱gini impurity)或entropy；回歸任務可以使用MSE、MAE等。
> DecisionTree.jl 是使用 entropy 和 MSE



## 參考網頁
- https://en.wikipedia.org/wiki/Decision_tree_learning
- https://ithelp.ithome.com.tw/articles/10271143
- https://zhuanlan.zhihu.com/p/82054400
- https://scikit-learn.org/stable/
- https://www.youtube.com/watch?v=I8pXQC7i6Fk