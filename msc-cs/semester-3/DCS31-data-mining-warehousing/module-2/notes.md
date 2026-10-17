# Module 2 — Data Warehousing, OLAP & Classification

---

## 1. What is a Data Warehouse?

A data warehouse is a **subject-oriented, integrated, time-variant, and non-volatile** collection of data in support of decision-making.

— William H. Inmon (Father of Data Warehousing)

### Key Properties:

| Property | Meaning |
|---|---|
| Subject-oriented | Organized around major subjects (customers, products, sales) — not around daily operations |
| Integrated | Data from multiple sources is cleaned, transformed, and unified into consistent format |
| Time-variant | Data is stored with a time dimension — allows historical analysis (last 5-10 years) |
| Non-volatile | Data is loaded and accessed (read-only) — not updated or deleted like in OLTP systems |

### Data Warehouse vs Operational Database (OLTP)

| Feature | OLTP | Data Warehouse (OLAP) |
|---|---|---|
| Purpose | Day-to-day operations | Analysis and decision-making |
| Data | Current, detailed | Historical, summarized |
| Operations | Insert, Update, Delete | Read-only (SELECT, complex queries) |
| Users | Clerks, IT | Analysts, managers, executives |
| Design | ER-based, normalized | Star/Snowflake schema, denormalized |
| Size | MBs to GBs | GBs to TBs |
| Query type | Simple transactions | Complex analytical queries |

---

## 2. Data Warehouse Architecture

### Three-Tier Architecture:
```
Bottom Tier:   Data Warehouse Server (data storage, ETL)
Middle Tier:   OLAP Server (query processing, aggregation)
Top Tier:      Front-end tools (reporting, visualization, data mining)
```

### ETL Process (Extract, Transform, Load):
1. **Extract** — Pull data from multiple sources (databases, files, APIs)
2. **Transform** — Clean, convert, merge, aggregate data
3. **Load** — Store transformed data into the warehouse

### Metadata:
- **Administrative metadata** — Source descriptions, warehouse schema, transformation rules
- **Business metadata** — Business terms, data ownership, reporting rules

---

## 3. Data Warehouse Modeling

### a) Star Schema
- Central **fact table** connected to multiple **dimension tables**
- Simplest and most common schema
- Fact table contains measures (sales_amount, quantity) and foreign keys to dimensions
- Dimension tables contain descriptive attributes (product_name, customer_city)

```
           [Time]
             |
[Product] -- [SALES FACT] -- [Customer]
             |
           [Store]
```

**Fact Table: Sales**
| time_key | product_key | customer_key | store_key | sales_amount | quantity |
|---|---|---|---|---|---|

**Dimension Table: Product**
| product_key | product_name | category | brand |
|---|---|---|---|

### b) Snowflake Schema
- Extension of star schema where **dimension tables are normalized**
- Reduces redundancy but increases query complexity (more joins)

```
[Category] -- [Product] -- [SALES FACT] -- [Customer] -- [City] -- [State]
```

### c) Fact Constellation (Galaxy Schema)
- Multiple fact tables sharing dimension tables
- Used when there are multiple related subjects

### Star vs Snowflake:

| Feature | Star | Snowflake |
|---|---|---|
| Dimension tables | Denormalized | Normalized |
| Joins | Fewer (faster queries) | More (slower queries) |
| Redundancy | More | Less |
| Query simplicity | Simpler | More complex |
| Storage | More space | Less space |

---

## 4. Data Cube and OLAP

### What is a Data Cube?
A multi-dimensional representation of data that allows viewing data from different perspectives.

**Example:** Sales data viewed by Time, Product, and Location — forms a 3D cube.

### Cuboid:
- A **cube** at a specific level of aggregation
- **Base cuboid** — most detailed (individual records)
- **Apex cuboid** — most summarized (single total value)
- **Lattice of cuboids** — all possible aggregation levels

### OLAP (Online Analytical Processing)
Interactive analysis of multidimensional data.

### OLAP Operations:

| Operation | Description | Example |
|---|---|---|
| **Roll-up** (drill-up) | Aggregate data — go from detailed to summarized | City -> State -> Country |
| **Drill-down** | Go from summarized to detailed | Year -> Quarter -> Month -> Day |
| **Slice** | Select a single value for one dimension (2D cross-section) | Sales for Q1 only |
| **Dice** | Select multiple values for multiple dimensions (sub-cube) | Sales for Q1 and Q2, in Delhi and Mumbai |
| **Pivot** (rotate) | Rotate the cube to view data from a different perspective | Swap rows and columns |

