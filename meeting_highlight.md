# Highlight of inside meeting

- 農業需求: 10公尺尺度的土壤溼度預測


## Insights
以平穩過程為目標
- 以差值(diff)去趨勢、使得 ACF (autocorrelation function) 展現低記憶效應($t_{n=i}$ 與 $t_{n=i-1, i-2, ...}$的關連性隨$n$增加很快地降低)
- 取 $\log$


### ideas or keywords that may or may not be helpful
- Confusion Matrix & Statistics: To see the importance of features (factors)
- use CNN $\rightarrow$ heatmap to view target feature
- [CNN attention transformer](https://hackmd.io/@abliu/BkXmzDBmr)
- [Boruta: feature selection algorithm](https://towardsdatascience.com/boruta-explained-the-way-i-wish-someone-explained-it-to-me-4489d70e154a); [PyCall BorutaPy and Shapley values ShapML.jl](https://discourse.julialang.org/t/boruta-algorithm/76821)


## Earthquake prediction
- use AI to find what featrue relates to earthquake
- AI may support/prove whether final seismic size is deterministic by the first few seconds
- whether an earthquake is a foreshock of a bigger one