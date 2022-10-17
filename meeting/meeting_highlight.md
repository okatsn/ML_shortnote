[TOC]

[TOC]

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


## Log
#### 2022-08-22
Highlight
- the most dominant predictor (i.e., `precipitation_1d_t0`)
- study relevance between depth and time scale (include time lag & accumulating time)
- we had debates on coarse graining, and there is still no conclusion yet (and the issue is halt that temporary I need to do nothing)

Insights
- what if we exclude the most dominant predictor (i.e., `precipitation_1d_t0`)?
- how does the key features the model (tree) tell us links to parameters in the hydrological model (precipitation as a function of time ↔️ `precipitation_1d_t0`, `_t-1`, `_t-2`...)

#### 2022-09-12 For publication to a journal 

Solely from data, the tree structures (statistics of node labels) can tell the mechanism of physical world
- the link between trained trees and the existing soil-hydrological model
- e.g., If `X_t0`, `X_t-1` are dominant at nodes close to the root, we may expect the differentiation of `X` is critical to a soil-hydrological model.
- can the tree structures tells something more beyond existing model?

Does a tree that performs bad in testing have a unreasonable/illed tree structure?
Does a tree of bad performance in testing have a different statistics of node labels comparing with a tree of good performance?
At the depth of 10cm, root label is dominant by `precipitation_1d`; can we see the result from those at depth of 100cm that root label is dominant by `precipitation_more_than_1d`?

According to the learning curve of feature sets based on ARI data, depth of 50cm is clearly a transition that MAE at every feature set (#1 to #12) is almost the same. Does this implies that there is a physical boundary at 50cm?
- [ ] ask 許家寅 for the core.

Guidelines (move to the manuscript repository)
- 以圖和表格整理盤點既有成果
- 先就資料完整的部分準備文章
- 截至目前為止，僅討論時間面。空間維度(深度)相關方面皆未涉。

Do-it-later
- 資料缺失與否的影響分析

Also see
- TWAI土壤水內部_吳宗羲_20220818_007Af.pptx





#### 2022-10-12
##### 期中報告審查要點
- 是否將預測結果公開
- 為何使用此技術、帶來什麼改變? 
  > Ans: 計算速度短，可即時、針對大量目標預測。
- 希望在來年看到容許度的提升。

##### 蒸發散模式
![](eq_penmanmonteith.png)
- 根據輻射、濕度、風速等推算蒸發散
- 建立在無雨的狀況假設下

##### Tolerance ("5% 假設")
"猜錯的話可撐多久"：預測誤差的水量在實際應用場景的緩衝時間是多少
- 假設以下場景：SWC 低至20% 再澆水；15% 開始枯死；5% 水量可供稻米用5天。目前預測值是25%，真值20%，那容許度為5天。(大概是這樣的感覺)
- 之前定陳沛芫老師訂定的 "目標誤差低於5%" 就是在這個邏輯下計算得到的。

"5% 假設"的基礎 (陳沛芫/line/2022-10-15)
- 假設草地每天蒸發散量是5mm
- 若最嚴重情況下，土壤水份只剩凋萎點以上5mm時，預測誤差5%*100mm土厚=5mm，日尺度預測誤差5%即可能避免植物從水份充足至枯萎之上限 ("少一天提早儲水(讓植物不要枯萎)的影響程度"--2022-3-17)
- 水稻田蒸發散可能每天0.1-6.5mm，6.5mm/土厚假設100mm，日尺度預測誤差6.5%即可能避免作物從水份充足至枯萎之上限

前述基礎的外推 (陳建志/line/2022-10-15)
- 深度10 cm ，預測誤差 3% (SWC) 則大約兩天該澆灌沒澆灌之容忍期。
- 日尺度: 一日的澆灌作業容忍期

##### 點子
- 目標預測 $t_{+n}$ SWC。
- 以降雨為主的變數預測 $t_0$ 土水絕對值 $Y_{p, t0}$。(`mach_a`)
- 以蒸發散模式變數預測 $t_0$ 至 $t_{+n}$ 土水增值 $\Delta Y_{p, t0n}$。(`mach_b`)
- 直接預測 $t_{+n}$ 土水絕對值 $Y_{p, tn}$。(`mach_ax`)
- 預測未來區間內 ($t_0$至 $t_n$)會不會下雨。(`mach_NN`)
  - Yes ➡️ use `mach_ax`: $Y_{pred} = Y_{p, tn}$
  - No  ➡️ use `mach_a` + `mach_b`: $Y_{pred} = Y_{p, t0} + \Delta Y_{p, t0n}$