### Types of OLAP Servers:

| Type | Description |
|---|---|
| ROLAP (Relational) | Uses relational databases to store and manage data |
| MOLAP (Multidimensional) | Uses multidimensional arrays for storage |
| HOLAP (Hybrid) | Combination of ROLAP and MOLAP |

---

## 5. Data Warehouse Design and Usage

### Steps in Design:
1. Choose the business process (sales, inventory, etc.)
2. Choose the grain (level of detail — daily, monthly)
3. Choose the dimensions (time, product, location, customer)
4. Choose the measures/facts (sales_amount, quantity, profit)

### Usage:
- **Information processing** — Querying, reporting, statistical analysis
- **Analytical processing** — OLAP operations (roll-up, drill-down, etc.)
- **Data mining** — Finding patterns, associations, clusters from warehouse data

---

## 6. Data Warehouse Implementation

### Approaches:

| Approach | Description |
|---|---|
| Top-down (Inmon) | Build enterprise-wide data warehouse first, then create data marts |
| Bottom-up (Kimball) | Build individual data marts first, then integrate into warehouse |

### Data Mart:
- A subset of the data warehouse focused on a specific department or business function
- Example: Marketing data mart, Finance data mart

### Indexing:
- **Bitmap index** — Efficient for low-cardinality attributes (Gender: M/F)
- **Join index** — Precomputed joins between fact and dimension tables

### Materialized Views:
- Precomputed query results stored for faster access
- Need to be refreshed when source data changes

---

## 7. Classification

Classification is a **supervised learning** technique where we build a model (classifier) from training data to predict the class label of new, unseen data.

### Classification Process:
```
Step 1: Training — Build model from labeled training data
Step 2: Testing — Evaluate model accuracy on test data
Step 3: Application — Use model to classify new data
```

---

## 8. Decision Tree Induction

A decision tree is a flowchart-like tree structure where:
- **Internal nodes** = tests on attributes
- **Branches** = outcomes of tests
- **Leaf nodes** = class labels

### Example:
```
                [Age?]
              /    |    \
         Youth   Middle  Senior
           |       |       |
       [Student?] Yes   [Credit?]
        /    \          /      \
      Yes    No    Excellent   Fair
       |      |       |         |
      Yes    No      No        Yes
```
(Predicting whether a person buys a computer)

### How to Build a Decision Tree?

**Key Question:** Which attribute to split on first?

### a) Information Gain (ID3 Algorithm)

**Entropy** — Measures impurity/disorder in data:
```
Entropy(S) = -SUM[pi * log2(pi)]
```
- pi = proportion of class i in dataset S
- Entropy = 0: pure (all same class)
- Entropy = 1: maximum impurity (50-50 split for binary)

**Information Gain:**
```
Gain(S, A) = Entropy(S) - SUM[(|Sv|/|S|) * Entropy(Sv)]
```
- A = attribute being tested
- Sv = subset of S where attribute A has value v
- Choose attribute with **highest information gain**

### b) Gain Ratio (C4.5 Algorithm)
- Information gain is biased toward attributes with many values
- Gain ratio normalizes by split information:
```
SplitInfo(S, A) = -SUM[(|Sv|/|S|) * log2(|Sv|/|S|)]
GainRatio(S, A) = Gain(S, A) / SplitInfo(S, A)
```

### c) Gini Index (CART Algorithm)
```
Gini(S) = 1 - SUM[pi^2]
```
- Gini = 0: pure
- Choose attribute with **lowest Gini index** after split

### Tree Pruning:
- **Pre-pruning** — Stop tree growth early (set max depth, min samples)
- **Post-pruning** — Build full tree, then remove branches that don't improve accuracy

---

## 9. Bayesian Classification (Naive Bayes)

Based on **Bayes' Theorem:**
```
P(C|X) = P(X|C) * P(C) / P(X)
```
- P(C|X) = posterior probability of class C given data X
- P(X|C) = likelihood — probability of data X given class C
- P(C) = prior probability of class C
- P(X) = probability of data X

### Naive Assumption:
Attributes are **conditionally independent** given the class label.
```
P(X|C) = P(x1|C) * P(x2|C) * ... * P(xn|C)
```

