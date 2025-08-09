# Decision Trees and Entropy

This document provides a detailed explanation of Decision Trees and the concept of Entropy used within them.

---

## What is a Decision Tree?

A **decision tree** is a supervised machine learning algorithm that is used for both **classification** and **regression** tasks. It's a non-parametric method that works by learning simple decision rules inferred from the data features. The model resembles a tree-like structure, hence the name.

Think of it as a flowchart or a series of if-then-else statements that help in making a final decision or prediction.

### Structure of a Decision Tree 🌳

A decision tree has a hierarchical structure consisting of:

* **Root Node**: The top-most node in the tree, representing the entire dataset. It's the starting point from which the tree splits.
* **Decision Nodes (Internal Nodes)**: These are the nodes that represent a "test" on a feature. They split into branches, each representing an outcome of the test.
* **Leaf Nodes (Terminal Nodes)**: These are the final nodes of the tree that represent the class label (in classification) or a continuous value (in regression). They do not split any further.
* **Branches**: The links connecting the nodes, representing the decision rules.


                  [Root Node: Weather?]
                       /      |      \
                  Sunny /   Overcast |   Rainy \
                     /          |          \
    [Decision Node: Humidity?] [Leaf: Play] [Decision Node: Wind?]
          /       \                          /         \
    High /     Normal \                  Strong /       Weak \
      /           \                      /             \
[Leaf: No]     [Leaf: Yes]         [Leaf: No]       [Leaf: Yes]


### How a Decision Tree Works

A decision tree works by recursively partitioning the data into smaller, more homogeneous subsets. At each node, the algorithm selects the best feature to split the data based on a certain criterion (like Gini impurity or Information Gain). This process, known as **recursive partitioning**, continues until a stopping condition is met, such as:

* All data points in a node belong to the same class.
* There are no more features to split on.
* The tree has reached a predefined maximum depth to prevent overfitting.

### Types of Decision Trees

1.  **Classification Trees**: Used when the target variable is categorical (e.g., "Yes" or "No", "Spam" or "Not Spam"). The leaf nodes represent the class labels.
2.  **Regression Trees**: Used when the target variable is continuous (e.g., predicting the price of a house or temperature). The leaf nodes represent a continuous value, often the mean of the target values in that leaf.

---

## What is Entropy?

In the context of decision trees, **entropy** is a metric used to measure the level of impurity, disorder, or uncertainty in a set of data. It's a key concept from information theory.

* **High Entropy**: A high entropy value (closer to 1) indicates that the data is very mixed and impure. For example, a dataset with an equal number of samples from two different classes has high entropy because it's hard to predict the class of a new sample.
* **Low Entropy**: A low entropy value (closer to 0) indicates that the data is very pure and homogeneous. For example, a dataset where all the samples belong to the same class has zero entropy because there is no uncertainty.

The primary goal when building a decision tree is to split the data in a way that **reduces entropy** at each subsequent node.

### Calculating Entropy

The formula for calculating the entropy of a dataset `S` is:


Entropy(S) = - Σ p(i) * log₂(p(i))


Where:

* `S` is the dataset.
* `p(i)` is the proportion (probability) of the data belonging to class `i`.
* `Σ` is the summation over all the classes.
* `log₂` is the base-2 logarithm.

An entropy of **0** signifies a perfectly pure set (all data belongs to one class), while an entropy of **1** signifies a completely impure set (data is evenly split among classes in a binary classification scenario).

---

## How Entropy is Used: Information Gain

Decision tree algorithms like **ID3 (Iterative Dichotomiser 3)** use entropy to calculate **Information Gain**. Information Gain measures the reduction in entropy achieved by splitting a dataset based on a particular attribute.

**Information Gain = Entropy(parent) - Weighted Average Entropy(children)**

The attribute that results in the **highest information gain** is chosen as the splitting attribute for the current node. By maximizing information gain, the algorithm chooses the split that leads to the "purest" child nodes, thus building an effective and accurate decision tree.
