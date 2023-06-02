

Can R2 be greater than 1?
- The value greater than 1 can be calculated if the equation of R2 for linear model is applied to non-linear model. The result is thus non-sense. See the thread [Can R2
be greater than 1?](https://stats.stackexchange.com/questions/334004/can-r2-be-greater-than-1).
- R2 reflects the portion of the variation of Y explained by X via the model. See [Avoid R-squared to judge regression model performance](https://towardsdatascience.com/avoid-r-squared-to-judge-regression-model-performance-5c2bc53c8e2e), and it says Use [prediction interval](https://medium.com/towards-data-science/confidence-interval-vs-prediction-interval-what-is-the-difference-64c45146d47d) instead.


Prediction interval
- See [Confidence Interval vs Prediction Interval: What is the Difference?](https://medium.com/towards-data-science/confidence-interval-vs-prediction-interval-what-is-the-difference-64c45146d47d)
- For non-linear model, use bootstrap for calculating prediction interval
  > ChatGPT's answer for how to do: 
  > 1. Fit the non-linear regression model: Use an appropriate method or software to fit the non-linear regression model to your data and obtain the estimated parameters.
  > 1. Generate bootstrap samples: Create a large number (e.g., 1000) of bootstrap samples by randomly sampling with replacement from the original dataset. Each bootstrap sample should have the same size as the original dataset.
  > 1. Perform model fitting for each bootstrap sample: For each bootstrap sample, fit the non-linear regression model and obtain the estimated parameters.
  > 1. Generate predictions for each bootstrap sample: Use the estimated parameters from each bootstrap sample to generate predictions for the specific x value(s) of interest.
  > 1. Calculate prediction intervals: For each x value of interest, collect the corresponding predictions from all bootstrap samples. Sort the predictions and use percentiles to calculate the lower and upper bounds of the prediction interval. The percentiles used will depend on the desired confidence level (e.g., for a 95% prediction interval, you would use the 2.5th and 97.5th percentiles).
  > 1. Report the prediction interval: Finally, report the lower and upper bounds of the prediction interval for each x value of interest.

Bagging in Random forest applies bootstrap:
- Here is [Why Bootstrapping Actually Works?](https://medium.com/towards-data-science/why-bootstrapping-actually-works-1e75640cf172)
- Bagging is [**B**ootstrap and **Agg**regat**ing**](https://medium.com/@sly.of.zero/decision-trees-bootstrap-aggregating-and-bagging-8c6cf764e689). In this article, it mentions **Boosting**, another ensemble technique

[Gradient Boosted Decision Tree](https://towardsdatascience.com/gradient-boosted-decision-trees-explained-9259bd8205af)
- trees in sequence with a later tree learn from previous error
- more accurate than bagging but prone to overfitting and sensitive to outliers

Julia packages for boosted tree, EvoTrees:
- https://github.com/Evovest/EvoTrees.jl
- https://evovest.github.io/EvoTrees.jl/dev/