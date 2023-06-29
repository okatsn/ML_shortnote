[TOC]

[Machine learning using Julia by Yuehhua](https://yuehhua.github.io/2021/03/28/the-future-of-julialang/)

[用Julia研究人工智能？這5個機器學習項目不得不看](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/728907/)

# MLJ
Getting start
https://alan-turing-institute.github.io/MLJ.jl/stable/getting_started/#Getting-Started


https://towardsdatascience.com/part-ii-using-a-decision-tree-ddffa4004e47

## Model tuning
Start up: https://juliaai.github.io/DataScienceTutorials.jl/getting-started/model-tuning/

[A `DeterministicTunedModel` example for decision tree regressor](https://alan-turing-institute.github.io/MLJ.jl/dev/tuning_models/)


### Feature selector
https://github.com/alan-turing-institute/MLJ.jl/issues/521

### Multi-threading
[JULIA_NUM_THREADS in VS Code (Windows 10 + WSL)](https://discourse.julialang.org/t/julia-num-threads-in-vs-code-windows-10-wsl/28794/13)

- Add `"julia.NumThreads": "auto"` to `"settings.json"` [(julia auto detecting max threads)](https://discourse.julialang.org/t/julia-num-threads-in-vs-code-windows-10-wsl/28794/13)
- Add kwarg in `TunedModel` (`TunedModel(; acceleration = MLJ.CPUThreads())`); also see: https://alan-turing-institute.github.io/MLJ.jl/dev/acceleration_and_parallelism/
  - there is also a `acceleration_resampling` kwarg

### Customize measure functions
Implementation detail: Internally, every measure is evaluated using the syntax

```julia
MLJ.value(measure, ŷ, X, y, w)
```

The simplest form is `mymeasure(y_hat, y)`; in which 
- Weight `w` is optional. 
- `X` is a named-tuple with field `x` and `penalty`. 
- For more information, see https://alan-turing-institute.github.io/MLJ.jl/stable/performance_measures/

You can also assign multiple measures
see https://alan-turing-institute.github.io/MLJ.jl/stable/evaluating_model_performance/

In tuning, scores are maximised, while losses are minimised. 
- By default, the orientation is `:loss`
- https://alan-turing-institute.github.io/MLJ.jl/dev/tuning_models/#Specifying-a-custom-measure


# Algorithm
## SVM
### Kernel functions
Please read this and the references therein: https://zhuanlan.zhihu.com/p/135898326
附實作： https://www.cnblogs.com/volcao/p/9465214.html


## Tree
[經典演算法詳解–CART分類決策樹、迴歸樹和模型樹](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/564323/)

[The Complete Guide to Decision Tree Analysis (with history)](https://www.explorium.ai/blog/the-complete-guide-to-decision-trees/)

## LSTM using Julia
[Basic Sentiment Analysis with Julia using LSTM](https://emoryraphael.medium.com/basic-sentiment-analysis-with-julia-using-lstm-e12d4754ee6b)

[Flux.jl: Recurrent Models](https://fluxml.ai/Flux.jl/stable/models/recurrence/)

# Algorithm - unsupervised learning
Resources that might be useful:
- https://juliaai.github.io/DataScienceTutorials.jl/getting-started/composing-models/#declaring_a_pipeline

# API
以下是可以用來建立 API 的 julia 套件
https://github.com/JuliaWeb/HTTP.jl
https://github.com/ndortega/Oxygen.jl
https://github.com/GenieFramework/Genie.jl
https://github.com/neomatrixcode/Merly.jl
https://github.com/wookay/Bukdu.jl
https://github.com/JuliaWeb/JuliaWebAPI.jl
我之前貼的參考資料，它是利用 HTTP.jl 建立API
https://ncu-aiworkspace.slack.com/archives/C0344KXQK28/p1645776794658099

3:43
這篇對前後端有簡單解釋，可了解基礎概念
https://www.yuanlin.dev/posts/626d253734fa51e8b0764add


# Other materials on Slack by Zk
以下文章介紹使用機器學習進行時間序列預測的任務，以及如何避免一些常見的陷阱。提供給各位參考。
https://www.kdnuggets.com/2019/05/machine-learning-time-series-forecasting.html
https://www.kdnuggets.com/2020/03/machine-learning-time-series-forecasting-sequel.html


已由 葉政凱 釘選
10:38
時序資料分析/預報
https://otexts.com/fpp2/
https://online.stat.psu.edu/stat510/


葉政凱  下午 4:13
Julia Computing 的網絡研討會，End-to-End Machine Learning Workflow Using Julia 的教材
https://www.youtube.com/watch?v=dzChtn9WWT8
https://github.com/JuliaComputing/ScoringEngineDemo.jl (已編輯) 


葉政凱  上午 11:23
使用神經網路進行時序預測
https://machinelearningmastery.com/how-to-develop-convolutional-neural-network-models-for-time-series-forecasting/
https://medium.com/analytics-vidhya/time-series-prediction-feat-introduction-of-julia-78ed6897910c
https://www.analyticsvidhya.com/blog/2021/02/using-multiple-features-in-time-series-prediction-with-cnn-gru/
https://github.com/sdobber/FluxArchitectures.jl

