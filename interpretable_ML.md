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

$\hat{f}$ is the model where $\hat{f}(x_1, x_2, ..., x_p)$ gives the prediction based on a set (a "row" in table) of input features $x_1, x_2, ..., x_p$. As we cannot simply exclude certain features, in practice the feature values NOT in the subset $S$ is sampled from empirical distribution.

The **value function** (know as the **payout function** for coalitions of players) gives the **contribution to the prediction** from a certain combination of features alone, for example, 
$$
val_x(S) =val_x(\{1,3\}) = \displaystyle\int \hat{f} (x_1, X_2, x_3,X_4) d\mathbb{P}_{X_2, X_4} - \mathbb{E}_X (\hat{f}(X))
$$
where $x_i$ is a certain feature value (e.g., `air_temperature=20.5`), and $X_i$ is the random variable of feature $i \in \{1,2,3,...,p\}$. 

According to these equations, 
- the Shapley value of a certain value of $j_{th}$ feature (e.g., `air_temperature=20.5`), $\phi_j (val)$, equals zero (to the average prediction value) as there is no difference with or without feature $j$.
- we CANNOT have feature importance estimation if there is only "a row of data" for a single prediction; instead, we must have "a table" of input features in order to allow $\int\hat{f}d\mathbb{P}_{X\notin S}$, as $X$ are random variables). See the **Disadvantage** section in [A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/).
- we CAN have the feature importance (contribution) of a certain feature value (e.g., the contribution of `air_temperature=20.5` to)


#### Visualization tools
[eXplainable AI (XAI)](https://towardsdatascience.com/explainable-ai-xai-lime-shap-two-great-candidates-to-help-you-explain-your-machine-learning-a95536a46c4e)
Shapley value
- Variable importance plot: A horizontal bar plot showing the importance of features as mean absolute Shapley value.
- Summary plot: Categorical scatter plot, showing contribution (positive or negative) of individual value of each feature to the prediction as a point. We can find out for example if the "Age" feature is high, it contributes to positive prediction (toward diabetes = true).
- Dependence plot: Scatter plot of the dependency of a specific feature and the calculated Shapley values; that is, feature values v.s. the Shapley values of that feature.

LIME
- Local Interpretable Model Agnostic Explanation; it explains *individual prediction*.

## Other resources

- Also see [shap (Python)](https://github.com/slundberg/shap); where there are [references](https://github.com/slundberg/shap#citations) of related methods and critical keywords.