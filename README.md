# Logistic Regression vs. Decision Trees: Two Ways to Learn from Data

Two classic models, two very different ideas. **Logistic regression** draws a smooth linear boundary between classes. A **decision tree** carves the feature space into boxes with a sequence of yes/no questions. This notebook compares them on two problems and shows how to keep a tree from overfitting.

## Part 1: Breast cancer classification

The task is to decide whether a tumour is malignant or benign from measurements such as mean radius, texture, perimeter and smoothness (30 features in total).

- Scatter plots of pairs of features show that the two classes are already largely separable.
- A **decision tree** (limited to depth 10) learns a readable set of rules, and its plot shows which features it splits on first. Feature importances reveal that only a handful of measurements do most of the work.
- A **logistic regression** is trained on the same split.

| Model | Test accuracy |
|---|---|
| Logistic regression | **97.2 %** |
| Decision tree | 92.3 % |

The linear model wins here. When classes are separated by something close to a straight boundary in a well-scaled feature space, a simple linear model has little to gain from the tree's flexibility, while the tree is more exposed to overfitting.

## Part 2: Predicting wine quality (regression)

A decision tree **regressor** predicts the quality score of white wine from its chemical properties. The two key hyperparameters control how complex the tree can get:

- `max_depth`: how many questions deep the tree may go
- `min_samples_split`: how many samples a node needs before it may split

Sweeping each of them and plotting the test error shows the classic **bias-variance trade-off**: very shallow trees underfit, very deep trees chase noise. The best depth is around 6 and the best `min_samples_split` around 10, giving a test MSE of roughly **0.60**.

## What you can take from this

- Trees are easy to read and need no feature scaling, but they overfit unless you limit their depth.
- Tuning is a curve, not a guess: plot the error against the hyperparameter and look for the minimum.
- A simple model is often hard to beat. Compare against it before reaching for something complex.

## Files

- `LR_DT.ipynb`: both parts with code, plots and discussion
- `winequality_white.csv`: the wine data (semicolon-separated)