### Steps:
1. Calculate P(C) for each class from training data
2. For each attribute, calculate P(xi|C) for each class
3. For new data X, calculate P(C|X) for each class
4. Assign the class with **highest P(C|X)**

### Example:
```
Data: Age=Youth, Income=Medium, Student=Yes, Credit=Fair
Predict: Buys_Computer?

P(Yes) = 9/14,  P(No) = 5/14

P(Age=Youth|Yes) = 2/9    P(Age=Youth|No) = 3/5
P(Income=Medium|Yes) = 4/9  P(Income=Medium|No) = 2/5
P(Student=Yes|Yes) = 6/9   P(Student=Yes|No) = 1/5
P(Credit=Fair|Yes) = 6/9   P(Credit=Fair|No) = 2/5

P(X|Yes) * P(Yes) = (2/9)*(4/9)*(6/9)*(6/9)*(9/14) = 0.028
P(X|No) * P(No) = (3/5)*(2/5)*(1/5)*(2/5)*(5/14) = 0.007

P(Yes|X) > P(No|X) => Class = Yes (Buys Computer)
```

### Advantages:
- Simple, fast, works well with high-dimensional data
- Handles missing values naturally
- Good for text classification (spam detection)

### Disadvantage:
- Independence assumption rarely holds in real life

---

## 10. Rule-Based Classification

Classification using **IF-THEN rules**.

### Rule Format:
```
IF condition THEN conclusion
IF Age=Youth AND Student=Yes THEN Buys_Computer=Yes
```

### Rule Evaluation:
- **Coverage** — Percentage of tuples that satisfy the condition
- **Accuracy** — Percentage of tuples satisfying condition that also satisfy conclusion

### Rule Extraction from Decision Trees:
- One rule per path from root to leaf
- Conditions are the internal node tests along the path

### Rule-Based Methods:
- **Sequential covering** — Learn one rule at a time, remove covered examples, repeat
- **RIPPER** — Repeated Incremental Pruning to Produce Error Reduction

---

## 11. Classification by Back Propagation (Neural Networks)

### Structure:
```
Input Layer -> Hidden Layer(s) -> Output Layer
```
- Each connection has a **weight**
- Each node applies an **activation function**

### Activation Functions:
- **Sigmoid:** f(x) = 1 / (1 + e^(-x))  — output between 0 and 1
- **ReLU:** f(x) = max(0, x)

### Back Propagation Algorithm:
1. **Forward pass** — Input flows through network, produces output
2. **Calculate error** — Compare output with expected (target) value
3. **Backward pass** — Propagate error backward, update weights
4. **Repeat** until error is minimized or max iterations reached

### Weight Update Rule:
```
w_new = w_old + learning_rate * error * input
```

### Advantages:
- Can learn complex, non-linear decision boundaries
- High accuracy for many tasks

### Disadvantages:
- Slow training (many iterations needed)
- Black box — hard to interpret the model
- Can overfit on small datasets

---

## 12. Model Evaluation

### Confusion Matrix:
```
                  Predicted
                  Yes    No
Actual  Yes  |   TP   |  FN  |
        No   |   FP   |  TN  |
```

### Metrics:
```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
Precision = TP / (TP + FP)     — "Of all predicted Yes, how many are actually Yes?"
Recall = TP / (TP + FN)        — "Of all actual Yes, how many did we find?"
F1-Score = 2 * (Precision * Recall) / (Precision + Recall)
```

### Validation Methods:
- **Holdout** — Split data into training (70%) and testing (30%)
- **K-fold cross-validation** — Split data into k parts, train on k-1, test on 1, rotate
- **Leave-one-out** — K-fold where k = number of data points

---

## Important Questions (Likely for Exam)

1. Define Data Warehouse. Explain its characteristics.
2. Compare OLTP and OLAP.
3. Explain Star Schema and Snowflake Schema with diagrams.
4. What is a Data Cube? Explain OLAP operations with examples.
5. Explain the ETL process.
6. What is a Decision Tree? Explain ID3 algorithm with Information Gain.
7. Compare Information Gain, Gain Ratio, and Gini Index.
8. Explain Naive Bayes classification with an example.
9. Explain Back Propagation algorithm for neural networks.
10. What is a Confusion Matrix? Define Accuracy, Precision, Recall, and F1-Score.
