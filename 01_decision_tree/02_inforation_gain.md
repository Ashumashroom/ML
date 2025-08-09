# Information Gain in Decision Trees

This document explains the concept of Information Gain and walks through a practical example to determine the root node of a decision tree.

---

## What is Information Gain?

**Information Gain** is the core metric used by decision tree algorithms (like ID3) to select the best feature to split the dataset at each node. It measures how much "information" a feature provides about the class.

In simple terms, Information Gain is the **reduction in entropy** (or uncertainty) that results from splitting the data on a particular attribute. The feature that causes the largest reduction in entropy is chosen for the split because it does the best job of separating the data into purer, more homogeneous groups.

### The Formula

The formula for Information Gain is:


Gain(S, A) = Entropy(S) - Σ (|S_v| / |S|) * Entropy(S_v)


Where:

* `Gain(S, A)` is the gain of the dataset `S` after splitting on attribute `A`.
* `Entropy(S)` is the entropy of the entire dataset `S` before the split.
* `v` represents each unique value in attribute `A`.
* `|S_v|` is the number of instances for the value `v`.
* `|S|` is the total number of instances in the dataset `S`.
* `Entropy(S_v)` is the entropy of the subset of instances `S_v`.
* The term `Σ (|S_v| / |S|) * Entropy(S_v)` represents the **weighted average entropy** of the children nodes after the split.

The goal is to find the attribute `A` that **maximizes** the Information Gain.

---

## Example Problem: Will I Pass the Exam?

Let's determine the best initial question to ask (i.e., find the root node) for a decision tree using the following dataset. The goal is to predict whether a student will **Pass** the exam.

### The Dataset

| Day | Sleep | Coffee | Topic Difficulty | Pass |
|:----|:------|:-------|:-----------------|:-----|
| 1   | Good  | Yes    | Easy             | Yes  |
| 2   | Good  | No     | Hard             | No   |
| 3   | Bad   | Yes    | Easy             | Yes  |
| 4   | Bad   | Yes    | Hard             | Yes  |
| 5   | Good  | No     | Easy             | Yes  |
| 6   | Bad   | No     | Hard             | No   |
| 7   | Good  | Yes    | Hard             | Yes  |
| 8   | Bad   | No     | Easy             | No   |

### Step 1: Calculate the Entropy of the Entire Dataset (Parent Entropy)

First, we calculate the entropy of our target variable, 'Pass'.

* Total instances: **8**
* Count of 'Yes': **5**
* Count of 'No': **3**

The formula for entropy is `Entropy = -p(Yes)log₂(p(Yes)) - p(No)log₂(p(No))`.

* `p(Yes) = 5/8 = 0.625`
* `p(No) = 3/8 = 0.375`

`Entropy(S) = - (0.625 * log₂(0.625)) - (0.375 * log₂(0.375))`
`Entropy(S) = - (0.625 * -0.678) - (0.375 * -1.415)`
`Entropy(S) = 0.42375 + 0.530625`
`Entropy(S) = 0.954`

The initial entropy of our dataset is **0.954**. This is the value we want to reduce.

### Step 2: Calculate Information Gain for Each Attribute

We will now calculate the Information Gain for each of the three attributes: 'Sleep', 'Coffee', and 'Topic Difficulty'.

#### A) Attribute: 'Sleep'

1.  **Split on 'Sleep' = 'Good'**:
    * 4 instances: 3 'Yes', 1 'No'
    * `Entropy(Sleep=Good) = - (3/4 * log₂(3/4)) - (1/4 * log₂(1/4)) = 0.811`

2.  **Split on 'Sleep' = 'Bad'**:
    * 4 instances: 1 'Yes', 3 'No'
    * `Entropy(Sleep=Bad) = - (1/4 * log₂(1/4)) - (3/4 * log₂(3/4)) = 0.811`

3.  **Calculate Information Gain for 'Sleep'**:
    * `Weighted Avg Entropy(Sleep) = (4/8) * 0.811 + (4/8) * 0.811 = 0.811`
    * `Gain(Sleep) = Entropy(S) - Weighted Avg Entropy(Sleep) = 0.954 - 0.811 = 0.143`

#### B) Attribute: 'Coffee'

1.  **Split on 'Coffee' = 'Yes'**:
    * 4 instances: 4 'Yes', 0 'No'
    * This is a pure subset, so `Entropy(Coffee=Yes) = 0`

2.  **Split on 'Coffee' = 'No'**:
    * 4 instances: 1 'Yes', 3 'No'
    * `Entropy(Coffee=No) = - (1/4 * log₂(1/4)) - (3/4 * log₂(3/4)) = 0.811`

3.  **Calculate Information Gain for 'Coffee'**:
    * `Weighted Avg Entropy(Coffee) = (4/8) * 0 + (4/8) * 0.811 = 0.4055`
    * `Gain(Coffee) = Entropy(S) - Weighted Avg Entropy(Coffee) = 0.954 - 0.4055 = 0.5485`

#### C) Attribute: 'Topic Difficulty'

1.  **Split on 'Topic Difficulty' = 'Easy'**:
    * 4 instances: 3 'Yes', 1 'No'
    * `Entropy(Topic=Easy) = - (3/4 * log₂(3/4)) - (1/4 * log₂(1/4)) = 0.811`

2.  **Split on 'Topic Difficulty' = 'Hard'**:
    * 4 instances: 2 'Yes', 2 'No'
    * This is a 50/50 split, so `Entropy(Topic=Hard) = 1`

3.  **Calculate Information Gain for 'Topic Difficulty'**:
    * `Weighted Avg Entropy(Topic) = (4/8) * 0.811 + (4/8) * 1 = 0.9055`
    * `Gain(Topic) = Entropy(S) - Weighted Avg Entropy(Topic) = 0.954 - 0.9055 = 0.0485`

### Step 3: Compare the Gains and Determine the Root Node

Now, let's compare the Information Gain for each attribute:

* `Gain(Sleep)` = 0.143
* **`Gain(Coffee)` = 0.5485**
* `Gain(Topic Difficulty)` = 0.0485

The attribute **'Coffee'** has the highest Information Gain (0.5485).

### Solution

The decision tree algorithm will select **'Coffee'** as the **root node** for the tree. Splitting the dataset based on whether the student had coffee provides the largest reduction in uncertainty and creates the most homogeneous child nodes to start the tree.
