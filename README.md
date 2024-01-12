# explaining-explainable-ai

This repo is to share some of my personal findings on Explainable AI, in particular, the journey from interpretable models to using various methods to explain complex neural network models. 

1. [Linear Regression](https://github.com/wingyiuc/explaining-explainable-ai/blob/main/Linear%20Regression.ipynb)
2. [Decision Trees](https://github.com/wingyiuc/explaining-explainable-ai/blob/main/Decision%20Trees.ipynb)
     * 2.1. Random Forests feature importances
     * 2.2. Local Interpretable Model-agnostic Explanations (LIME)
     * 2.3. Tree SHAP
3. XAI for Computer Vision
     * 3.1. [Activation Maximization](https://github.com/wingyiuc/explaining-explainable-ai/blob/main/Activation%20Maximization.ipynb)
     * 3.2. [Saliency methods (SmoothGrad, GRAD-CAM, SHAP Gradient Explainer)](https://github.com/wingyiuc/explaining-explainable-ai/blob/main/Saliency%20Methods.ipynb)
4. [SHAP - a detailed explanation](https://github.com/wingyiuc/explaining-explainable-ai/blob/main/SHAP-explaining-explainable-ai.ipynb)



## Explainable AI - An Introduction

The use of AI in industry is gaining popularity, however, there are still some difficulties in trusting AI for decision making. It is crucial for business to understand how models make predictions. The lack of tranparency and accountability is unacceptable in a lot of domains, such as the medicial, compliance and legal field. Therefore, Explainable AI (XAI) methods are used to help us discover the AI decision process, and thus mitigate the risks with bias and fairness issues that might arise.

## Prediction Accuracy and Model Interpretability Trade-off

Not all AI models are black boxes. Simpler models, such as linear regressions, are known for its high interpretability. We can easily observe the weights and features, and this helps us to understand why and how a model predicts. However, it comes with a trade-off with the prediction accuracy. Since the model is too simple, it may fail to predict accurately on complex and large data.

The figure below shows the interpretability versus performance trade-off given common ML algorithms:

![Diagram showing Interpretability versus performance trade-off given common ML algorithms](https://docs.aws.amazon.com/images/whitepapers/latest/model-explainability-aws-ai-ml/images/interpretability-vs-performance-trade-off.png)

Source: https://docs.aws.amazon.com/whitepapers/latest/model-explainability-aws-ai-ml/interpretability-versus-explainability.html

Fortunately, there are methods to explain high performance complex models. In the subsequent chapters, we will look at the different model explanation methods and their Python implementation.

## Explainability vs Interpretability

We often use the terms "explainability" and "interpretability" interchangeabily, however, there are some subtle differences. Explaining a model means making its predictions understandable for human and plain to see. Interpretation would require a higher level of understanding of the meaning of the model . It is beyond making an observation clear, and we could interpret the actions we can take from the model outcomes.

## Types of Interpretability in Machine Learning

There are different ways to achieve interpretability in machine learning:

1. Use models that are inherently interpretable

Models such as linear models are inherently interpretable, however, these models often trade off with predictability.

2. Design complex models that are able to generate predictions and explanations

Training these models is very challenging, and this approach is inflexible as it applies to the very specific model.

3. Building explanation methods on top of existing models

This method can explain models without sacrificing model performances, and without the need for retaining the model.

This repo would focus on introducing the third type of model explanation methods, and provide the Python implementation with code examples.
