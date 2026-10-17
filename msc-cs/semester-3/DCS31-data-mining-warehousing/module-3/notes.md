# Module 3 — Clustering, Outlier Detection & Advanced Techniques

---

## 1. Cluster Analysis

Clustering is an **unsupervised learning** technique that groups data objects into clusters such that:
- Objects within the same cluster are **similar** to each other
- Objects in different clusters are **dissimilar**

### Clustering vs Classification:

| Clustering | Classification |
|---|---|
| Unsupervised (no labels) | Supervised (labels given) |
| Discovers groups | Assigns to predefined groups |
| Exploratory | Predictive |

### Requirements of Good Clustering:
- Scalability — handle large datasets
- Ability to handle different types of attributes
- Discovery of clusters with arbitrary shapes
- Minimal requirement for domain knowledge
- Ability to handle noise and outliers

---

## 2. Partitioning Methods

Divide n objects into k clusters, where each object belongs to exactly one cluster.

### a) K-Means Algorithm

**The most widely used clustering algorithm.**

**Steps:**
1. Choose k (number of clusters)
2. Randomly select k objects as initial **centroids**
3. Assign each object to the nearest centroid (using Euclidean distance)
4. Recalculate centroids as the **mean** of all objects in each cluster
5. Repeat steps 3-4 until centroids don't change (convergence)

**Example:**
```
Data points: 2, 4, 10, 12, 3, 20, 30, 11, 25
k = 2

Step 1: Initial centroids: C1=4, C2=12

Step 2: Assign to nearest centroid:
  Cluster 1 (near 4): 2, 4, 3
  Cluster 2 (near 12): 10, 12, 20, 30, 11, 25

Step 3: New centroids:
  C1 = (2+4+3)/3 = 3
  C2 = (10+12+20+30+11+25)/6 = 18

Step 4: Reassign:
  Cluster 1 (near 3): 2, 4, 3
  Cluster 2 (near 18): 10, 12, 20, 30, 11, 25

Centroids unchanged -> STOP
```

**Advantages:**
- Simple, efficient, O(nkt) time complexity
- Works well for compact, spherical clusters

**Disadvantages:**
- Must specify k in advance
- Sensitive to initial centroids (may converge to local optimum)
- Sensitive to outliers (mean is affected by extreme values)
- Only finds spherical/convex clusters

### b) K-Medoids (PAM — Partitioning Around Medoids)

- Uses **actual data points (medoids)** as cluster centers instead of mean
- More robust to outliers than K-Means
- Medoid = the most centrally located object in a cluster

**Steps:**
1. Select k objects randomly as medoids
2. Assign each object to nearest medoid
3. For each medoid, try swapping with a non-medoid object
4. If swap reduces total cost (sum of distances), make the swap permanent
5. Repeat until no swap improves the result

**K-Means vs K-Medoids:**

| Feature | K-Means | K-Medoids |
|---|---|---|
| Center | Mean (virtual point) | Actual data point |
| Outlier sensitivity | High | Low (robust) |
| Speed | Faster | Slower |
| Applicability | Numeric data only | Any data type |

---

## 3. Hierarchical Methods

Build a hierarchy of clusters — either bottom-up or top-down.

### a) Agglomerative (Bottom-Up) — AGNES
1. Start with each object as its own cluster (n clusters)
2. Merge the two closest clusters
3. Repeat until only one cluster remains (or desired k clusters)

### b) Divisive (Top-Down) — DIANA
1. Start with all objects in one cluster
2. Split the most heterogeneous cluster
3. Repeat until each object is its own cluster (or desired k clusters)

### Distance Between Clusters:

| Method | Definition | Characteristic |
|---|---|---|
| Single linkage | Minimum distance between any pair across clusters | Can handle elongated shapes, sensitive to noise |
| Complete linkage | Maximum distance between any pair across clusters | Compact clusters, less sensitive to noise |
| Average linkage | Average distance between all pairs across clusters | Compromise between single and complete |
| Centroid linkage | Distance between cluster centroids | Can cause inversions |
| Ward's method | Merge clusters that cause minimum increase in total variance | Tends to create equal-sized clusters |

### Dendrogram:
- Tree-like diagram that records the sequence of merges/splits
- Cut at desired level to get k clusters

```
        __|__
       |     |
     __|__   E
    |     |
   _|_   _|_
  |   | |   |
  A   B C   D
```
Cutting at level 2 gives: {A,B}, {C,D}, {E}

### Advantages:
- No need to specify k in advance
- Produces a complete hierarchy (dendrogram)
- Can handle any shape of clusters

### Disadvantages:
- O(n^2) space, O(n^3) time — not scalable
- Cannot undo a merge/split once done

---

## 4. Outlier Detection

An outlier is a data object that is significantly different from the rest of the data.

### Why Detect Outliers?
- Fraud detection (unusual credit card transactions)
- Network intrusion detection
- Medical diagnosis (abnormal test results)
- Data cleaning (errors in data entry)

### Types of Outliers:

| Type | Description | Example |
|---|---|---|
| Global outlier | Significantly different from entire dataset | One purchase of Rs.10 lakh when average is Rs.1000 |
| Contextual outlier | Abnormal in a specific context | 40C temperature in December (normal in June) |
| Collective outlier | A group of data points collectively anomalous | Sudden spike in network traffic |

---

