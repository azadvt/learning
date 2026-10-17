# Module 1 — Introduction to Data Mining & Data Preprocessing

---

## 1. What is Data Mining?

Data mining is the process of discovering interesting patterns, knowledge, and useful information from large amounts of data. It is also called **Knowledge Discovery in Databases (KDD)**.

### The KDD Process:
```
Raw Data -> Data Cleaning -> Data Integration -> Data Selection -> Data Transformation -> Data Mining -> Pattern Evaluation -> Knowledge
```

### Formal Definition:
Data mining is the non-trivial extraction of implicit, previously unknown, and potentially useful information from data.

---

## 2. Different Kinds of Data That Are Mined

| Data Type | Examples |
|---|---|
| Relational databases | MySQL, Oracle tables |
| Data warehouses | Aggregated business data |
| Transactional databases | Supermarket purchases, bank transactions |
| Object-relational databases | Complex data with methods |
| Spatial databases | Maps, geographic data |
| Temporal databases | Time-series, stock market data |
| Text databases | Documents, web pages, emails |
| Multimedia databases | Images, audio, video |
| World Wide Web | Web pages, web logs |
| Stream data | Sensor data, network traffic |

---

## 3. Patterns That Are Mined

### a) Association Rules
- Finding items that frequently occur together
- Example: "Customers who buy bread also buy butter" (Market Basket Analysis)
- Represented as: `{Bread} -> {Butter}` with support and confidence

### b) Classification
- Assigning data objects to predefined classes/categories
- Example: Email -> Spam or Not Spam
- Models: Decision Trees, Naive Bayes, Neural Networks

### c) Clustering
- Grouping similar data objects together without predefined labels
- Example: Customer segmentation based on buying behavior
- Methods: K-Means, Hierarchical clustering

### d) Regression
- Predicting a continuous numerical value
- Example: Predicting house prices based on features

### e) Anomaly/Outlier Detection
- Finding data points that deviate significantly from the norm
- Example: Fraud detection in credit card transactions

### f) Sequential Pattern Mining
- Finding patterns in ordered/time-series data
- Example: Customer buys laptop -> then buys laptop bag -> then buys mouse

---

## 4. Technologies Used in Data Mining

- **Statistics** — Probability, distributions, hypothesis testing
- **Machine Learning** — Supervised, unsupervised, reinforcement learning
- **Database Systems** — Query processing, indexing, optimization
- **Pattern Recognition** — Classification, feature extraction
- **Information Retrieval** — Text mining, search engines
- **Visualization** — Graphical representation of patterns
- **High-Performance Computing** — Parallel and distributed processing for large datasets

---

## 5. Applications of Data Mining

| Domain | Application |
|---|---|
| Business | Customer segmentation, market basket analysis, churn prediction |
| Banking | Fraud detection, credit scoring, risk analysis |
| Healthcare | Disease prediction, drug discovery, patient diagnosis |
| Telecom | Network fault detection, customer profiling |
| Education | Student performance prediction, course recommendation |
| Web | Recommendation systems (Netflix, Amazon), search engines |
| Science | Gene analysis, climate prediction, astronomy |
| Social Media | Sentiment analysis, trend detection |

---

## 6. Major Issues in Data Mining

### a) Mining Methodology Issues
- Mining different kinds of knowledge from diverse data types
- Handling noisy and incomplete data
- Pattern evaluation — are the patterns truly interesting?

### b) Performance Issues
- Efficiency and scalability of algorithms
- Parallel, distributed, and incremental mining

### c) Diverse Data Types
- Mining complex data: text, spatial, multimedia, temporal, web data

### d) User Interaction Issues
- Interactive mining at multiple abstraction levels
- Presentation and visualization of results
- Background knowledge integration

### e) Security and Privacy Issues
- Data privacy — protecting sensitive information
- Avoiding misuse of mined knowledge

---

## 7. Data Objects and Attribute Types

### Data Object
A data object represents an entity. Also called: record, point, case, sample, tuple, instance, observation.

### Attribute (Feature/Variable)
A property or characteristic of a data object.

### Types of Attributes:

#### a) Nominal (Categorical)
- Names or labels, no meaningful order
- Examples: Color (Red, Blue, Green), Gender (M, F), ID numbers
- Operations: =, !=

#### b) Binary
- Only two states: 0 and 1
- **Symmetric binary**: Both values equally important (e.g., Gender: M/F)
- **Asymmetric binary**: One outcome is more important (e.g., Disease test: Positive/Negative)

