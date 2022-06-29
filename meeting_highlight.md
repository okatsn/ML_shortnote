# Highlight of inside meeting

- 農業需求: 10公尺尺度的土壤溼度預測


## Insights
以平穩過程為目標
- 以差值(diff)去趨勢、使得 ACF (autocorrelation function) 展現低記憶效應($t_{n=i}$ 與 $t_{n=i-1, i-2, ...}$的關連性隨$n$增加很快地降低)
- 取 $\log$

Time shift
- use ACF (AutoCorrelation Function) to decide $t_{i, i=-1,-2, \text{or }?...}$


### Granger Causality test
Check whether a feature (e.g., precipitation) is a effective "cause"
- for precipitation, yes
- `soil_water_content_t-1` seems not able to predict `soil_water_content_t0`

### ideas or keywords that may or may not be helpful
- Confusion Matrix & Statistics: To see the importance of features (factors)
- use CNN $\rightarrow$ heatmap to view target feature
- [CNN attention transformer](https://hackmd.io/@abliu/BkXmzDBmr)
- [Boruta: feature selection algorithm](https://towardsdatascience.com/boruta-explained-the-way-i-wish-someone-explained-it-to-me-4489d70e154a); [PyCall BorutaPy and Shapley values ShapML.jl](https://discourse.julialang.org/t/boruta-algorithm/76821)


## Earthquake prediction
- use AI to find what featrue relates to earthquake
- AI may support/prove whether final seismic size is deterministic by the first few seconds
- whether an earthquake is a foreshock of a bigger one


# TO-DOs
TODO: try `SWC_30cm` of site Tower (continue from `decisiontree_20220527/SET_Tower_30cm`)
TODO: test whether 5-day accumulated precipitation helps prediction in `SWC_30cm`

### TODO: For NEXT report
- plot learning_curve! with number of trees (for random forest); heatmap of performance for two hyper-parameter (e.g. `n_subfeatures` v.s. `bagging_fraction`);see [this](https://juliaai.github.io/DataScienceTutorials.jl/getting-started/ensembles-2/).


### TODO: Try these features
- try `no_rain_hour_t0`; test `precipitation_2day` and `precipitation_3day` without time-shift (there seems no requirement to shift them)
- averaged temperature as input variable
- wind speed
- solar radiation
- use calculated (not observed) `SWC_10cm` as input feature to predict `SWC_30cm`

### TODO: Try model composition
- one model for absolute SWC nowscast, one for predicting SWC increment
- one model that learns from the data of the entire year (or season); one for the recent month

### TODO: better imputation
- it is OK to impute data in testing phase with mean
- for training dataset, after series to supervised, delete all rows that has missing value; `series2supervise` has to allow missing (or NaN) 


### todo: less important
- record the necessary information about series-to-supervised process that we can restore `Xtrain`,`Xtest`,`ytrain`,`ytest` from input features' name (and its order) from the original data.