## 5. Outlier Detection Techniques

### a) Statistical Methods
- Assume data follows a distribution (usually normal/Gaussian)
- Points that fall outside expected range are outliers
- **Z-score method:** Outlier if |z| > 3 (more than 3 standard deviations from mean)
- **IQR method:** Outlier if value < Q1 - 1.5*IQR or value > Q3 + 1.5*IQR

### b) Distance-Based Methods
- Object O is an outlier if at least fraction p of objects are at distance greater than d from O
- Does not assume any distribution
- Expensive for large datasets

### c) Density-Based Methods (LOF — Local Outlier Factor)
- Compares the local density of a point with the local densities of its neighbors
- LOF >> 1: outlier (much lower density than neighbors)
- LOF ~ 1: normal point (similar density to neighbors)
- Better than distance-based methods for datasets with varying densities

### d) Clustering-Based Methods
- Cluster the data, then:
  - Objects that don't belong to any cluster = outliers
  - Objects far from their cluster center = outliers
  - Small clusters may represent outliers

---

## 6. Advanced Techniques

### a) Web Mining

Extracting knowledge from web data.

| Type | What it mines | Example |
|---|---|---|
| Web Content Mining | Content of web pages (text, images) | Extracting product info from e-commerce sites |
| Web Structure Mining | Hyperlink structure between pages | PageRank (Google) |
| Web Usage Mining | User browsing patterns from server logs | Recommendation systems, personalization |

### b) Text Mining

Extracting useful information from text documents.

**Steps:**
1. Text preprocessing — tokenization, stop word removal, stemming
2. Text representation — Bag of Words, TF-IDF
3. Pattern discovery — classification, clustering, sentiment analysis

**TF-IDF (Term Frequency — Inverse Document Frequency):**
```
TF(t,d) = (Number of times term t appears in document d) / (Total terms in d)
IDF(t) = log(Total documents / Documents containing term t)
TF-IDF(t,d) = TF(t,d) * IDF(t)
```
- High TF-IDF = term is important in that specific document
- Low TF-IDF = term is common across all documents (less informative)

**Applications:**
- Spam detection
- Sentiment analysis (product reviews, social media)
- Document categorization
- Information extraction

### c) Spatial Mining
- Mining patterns from spatial/geographic data
- Examples: Finding disease clusters in a region, urban planning, environmental monitoring
- Techniques: Spatial clustering, spatial association rules, spatial classification

### d) Temporal Mining
- Mining patterns from time-series data
- Examples: Stock market prediction, weather forecasting, sensor data analysis
- Techniques: Trend analysis, seasonal pattern detection, similarity search in time series

---

## 7. Data Mining Applications

| Domain | Application |
|---|---|
| Retail | Market basket analysis, customer segmentation, demand forecasting |
| Banking | Fraud detection, credit scoring, anti-money laundering |
| Healthcare | Drug discovery, disease outbreak prediction, patient readmission prediction |
| Telecom | Churn prediction, network optimization |
| Manufacturing | Defect detection, predictive maintenance |
| Social Media | Sentiment analysis, influence detection, community detection |
| Government | Tax fraud detection, crime pattern analysis |
| Education | Student performance prediction, dropout prediction |

---

## 8. Data Mining and Society

### Ethical Issues:
- **Privacy** — Mining personal data without consent
- **Surveillance** — Government/corporate tracking of individuals
- **Discrimination** — Biased algorithms (racial, gender bias in hiring/lending)
- **Manipulation** — Using mined patterns to manipulate behavior (targeted ads, fake news)

### Legal Issues:
- GDPR (General Data Protection Regulation) — EU
- IT Act — India
- Right to be forgotten
- Informed consent for data collection

---

## 9. Data Mining Trends

- **Big Data Mining** — Mining massive datasets using Hadoop, Spark
- **Deep Learning** — Neural networks with many layers for complex patterns
- **Real-time Mining** — Mining streaming data as it arrives
- **IoT Mining** — Mining data from sensors and connected devices
- **Privacy-Preserving Mining** — Mining while protecting individual privacy
- **Cloud-based Mining** — Mining as a service
- **Graph Mining** — Mining social networks, knowledge graphs

---

## 10. Data Mining Software

| Software | Type | Description |
|---|---|---|
| Weka | Open source | Java-based, GUI, widely used in academia |
| RapidMiner | Commercial/Free | Visual workflow designer, drag-and-drop |
| KNIME | Open source | Visual programming, analytics platform |
| Orange | Open source | Python-based, visual programming |
| R | Open source | Statistical computing, many mining packages |
| Python (scikit-learn) | Open source | Most popular ML/mining library |
| SAS | Commercial | Enterprise analytics platform |
| IBM SPSS | Commercial | Statistical analysis and data mining |

---

## Important Questions (Likely for Exam)

1. Explain K-Means clustering algorithm with an example.
2. Compare K-Means and K-Medoids.
3. Explain Agglomerative Hierarchical Clustering with a dendrogram.
4. What are the different distance measures between clusters? (Single, Complete, Average linkage)
5. What are outliers? Explain different types of outliers.
6. Explain LOF (Local Outlier Factor) method for outlier detection.
7. What is Web Mining? Explain its types.
8. Explain TF-IDF with an example.
9. Discuss ethical issues in data mining.
10. Compare partitioning and hierarchical clustering methods.