#### c) Ordinal
- Has a meaningful order, but differences between values are not meaningful
- Examples: Size (S, M, L, XL), Grades (A, B, C, D), Rankings (1st, 2nd, 3rd)
- Operations: =, !=, <, >

#### d) Numeric
- **Interval-scaled**: Measured on a scale with equal intervals, no true zero
  - Examples: Temperature in Celsius (0C doesn't mean "no temperature"), Calendar dates
  - Operations: +, - (differences meaningful, ratios not)
- **Ratio-scaled**: Has a true zero point, ratios are meaningful
  - Examples: Age, Weight, Height, Salary, Distance
  - Operations: +, -, *, / (all meaningful)

### Summary Table:

| Type | Order | Example | Operations |
|---|---|---|---|
| Nominal | No | Colors, ID | =, != |
| Binary | No | Yes/No | =, != |
| Ordinal | Yes | Grades, Ranks | =, !=, <, > |
| Interval | Yes | Temperature (C) | =, !=, <, >, +, - |
| Ratio | Yes | Weight, Age | =, !=, <, >, +, -, *, / |

---

## 8. Basic Statistical Description of Data

Used to understand the overall properties and distribution of data.

### a) Measures of Central Tendency

**Mean (Average):**
```
Mean = (x1 + x2 + ... + xn) / n
```
- Sensitive to outliers
- Weighted mean: gives different importance to different values
- Trimmed mean: removes extreme values before computing

**Median:**
- Middle value when data is sorted
- If n is odd: middle element
- If n is even: average of two middle elements
- Not sensitive to outliers (robust measure)

**Mode:**
- Most frequently occurring value
- Unimodal (1 mode), Bimodal (2 modes), Multimodal (3+ modes)

### b) Measures of Dispersion (Spread)

**Range:**
```
Range = Max - Min
```

**Variance:**
```
Variance (s^2) = (1/n) * SUM[(xi - mean)^2]
```

**Standard Deviation:**
```
SD (s) = sqrt(Variance)
```

**Interquartile Range (IQR):**
```
IQR = Q3 - Q1
```
- Q1: 25th percentile (lower quartile)
- Q2: 50th percentile (median)
- Q3: 75th percentile (upper quartile)
- Used to detect outliers: values below Q1 - 1.5*IQR or above Q3 + 1.5*IQR

### c) Five-Number Summary
```
Min, Q1, Median, Q3, Max
```
Visualized using a **Box Plot (Box-and-Whisker plot)**

### d) Graphic Displays

| Chart | Purpose |
|---|---|
| Histogram | Shows frequency distribution of a single attribute |
| Box Plot | Shows five-number summary, detects outliers |
| Scatter Plot | Shows relationship between two attributes |
| Quantile Plot | Shows distribution of data along one dimension |
| Q-Q Plot | Compares distributions of two datasets |

---

## 9. Data Visualization

Graphical representation of data to discover patterns, trends, and outliers.

### Techniques:
- **Pixel-oriented** — Each data value mapped to a colored pixel
- **Geometric projection** — Scatter plots, parallel coordinates
- **Icon-based** — Chernoff faces, stick figures
- **Hierarchical** — Tree maps, dimensional stacking
- **Tag clouds** — Word frequency visualization

---

## 10. Measuring Data Similarity and Dissimilarity

### Proximity Measures
Used to measure how alike or different two data objects are.

### a) Dissimilarity Matrix
- d(i,j) = dissimilarity between objects i and j
- d(i,i) = 0 (object is identical to itself)
- d(i,j) = d(j,i) (symmetric)

### b) For Nominal Attributes
```
d(i,j) = (p - m) / p
```
- p = total number of attributes
- m = number of matching attributes

### c) For Binary Attributes

**Symmetric binary dissimilarity:**
```
d(i,j) = (r + s) / (q + r + s + t)
```

**Asymmetric binary (Jaccard coefficient):**
```
d(i,j) = (r + s) / (q + r + s)
```
Where (using contingency table):
- q = both 1, r = i=1,j=0, s = i=0,j=1, t = both 0

### d) For Numeric Attributes

**Euclidean Distance:**
```
d(i,j) = sqrt(SUM[(xi - xj)^2])
```

**Manhattan Distance (City Block):**
```
d(i,j) = SUM[|xi - xj|]
```

**Minkowski Distance (Generalized):**
```
d(i,j) = (SUM[|xi - xj|^h])^(1/h)
```
- h=1: Manhattan, h=2: Euclidean

**Cosine Similarity:**
```
cos(A,B) = (A . B) / (|A| * |B|)
```
- Used for document/text similarity
- Value between 0 and 1 (1 = identical direction)

---

## 11. Data Preprocessing

Real-world data is dirty: incomplete, noisy, inconsistent. Preprocessing improves data quality.

### Why Preprocessing?
- Incomplete data — missing values, missing attributes
- Noisy data — errors, outliers, duplicate records
- Inconsistent data — different formats, contradictory values

### Major Tasks:

### a) Data Cleaning
Filling missing values, smoothing noisy data, removing outliers, resolving inconsistencies.

**Handling Missing Values:**
| Method | Description |
|---|---|
| Ignore the tuple | If class label is missing |
| Fill manually | Time-consuming, not feasible for large data |
| Use global constant | Replace with "Unknown" or a default value |
| Use attribute mean | Replace with the mean of that attribute |
| Use class-specific mean | Mean of the attribute for the same class |
| Use most probable value | Predicted using regression, Bayesian, decision tree |

**Handling Noisy Data:**

Noise = random error or variance in a measured variable.

| Method | How it works |
|---|---|
| Binning | Sort data, partition into bins, smooth by bin mean/median/boundaries |
| Regression | Fit data to a function (linear/multiple regression) |
| Clustering | Group similar values, detect and remove outliers |
| Combined | Use computer and human inspection together |

**Binning Example:**
```
Sorted data: 4, 8, 9, 15, 21, 21, 24, 25, 26, 28, 29, 34
Bin 1: 4, 8, 9, 15    -> Bin mean: 9
Bin 2: 21, 21, 24, 25  -> Bin mean: 22.75
Bin 3: 26, 28, 29, 34  -> Bin mean: 29.25
```

### b) Data Integration
Combining data from multiple sources into a single coherent store.

**Issues:**
- **Schema integration** — Matching attributes from different sources (customer_id vs cust_no)
- **Entity identification** — Same entity with different representations
- **Redundancy** — Same attribute derived from another
  - Detected using **correlation analysis** (for numeric) or **chi-square test** (for nominal)
- **Data value conflicts** — Different scales, units, encoding

**Correlation (Pearson coefficient):**
```
r = SUM[(xi - mean_x)(yi - mean_y)] / (n * std_x * std_y)
```
- r > 0: positive correlation
- r < 0: negative correlation
- r = 0: no correlation

### c) Data Reduction
Reducing data volume while producing same or similar analytical results.

| Technique | Description |
|---|---|
| Dimensionality reduction | Reduce number of attributes (PCA, feature selection) |
| Numerosity reduction | Replace data with smaller representations (regression, histograms, sampling) |
| Data compression | Lossless or lossy compression |

**Principal Component Analysis (PCA):**
- Finds new orthogonal axes (principal components) that capture maximum variance
- Reduces dimensions while preserving most information

**Sampling Methods:**
- Simple random sampling (with or without replacement)
- Stratified sampling — divide into strata, sample from each
- Cluster sampling — divide into clusters, sample entire clusters

### d) Data Transformation
Converting data into forms appropriate for mining.

| Method | Description |
|---|---|
| Smoothing | Remove noise (binning, regression, clustering) |
| Aggregation | Summarize data (daily sales -> monthly sales) |
| Generalization | Replace low-level data with higher-level concepts (age -> age range) |
| Normalization | Scale data to a specific range |
| Attribute construction | Create new attributes from existing ones |

**Normalization Methods:**

**Min-Max Normalization:**
```
v' = (v - min) / (max - min) * (new_max - new_min) + new_min
```
Maps values to [new_min, new_max], typically [0,1]

**Z-Score Normalization:**
```
v' = (v - mean) / std_deviation
```
Maps based on mean and standard deviation

**Decimal Scaling:**
```
v' = v / 10^j
```
Where j is the smallest integer such that max(|v'|) < 1

### e) Data Discretization
Converting continuous attributes into discrete/categorical attributes.

| Method | Description |
|---|---|
| Equal-width binning | Divide range into N intervals of equal size |
| Equal-frequency binning | Each bin has approximately same number of data points |
| Entropy-based | Uses class information to determine split points |
| Clustering-based | Use clustering to determine natural groupings |

---

## Important Questions (Likely for Exam)

1. Explain the KDD process with a diagram.
2. What are the different types of attributes? Explain with examples.
3. Describe the measures of central tendency and dispersion.
4. Explain various data preprocessing techniques.
5. What are the different methods for handling missing values?
6. Explain binning with an example.
7. What is data normalization? Explain Min-Max and Z-Score methods.
8. Explain Euclidean, Manhattan, and Cosine similarity measures.
9. What are the major issues in data mining?
10. Explain data integration and the problems associated with it.
