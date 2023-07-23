# explaining-explainable-ai

This repo is to share some of my personal findings on Explainable AI, in particular, the interpretation of SHAP values and pitfalls when we deploy it in production.

The code illustration is in `explaining-explainable-ai.ipynb` or download and view `explaining-explainable-ai.html` to view all the JavaScript graph display that are disabled by github.

# Background

Machine learning models are always seen as "black box" models. From my personal experience working in the data science field I found two major issues when we use ML:

1. I deployed the model but I have no idea how the model produced the predictions
2. My clients find it hard to understand and trust the model predictions

Explainable AI (XAI) emerges in the research field to solve the above problems. It is a set of processes and methods which answer the questions "how" and "why" AI systems work. In the paper [A Unified Approach to Interpreting Model Predictions](https://arxiv.org/abs/1705.07874), Lundberg and Lee proposed using SHAP (SHapley Additive exPlanations) as most consistent and reliable way to interpret a prediction model.

This notebook aims to explain how SHAP works and explain the difficulties and pitfalls when using it on real-life. In particular, the reliablilty of SHAP values on an imbalanced dataset and the runtime if we need to deploy it in production.


# What is SHAP?

SHAP is a mathematical method to explain the predictions of machine learning models. It is based on game theory, which assigns values to the features importance based on the marginal contribution of each feature.

We can use an example to illustrate the concept of SHAP. Imagine we have a startup company with 3 employees. The company just made a new deal that worth $100. How should we distribute the compensation for the three employees, namely, A, B and C? In this case, we woud need to know how much each employee has contributed. Assuming A and B worked equally hard, and C had no contribution at all. Intuitively, we would give $50 to A and B each, and $0 to C. A mathematical and computational way to calculate this is to try all different combinations of the employees in this startup, and how much they could make. For example:

- Startup with A, B and C: $100
- Startup with A and B only: $100
- Startup with A and C only: $0
- Startup with A only: $0

Then, we can find the weighted sum of marginal contributions for A is

$$
0.3333\times0 + 0.1667\times0 + 0.1667\times100 + 0.3333\times100 = 50
$$

Similarly, B would also get $50 and C would get $0.

SHAP does a similar analysis. It has a property which feature contributions must add up to the difference between the prediction of $x$ and the average of the preciction of "an average observation"

$$
\sum_{j=1}^{p} \phi_j = \hat{f}(x) - E_X(\hat{f}(X))
$$

where $\phi_j$ is the SHAP value of feature $j \in \{1, 2, 3, ... p \}$. It means that the sum of all the feature SHAP values equals the model prediction minus the average of the model predictions on "some average observations".

If we apply SHAP values on the above example, we would assume $E_X(\hat{f}(X)) = 0$ as the company would make a zero revenue if we pick any employee to work on the project alone. $\hat{f}(x) = 100$ and $\phi_A = \phi_B = 50$ while $\phi_C = 0$.

Notice I put a quote on "some average observations". In practice, this is the part that makes interpreting SHAP difficult in real-life data.

# Experiment

I prompted ChatGPT to generate some simulated data with latitude and longitude of 161 cities. The goal is to predict whether a city is in Asia or not, however, the dataset was deliberately made to be imbalanced with too many European cities. This is to simulate the situation of using ML to solve business problems, such as fraud detection, which the dataset is usually imbalanced but we have a low risk tolerance for true negatives. 

It is found that an imbalanced dataset would also impact the SHAP interpretation. The baseline values used in the SHAP computation would greatly affect the results. Some features would have their SHAP over or under-estimated. Hence, we should be careful in choosing a truly "meaningless" baseline. For more details please read `explaining-explainable-ai.ipynb` or download and view `explaining-explainable-ai.html` to view all the JavaScript graph display that are disabled by github.`
