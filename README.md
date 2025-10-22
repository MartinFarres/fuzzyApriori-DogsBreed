# Fuzzy Apriori Analysis on Dog Breed Traits

This project applies the **Fuzzy-Apriori** algorithm to a dataset of dog breed characteristics to discover non-obvious association rules and patterns between traits.

The core of the analysis is in the `fuzzyApriori_DogsBreed.ipynb` notebook. The data is sourced from `breed_traits.csv`.

## Project Goal

The goal is to find interesting, predictive rules from a dataset of dog breed ratings. For example, can we find a strong rule like:

`IF (Energy Level is High) AND (Trainability is High) -> THEN (Mental Stimulation Needs are High)`

Standard Apriori cannot be used because our data consists of quantitative ratings (1-5), not simple binary (yes/no) transactions.

## The Fuzzy-Apriori Approach

We solve this problem by using **Fuzzy Logic** to convert our quantitative ratings into qualitative, overlapping sets, allowing us to find more nuanced patterns.

The analysis follows three main steps:

### Step 1: Fuzzification & Create Fuzzy Transactions

First, we **fuzzify** our quantitative data. We define **membership functions** (triangular rules) to translate the crisp numerical ratings (e.g., a score of 4) into meaningful, overlapping linguistic terms (e.g., `Medium` and `High`).

This process converts each breed into a **fuzzy transaction**, where every trait now has a "degree of membership" (a score from 0.0 to 1.0) in these fuzzy sets. For example, a `Shedding Level` of 4 becomes a "basket" containing items like `{ (Shedding=Medium: 0.5), (Shedding=High: 0.5) }`.

### Step 2: Run the Fuzzy-Apriori Algorithm

With our "fuzzy transactions" ready, we run the core algorithm to find **frequent itemsets**. This process iteratively calculates the `FuzzySupport` for all items (e.g., `Energy=High`) by summing their membership scores across all breeds. It then generates and prunes candidate itemsets (e.g., `{Energy=High, Playfulness=High}`) to find all combinations that meet a minimum support threshold.

### Step 3: Generate and Interpret Fuzzy Rules

From our list of frequent itemsets, we generate association rules. We test the strength of each rule by calculating its **Fuzzy Confidence** and **Lift**. These rules are then filtered by a `min_confidence` threshold to find only the most reliable patterns.

## Key Results & Visualizations

The analysis produced several key visualizations to interpret the patterns.

### 1\. Most Frequent Itemsets
<img width="1200" height="800" alt="most_frequent_itemsets" src="https://github.com/user-attachments/assets/66232d8a-5fa3-4195-8735-0564420dd136" />

This chart shows the most common individual traits and pairs found in the dataset. This helps us understand the baseline characteristics of the breeds.

### 2\. Association Rule Scatter Plot (Support vs. Confidence)
<img width="1000" height="600" alt="association_rules_support_vs_confidence" src="https://github.com/user-attachments/assets/cb3d3cb3-2ded-46e7-876d-75f0c5ce2c07" />

This plot shows all generated rules, allowing us to find the "best" ones. The most valuable rules are in the top-right, with high **Support** (common) and high **Confidence** (reliable). The color and size of each dot represent its **Lift** (how *interesting* or non-obvious the rule is).

### 3\. Top 10 Association Rules Network Graph
<img width="1200" height="800" alt="association_rules_network_improved" src="https://github.com/user-attachments/assets/a894b7bb-0611-428c-ab43-d6fdf276786f" />

This graph visualizes the **Top 10 most interesting rules (by Lift)**.

  * **Nodes (Circles)**: The traits.
  * **Arrows**: The rule (from "IF" to "THEN").
  * **Arrow Thickness**: Represents the `Lift` of the rule (thicker = more interesting).
  * **Node Size**: Represents the `Support` of the trait (bigger = more common).

## How to Use

1.  **Data:** The `breed_traits.csv` file contains the raw data.
2.  **Notebook:** The entire step-by-step analysis is in `fuzzyApriori_DogsBreed.ipynb`.
3.  **Dependencies:** You will need the following Python libraries:
      * `pandas`
      * `numpy`
      * `matplotlib`
      * `seaborn`
      * `networkx`
