[TOC]

# Interpretable machine learning

## e-Book: Interpretable Machine Learning
> [A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/) *by* Christoph Molnar
> [中文版](https://medium.com/ai-academy-taiwan/%E5%8F%AF%E8%A7%A3%E9%87%8B-ai-xai-%E7%B3%BB%E5%88%97-shap-2c600b4bdc9e)

### Shapley value

The Shapley value of feature $j$; a.k.a. the **contribution to the payout**:
$$
\phi_j (val) = \displaystyle\sum_{S \subseteq \{1,2,...,p\}\backslash\{j\}} \frac{|S|!(p-|S|-1)!}{p!}( val (S \cup \{j\}) - val(S)),
$$
where the value function is the 

$$
val_x(S) = \displaystyle\int \hat{f} (x_1, x_2, ...,x_p) d\mathbb{P}_{X\notin S} - \mathbb{E}_X (\hat{f}(X))
$$

In this equation, $S$ is a possible subset of the set without $j$. For example, for $\{1,2,3,4,...,p\} \backslash {4} = \{1,2,3,5,6,...,p\}$, $S$ are all possible subsets: $S = \{1\}, \{1,2\}, \{1,3\},\{2,3\},\{1,2,3\},\{1,2,3,5\},...,\{1,2,3,5,...,p\}$.
On the other hand, $S \cup \{j\}$ is a subset with $j$, whereas $S$ is the same subset but without $j$. 
$|S|$ is simply the number of elements in $S$; see [this](https://www.quora.com/What-is-the-absolute-value-of-a-set).
$val (S \cup \{j\}) - val(S)$ is sometimes called *marginal contribution*.

$\hat{f}$ is the model where $\hat{f}(x_1, x_2, ..., x_p)$ gives the prediction based on a set (a "row" in table) of input features $x_1, x_2, ..., x_p$. As we cannot simply exclude certain features, in practice the feature values NOT in the subset $S$ is sampled from empirical distribution, as demonstrated in the following example.

The **value function** (know as the **payout function** for coalitions of players) gives the **contribution to the prediction** from a certain combination of participated features alone, for example, 
$$
val_x(S) =val_x(\{1,3\}) = \displaystyle\int \hat{f} (x_1, X_2, x_3,X_4) d\mathbb{P}_{X_2, X_4} - \mathbb{E}_X (\hat{f}(X))
$$
where $x_{i\in S}$ is the measured value of a feature *in* $S$ (e.g., `air_temperature=20.5, humidity=0.3, ...` at time $t$), and $X_{k\notin S}$ denotes the random variable of a feature *not in* $S$; the integration over the probability density space of $X_2$ and $X_4$ is in practice the summation of the predicted values of model using only the observed value of feature 1 and 3 with the value of feature 2 and 4 "in the same row" replaced by random number generated according to the corresponded empirical distribution.

According to these equations, considering a table of of data with columns as features $x_1, x_2, ...,x_p$:
- the Shapley value of the value of $j_{th}$ feature in row $n$ (e.g., `air_temp = df[n, j]=20.5`), $\phi_j (val_{x}^{(n)})$, is the contribution of feature $j$ that makes actual prediction (the predicted value by model using row $n$ as input; $y^{(n)}$) deviates from average prediction (over the entire table).
- the summation of Shapley values of all features in row $n$ should approximates (theoretically equals) the difference between actual prediction $y^{(n)}$ and the average prediction.
- 
- we CANNOT calculate Shapley value if there is only "a row of data" for a single prediction; instead, we must have "a table" of input features in order to allow $\int\hat{f}d\mathbb{P}_{X\notin S}$, as $X$ are random variables. See the **Disadvantage** section in [A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/).
- we CAN have the feature importance (contribution) of a certain feature value (e.g., `air_temperature=20.5` at row $n$); that is, for each row 
- The Shapley value allows **contrastive** explanations. You can compare a prediction to the average prediction of the entire dataset, or only a subset of the dataset.
- The Shapley value of a feature value is **not the difference of the predicted value** after removing the feature from the model training. The interpretation of the Shapley value is: Given the current set of feature values, the contribution of a feature value to the difference between the actual prediction and the mean prediction is the estimated Shapley value.

equals zero (to the average prediction value) if the case with or without feature $j$ makes no difference.  <!-- # makes no difference to what? -->
#### Visualization tools
[eXplainable AI (XAI)](https://towardsdatascience.com/explainable-ai-xai-lime-shap-two-great-candidates-to-help-you-explain-your-machine-learning-a95536a46c4e)
Shapley value
- Variable importance plot: A horizontal bar plot showing the importance of features as mean absolute Shapley value.
- Summary plot: Categorical scatter plot, showing contribution (positive or negative) of individual value of each feature to the prediction as a point. We can find out for example if the "Age" feature is high, it contributes to positive prediction (toward diabetes = true).
- Dependence plot: Scatter plot of the dependency of a specific feature and the calculated Shapley values; that is, feature values v.s. the Shapley values of that feature.

LIME
- Local Interpretable Model Agnostic Explanation; it explains *individual prediction*.

#### julia packages
[Shapley.jl](https://expandingman.gitlab.io/Shapley.jl/)
[ShapML.jl](https://github.com/nredell/ShapML.jl)

#### Also see
- https://towardsdatascience.com/the-shapley-value-for-ml-models-f1100bff78d1

- [Counterfactual Explanations for Machine Learning: A Review](https://arxiv.org/pdf/2010.10596.pdf)

- [shap (Python)](https://github.com/slundberg/shap); where there are [references](https://github.com/slundberg/shap#citations) of related methods and critical keywords.