# DCS31 Data Mining & Warehousing — Exam Answer Sheet

> **How to use:** Part B = answer 2 of 3 per module (8 marks each). Part A = 9 short answers (3 marks each).
> ⭐ = asked before (Oct 2024, Oct 2023 or Dec 2021 papers, the test paper or the 2023 assignment). ⭐⭐ = asked in two or more.
> **Asked in almost every source:** k-means (Q13), data visualization (Q2), backpropagation / neural network classification (Q11), Bayes (Q16), similarity measures (Q3), data cube (Q6/Q8/Q20), warehouse design (Q19).
> This sheet **works together with the module notes** (`module-1/notes.md`, etc.). Topics already explained well there are linked; the topics the notes cover thinly are written out in full here.

## Syllabus coverage checklist

| Module | Syllabus topic | Where |
|---|---|---|
| 1 | Introduction, kinds of data and patterns | **Q18**, Notes M1 §1–3 |
| 1 | Technologies used | **Q1** |
| 1 | Applications, major issues | Notes M1 §5–6, **Q5** |
| 1 | Data objects and attribute types | Notes M1 §7 |
| 1 | Basic statistical description | Notes M1 §8 |
| 1 | Data visualization | **Q2** |
| 1 | Similarity and dissimilarity | **Q3**, Notes M1 §10 |
| 1 | Preprocessing: cleaning, integration, reduction, transformation, discretization | **Q4**, **Q17**, Notes M1 §11 |
| 2 | Data warehousing basics, architecture | **Q7**, Notes M2 §1–2 |
| 2 | Data cube, OLAP, schemas | **Q6**, Notes M2 §3–4 |
| 2 | Warehouse design and usage | **Q19** |
| 2 | Warehouse implementation, data cube technology, materialization | **Q8**, **Q20** |
| 2 | Classification, decision tree induction | **Q9**, Notes M2 §7–8 |
| 2 | Bayes classification | **Q16** |
| 2 | Rule-based classification | **Q10** |
| 2 | Classification by backpropagation | **Q11** |
| 3 | Cluster analysis, requirements, methods | **Q12** |
| 3 | Partitioning methods (k-means, k-medoids) | **Q13**, Notes M3 §2 |
| 3 | Hierarchical methods, BIRCH, CHAMELEON | **Q21** |
| 3 | Outliers and outlier detection | **Q14**, Notes M3 §4–5 |
| 3 | Web, text, spatial mining | Notes M3 §6 |
| 3 | Temporal mining | **Q22** |
| 3 | Applications, software | **Q15** |
| 3 | Data mining and society, trends | **Q23** |

---

# MODULE 1

## Q1. ⭐ Technologies that influence the development of data mining

**Asked:** 2024 Part B ("describe any four")

Data mining is **interdisciplinary**. It borrows from many fields:

```
          Statistics     Machine Learning    Pattern Recognition
                \               |               /
 Database   ---------->   DATA MINING   <----------  Visualization
 Systems                /       |       \
          Information   Algorithms   High-Performance
          Retrieval                  Computing
```

1. **Statistics**
   - Studies how data is collected, analysed and interpreted.
   - A *statistical model* describes the behaviour of data with random variables and probability distributions.
   - Used for data characterization, classification, verifying results (hypothesis testing, significance) and handling noise and missing values.
   - Example: regression models, Bayesian models.

2. **Machine learning**
   - Studies how computers can **learn and improve from data**.
   - *Supervised learning*: learn from labelled examples (classification).
   - *Unsupervised learning*: find groups in unlabelled data (clustering).
   - *Semi-supervised learning*: use a few labelled and many unlabelled examples.
   - *Active learning*: the learner asks the user to label selected examples.
   - Data mining adds **scalability** to ML, which matters for very large datasets.

3. **Database systems and data warehouses**
   - Provide data **storage, indexing, query processing and optimization**.
   - Data warehouses integrate data from many sources and support **OLAP** and multidimensional analysis.
   - Data mining needs scalable techniques that work on very large databases, sometimes inside the database ("in-database mining").

4. **Information retrieval (IR)**
   - The science of **searching documents** or information within documents (text, multimedia, web).
   - Uses *probabilistic models* and *topic models* (for example, a document as a bag of words).
   - Combined with data mining for text mining, web search and recommendations.

5. **Pattern recognition**: feature extraction and classification of patterns (images, speech).
6. **Visualization**: presents data and mined patterns graphically so users can understand them.
7. **Algorithms and high-performance computing**: parallel, distributed and cloud computing to mine huge data quickly.

**Conclusion:** because data volumes are huge, highly dimensional and complex, data mining **integrates** these technologies instead of relying on one.

---

## Q2. ⭐⭐ Data visualization techniques

**Asked:** 2024 Part B, Test paper

**Data visualization** shows data graphically so that patterns, trends, relationships and outliers are easy to see. It helps in data exploration, presenting results and quality checking.

Data visualization techniques are classified into **4 categories**:

### 1. Pixel-oriented visualization
- Each **attribute value is one coloured pixel**. The colour shows the value; for example, dark means low and bright means high.
- For n dimensions, the screen is divided into **n windows**, one per attribute.
- The records are sorted (for example by one attribute), and pixels for the same record sit at the **same position** in every window.
- **Circle segments**: arrange the windows as segments of a circle, so the dimensions are easy to compare.
- **Advantage:** shows a very large amount of data on one screen.

```
 Income      Credit limit     Transaction vol.     Age
+--------+   +--------+       +--------+          +--------+
|▓▓▒▒░░..|   |▓▓▓▒▒░..|       |▓▒░▒▓░..|          |░▒▓▓▒░..|
|▓▒▒░░...|   |▓▓▒▒░░..|       |▒░▓▒░▒..|          |▒▓▓▒░░..|
+--------+   +--------+       +--------+          +--------+
 (records sorted by income; same position = same customer)
```

### 2. Geometric projection techniques
Help find interesting projections of multidimensional data.
- **Scatter plot**: 2 attributes on the x and y axes. A third and fourth can be shown with colour or shape.
- **Scatter-plot matrix**: an n × n grid of scatter plots, one for every pair of dimensions.
- **Parallel coordinates**: n **equally spaced vertical axes**, one per dimension. Each record is a **polyline** crossing every axis at its value. It handles many dimensions, but clutters with many records.
- **Landscapes**: 3-D surfaces.

```
Parallel coordinates:
 A1   A2   A3   A4
 |\   |   /|    |
 | \__|__/ |____|
 |    |    |    |
```

### 3. Icon-based visualization
Use small **icons** to represent multidimensional values.
- **Chernoff faces**: up to 18 dimensions are mapped to **facial features** (eye size, mouth curve, nose length, face shape). People recognise small differences in faces easily.
- **Stick figures**: 2 dimensions map to the x and y axes, and the rest map to the angles and lengths of a stick figure's limbs. Large datasets form **textures**.

### 4. Hierarchical visualization
Split the dimensions into subsets (subspaces) and show them hierarchically.
- **Dimensional stacking**: embed one 2-D space inside another, level by level.
- **Worlds-within-worlds (n-Vision)**: fix some dimensions, then show the remaining ones in an inner 3-D "world".
- **Tree-maps**: show hierarchical data as **nested rectangles**. Area is proportional to an attribute (such as disk usage per folder).
- **Cone trees**, **InfoCube**: 3-D hierarchies.

### 5. Visualizing complex data and relations
- **Tag clouds**: words sized by their frequency or importance.
- **Graphs / networks**: show relationships, such as social networks.

**Basic graphic displays** (also accepted): histogram, box plot, quantile plot, Q-Q plot, scatter plot (see Notes M1 §8d).

---

## Q3. ⭐ Measures of data similarity and dissimilarity

**Asked:** 2024 Part B ("any four measures")

- **Similarity** measures how alike two objects are (0 to 1, higher means more alike).
- **Dissimilarity** (distance) measures how different they are (0 means identical).
- Used in clustering, outlier detection and nearest-neighbour classification.

**Data matrix** (n objects × p attributes) vs **dissimilarity matrix** (n × n, d(i,j), lower triangle only):
```
| 0                       |
| d(2,1)  0               |
| d(3,1)  d(3,2)  0       |
| ...                     |
```

### 1. Nominal attributes
**d(i,j) = (p − m) / p**, where m = number of matches and p = total attributes. Similarity sim = m/p.
*Example:* 4 attributes and 3 match, so d = 1/4 = 0.25.

### 2. Binary attributes (contingency table)
|  | j = 1 | j = 0 |
|---|---|---|
| **i = 1** | q | r |
| **i = 0** | s | t |

- **Symmetric binary** (0 and 1 equally important, such as gender): d = (r + s)/(q + r + s + t)
- **Asymmetric binary** (1 matters more, such as a test result): d = (r + s)/(q + r + s), ignoring t
- **Jaccard coefficient** (similarity): sim = q/(q + r + s)

### 3. Numeric attributes: Minkowski family
- **Euclidean (L2):** d(i,j) = √[(x_i1 − x_j1)² + … + (x_ip − x_jp)²]
- **Manhattan (L1, city block):** d(i,j) = |x_i1 − x_j1| + … + |x_ip − x_jp|
- **Minkowski (Lh):** d(i,j) = (Σ |x_if − x_jf|^h)^{1/h}
- **Supremum (L∞, Chebyshev):** d(i,j) = max_f |x_if − x_jf|

*Worked example:* x1 = (1, 2), x2 = (3, 5)
- Euclidean = √(4 + 9) = √13 ≈ 3.61
- Manhattan = 2 + 3 = 5
- Supremum = max(2, 3) = 3

Properties of a **metric**: d ≥ 0 (non-negativity); d(i,i) = 0; d(i,j) = d(j,i) (symmetry); d(i,j) ≤ d(i,k) + d(k,j) (triangle inequality).

### 4. Ordinal attributes
Replace each value with its rank r_if in {1, …, M_f}, then normalize: **z_if = (r_if − 1)/(M_f − 1)** so it lies in [0, 1]. Then use Euclidean or Manhattan.
*Example:* {fair, good, excellent} have ranks 1, 2, 3, giving z = 0, 0.5, 1.

### 5. Mixed attribute types
d(i,j) = Σ_f δ_ij^(f) d_ij^(f) / Σ_f δ_ij^(f). This combines each attribute's own measure; δ = 0 when a value is missing.

### 6. Cosine similarity (documents / term-frequency vectors)
**cos(x, y) = (x · y) / (‖x‖ ‖y‖)**
*Example:* x = (5, 0, 3, 0, 2), y = (3, 0, 2, 0, 1)
- x·y = 15 + 6 + 2 = 23; ‖x‖ = √38 = 6.16; ‖y‖ = √14 = 3.74
- cos = 23/(6.16 × 3.74) = **0.998**, so the documents are very similar.
- Ignores zero entries (0-matches), which suits sparse data.

---

## Q4. ⭐ Data preprocessing (need + major tasks) and missing values

**Asked:** 2024 Part A ("need for preprocessing", "ways to fill missing values")

### Why preprocessing? (Data quality)
Real-world data is **dirty**:
- **Incomplete**: missing values or attributes
- **Noisy**: errors and outliers (for example salary = −10)
- **Inconsistent**: conflicting codes (for example age = 42 but birth year = 2010)

**"Garbage in, garbage out":** poor-quality data leads to poor-quality mining results.
Quality factors: **accuracy, completeness, consistency, timeliness, believability, interpretability**.

### Major tasks
```
Dirty data -> [Cleaning] -> [Integration] -> [Reduction] -> [Transformation & Discretization] -> Clean data
```
1. **Data cleaning**: fill missing values, smooth noise, find outliers, fix inconsistencies.
2. **Data integration**: combine several sources. Handles entity identification (cust_id vs customer_no), **redundancy** (found by χ² test for nominal data, correlation coefficient for numeric data) and value conflicts (₹ vs $).
3. **Data reduction**: a smaller representation that gives the same results.
   - *Dimensionality reduction*: wavelet transform, **PCA**, attribute subset selection
   - *Numerosity reduction*: regression, histograms, clustering, **sampling**
   - *Data compression*
4. **Data transformation**:
   - **Min-max normalization:** v′ = (v − min)/(max − min) × (new_max − new_min) + new_min
   - **Z-score normalization:** v′ = (v − mean)/σ
   - **Decimal scaling:** v′ = v/10^j
   - Also smoothing, attribute construction, aggregation and concept hierarchy generation
5. **Data discretization**: replace numeric values with intervals or labels (age becomes youth, adult, senior), by binning, histogram analysis, cluster analysis or decision trees.

### Ways to fill missing values
1. Ignore the tuple (when the class label is missing)
2. Fill it in manually
3. Use a global constant ("Unknown")
4. Use the attribute **mean or median**
5. Use the attribute mean for **the same class**
6. Use the **most probable value** (regression, Bayesian inference, decision tree), which is the most popular method

### Noisy data: smoothing by binning (example)
Sorted: 4, 8, 15, 21, 21, 24, 25, 28, 34, in equal-frequency bins of 3:
- Bin 1: 4, 8, 15. By mean: 9, 9, 9. By boundaries: 4, 4, 15
- Bin 2: 21, 21, 24. By mean: 22, 22, 22. By boundaries: 21, 21, 24
- Bin 3: 25, 28, 34. By mean: 29, 29, 29. By boundaries: 25, 25, 34

---

## Q5. ⭐ Major issues in data mining

**Asked:** 2024 Part A ("list and define any two")

1. **Mining methodology**: mining different kinds of knowledge; mining in multidimensional space; interdisciplinary efforts; handling noise, uncertainty and incompleteness; pattern evaluation (interestingness).
2. **User interaction**: interactive mining; using background knowledge; ad-hoc mining and query languages; presentation and visualization of results.
3. **Efficiency and scalability**: algorithms must scale to huge data; parallel, distributed and incremental mining.
4. **Diversity of database types**: complex data (text, multimedia, spatial, temporal, web, streams); dynamic and global repositories.
5. **Data mining and society**: social impact; **privacy-preserving** mining; invisible data mining (built into systems such as recommendations).

---

# MODULE 2

## Q6. ⭐ Role of the data cube in the multidimensional model and its schemas

**Asked:** 2024 Part B

### Data cube
- A data cube lets data be **modelled and viewed in multiple dimensions**.
- **Dimensions** are the perspectives (time, item, location). Each has a **dimension table** (item_name, brand, type, …).
- **Facts** are the numeric measures (dollars_sold, units_sold), stored in the **fact table** with keys to every dimension.

```
             location
            /
           /  Chennai  Delhi  Mumbai
          +--------+--------+--------+
     Q1   |  605   |  825   |  14    |
time Q2   |  680   |  952   |  31    |
     Q3   |  812   | 1023   |  30    |
     Q4   |  927   | 1038   |  38    |  ---> item
          +--------+--------+--------+
```

### Lattice of cuboids
- With n dimensions there are **2ⁿ cuboids**.
- **Base cuboid** (0-D aggregation): the lowest summarization, all n dimensions.
- **Apex cuboid** (all): the highest summarization, a single total.

```
                    all (apex, 0-D)
          /          |          \
      time         item       location          (1-D)
       |   \      /    \     /    |
  time,item  time,location  item,location       (2-D)
          \          |          /
          time, item, location (base, 3-D)
```

### Role of the data cube
- Supports **OLAP**: roll-up, drill-down, slice, dice, pivot (see Notes M2 §4).
- **Precomputed aggregates** give fast answers to queries.
- Supports **concept hierarchies** (day → month → quarter → year) so data can be viewed at different levels.
- A natural basis for **multidimensional data mining (OLAM)**.

### Schemas
**1. Star schema**: one central **fact table** joined to a set of **unnormalized dimension tables**, shaped like a star.
```
           time_dim
              |
 item_dim -- SALES FACT -- branch_dim
              |
          location_dim
```
**2. Snowflake schema**: dimension tables are **normalized** into extra tables (location → city → state), shaped like a snowflake. It saves space but needs more joins.

**3. Fact constellation (galaxy)**: **multiple fact tables share dimension tables** (for example sales and shipping share time, item and location). Used in enterprise warehouses.

| | Star | Snowflake | Fact constellation |
|---|---|---|---|
| Fact tables | 1 | 1 | Many |
| Dimensions | Denormalized | Normalized | Shared |
| Joins | Few (fast) | More (slower) | Varies |
| Used for | Data marts | Saves storage | Enterprise warehouse |

---

## Q7. ⭐ Data warehouse architecture, data warehouse models, metadata repository

**Asked:** 2024 Part A ("features of any two data warehouse models", "properties of metadata repository")

### Definition (Inmon)
A data warehouse is a **subject-oriented, integrated, time-variant and non-volatile** collection of data that supports management's decision making.

### Three-tier architecture
```
TOP TIER       Front-end tools: query/report, analysis, data mining
                          ^
MIDDLE TIER    OLAP server (ROLAP / MOLAP / HOLAP)
                          ^
BOTTOM TIER    Data warehouse server (RDBMS) + data marts + METADATA REPOSITORY
                          ^
               Back-end tools: Extract -> Clean -> Transform -> Load -> Refresh
                          ^
               Operational databases + external sources
```
- **Bottom tier**: the warehouse database server. ETL tools extract, clean, transform, load and refresh the data. Gateways such as ODBC, JDBC and OLE-DB connect to the sources.
- **Middle tier**: the OLAP server. ROLAP maps the operations onto a relational DB; MOLAP uses multidimensional arrays.
- **Top tier**: client tools for queries, reports, analysis and data mining.

### Data warehouse models (from the architecture point of view)
1. **Enterprise warehouse**
   - Collects **all information about subjects across the whole organization**.
   - Corporate-wide integration from one or more operational systems or external providers.
   - Detailed plus summarized data; gigabytes to terabytes or more.
   - Takes **years** to design and build; built on mainframes or parallel platforms.
2. **Data mart**
   - A **subset** of corporate data that is useful to a **specific group** (marketing, sales).
   - Uses a star or snowflake schema; built on low-cost servers; takes **weeks** to build.
   - *Independent* data mart: sourced straight from operational systems.
   - *Dependent* data mart: sourced from the enterprise warehouse.
3. **Virtual warehouse**
   - A set of **views over operational databases**.
   - Only some summary views are materialized.
   - **Easy to build**, but needs spare capacity on the operational DB servers.

*Recommended approach:* incremental. Build a high-level corporate data model, then independent data marts and an enterprise warehouse in parallel, then a multitier warehouse.

### Metadata repository
**Metadata is data about data.** In a warehouse it defines the warehouse objects. The repository holds:
1. **A description of the warehouse structure**: schema, views, dimensions, hierarchies, derived-data definitions, data mart locations and contents.
2. **Operational metadata**: **data lineage** (where data came from and how it was transformed), **currency** (active, archived or purged) and monitoring information (usage statistics, error reports, audit trails).
3. **The algorithms used for summarization**: measure and dimension definitions, granularity, partitions, predefined queries and reports.
4. **The mapping from the operational environment to the warehouse**: source DBs, gateways, cleaning and transformation rules, refresh and purge rules, security.
5. **Data related to system performance**: indices and profiles, refresh timing and scheduling.
6. **Business metadata**: business terms and definitions, data ownership, charging policies.

**Properties / uses:** acts as a directory to find warehouse contents; guides the mapping during transformation; guides the summarization algorithms; and must be **kept persistent, on stable storage**.

---

## Q8. Data warehouse implementation and data cube technology

### 1. Efficient data cube computation
- **The compute cube operator** computes aggregates over all subsets of the dimensions. For example, `define cube sales [item, city, year]: sum(sales)` computes 2³ = **8 cuboids**.
- **The curse of dimensionality:** with concept hierarchies, **total cuboids T = Π_{i=1}^{n} (L_i + 1)**, where L_i is the number of levels of dimension i (+1 for "all"). For example, 10 dimensions with 5 levels each give 6¹⁰ ≈ 6 × 10⁷ cuboids.
- **Materialization choices:**
  - *No materialization*: compute on the fly, which is slow
  - *Full materialization*: precompute everything, which needs a huge amount of storage
  - *Partial materialization*: precompute a chosen subset, the best trade-off
- **Kinds of cube:**
  - **Full cube**: all cuboids
  - **Iceberg cube**: only cells that pass a minimum-support threshold (`HAVING COUNT(*) >= min_sup`)
  - **Closed cube**: only closed cells, which removes redundancy
  - **Shell cube**: only cuboids with few dimensions (for example 3-D)
- **Cube computation methods:**
  - **Multiway array aggregation** (MOLAP): partition the array into chunks and compute several aggregates in one scan
  - **BUC (bottom-up computation)**: from the apex down, with **Apriori pruning** for iceberg cubes
  - **Star-Cubing**: combines top-down and bottom-up, using a star tree

### 2. Indexing OLAP data
- **Bitmap index**: one bit vector per attribute value. Fast AND/OR comparisons; ideal for **low-cardinality** attributes (gender, region).

  | RID | item | H (home) | C (computer) |
  |---|---|---|---|
  | R1 | H | 1 | 0 |
  | R2 | C | 0 | 1 |
  | R3 | H | 1 | 0 |

- **Join index**: precomputes joins between the fact table and the dimension tables (for example location "Delhi" → the matching fact rows). Suits a star schema.

### 3. Efficient OLAP query processing
1. Find which operations to run on the available cuboids (map slice and dice onto selections and projections).
2. Choose the **cheapest materialized cuboid** that can answer the query (the smallest one that includes the needed dimensions at a fine enough level).

### 4. OLAP server architectures
- **ROLAP**: relational DB, scalable
- **MOLAP**: sparse array storage, fast
- **HOLAP**: detail in ROLAP and aggregates in MOLAP
- **Specialized SQL servers**: built for star and snowflake queries

---

## Q9. ⭐ Decision tree induction for classification

**Asked:** 2024 Part A

- A **flowchart-like tree**: internal nodes test an attribute, branches are test outcomes and leaves are class labels.
- **Classify** a new tuple by tracing the path from the root to a leaf.
- Algorithms: **ID3** (information gain), **C4.5** (gain ratio), **CART** (Gini index). All use a greedy, top-down, recursive divide-and-conquer approach.

**Algorithm (Generate_decision_tree):**
1. Create node N.
2. If all tuples are in the same class, make N a leaf with that class.
3. If no attributes are left, make N a leaf with the **majority class**.
4. Otherwise, choose the **best splitting attribute** (highest information gain).
5. Label N with it and create a branch for each outcome.
6. Recurse on each partition.

**Information gain:**
- Info(D) = −Σ p_i log₂(p_i)
- Info_A(D) = Σ (|D_j|/|D|) × Info(D_j)
- **Gain(A) = Info(D) − Info_A(D)**

*Worked example (buys_computer: 9 yes, 5 no):*
- Info(D) = −(9/14)log₂(9/14) − (5/14)log₂(5/14) = **0.940**
- Age: youth (2Y, 3N), middle (4Y, 0N), senior (3Y, 2N), so Info_age = (5/14)(0.971) + (4/14)(0) + (5/14)(0.971) = **0.694**
- Gain(age) = 0.940 − 0.694 = **0.246**, the highest, so **age is the root**.

**Tree pruning:** removes branches that reflect noise (overfitting).
- *Pre-pruning*: stop early when a threshold is reached.
- *Post-pruning*: grow the full tree, then remove subtrees (cost-complexity).

More: Notes M2 §8 (gain ratio, Gini index).

---

## Q10. ⭐ Rule-based classification with examples

**Asked:** 2024 Part B

### IF-THEN rules
`R1: IF age = youth AND student = yes THEN buys_computer = yes`
- The IF part is the **antecedent / precondition**. The THEN part is the **consequent**.
- A rule **covers** a tuple if the tuple satisfies the antecedent.

**Rule quality:**
- **coverage(R) = n_covers / |D|**
- **accuracy(R) = n_correct / n_covers**

*Example:* D has 14 tuples. R1 covers 2 and both are correct, so coverage = 2/14 = **14.28%** and accuracy = 2/2 = **100%**.

### Conflict resolution (when more than one rule fires)
1. **Size ordering**: the rule with the **most attribute tests** (the toughest one) wins.
2. **Rule ordering** (a **decision list**), either:
   - *Class-based*: classes in order of importance or frequency
   - *Rule-based*: rules in order of quality (accuracy, coverage, size)
3. **Default rule**: applies when **no rule fires**, usually the majority class.

### Method 1: rule extraction from a decision tree
- **One rule per root-to-leaf path**. Each test along the path is ANDed; the leaf gives the class.
- The rules are **mutually exclusive** (no conflicts) and **exhaustive** (one rule for every attribute-value combination).

```
age?
├─ youth  → student? ├─ no  → NO      R1: IF age=youth AND student=no  THEN buys=no
│                    └─ yes → YES     R2: IF age=youth AND student=yes THEN buys=yes
├─ middle → YES                       R3: IF age=middle_aged           THEN buys=yes
└─ senior → credit?  ├─ excellent→NO  R4: IF age=senior AND credit=excellent THEN buys=no
                     └─ fair → YES    R5: IF age=senior AND credit=fair      THEN buys=yes
```
- Rules can be **pruned** by removing conditions that don't improve accuracy (as in C4.5).

### Method 2: sequential covering algorithm
Learns rules **directly from the data, one at a time**.
```
Rule_set = {}
for each class c:
    repeat
        Rule = Learn_One_Rule(D, Att_vals, c)
        remove the tuples covered by Rule from D
        Rule_set = Rule_set + Rule
    until terminating condition (no tuples left, or rule quality too low)
return Rule_set
```
- **Learn_One_Rule** works **general-to-specific**: start with `IF {} THEN class`, then greedily add the attribute test that most improves rule quality.
- **Quality measure: FOIL_Gain** = pos′ × [log₂(pos′/(pos′+neg′)) − log₂(pos/(pos+neg))]. It favours rules with high accuracy that cover many positives.
- **Rule pruning: FOIL_Prune(R) = (pos − neg)/(pos + neg)**. If the pruned version scores higher, prune.
- Examples: AQ, CN2, **RIPPER**.

**Advantages:** easy to understand and interpret, and as accurate as decision trees. Classifying new data is fast.

---

## Q11. ⭐⭐ Backpropagation algorithm (classification by backpropagation)

**Asked:** 2024 Part B, Test paper

**Backpropagation** is a neural network learning algorithm for a **multilayer feed-forward network**. It learns by iteratively processing training tuples, comparing the network's prediction with the actual target, and **adjusting the weights to minimize the mean-squared error**. The changes travel **backwards** from the output layer through the hidden layers, hence the name.

### Network
```
 x1 ──○──┐        ○──┐
         ├──w_ij──○  ├──w_jk──○ ──> output O_k
 x2 ──○──┤        ○──┤
         │        ○──┘
 x3 ──○──┘
 Input layer   Hidden layer    Output layer
```
- Each unit j has a **bias θ_j** and connection **weights w_ij**.
- Initialize all weights and biases to **small random numbers** (for example −0.5 to +0.5).

### Algorithm
**Input:** D (training tuples), l (learning rate, 0 to 1), the network.

**Step 1: Propagate the inputs forward**
- Input unit: output O_j = input x_j
- Hidden and output unit j:
  - **Net input: I_j = Σ_i w_ij O_i + θ_j**
  - **Output (sigmoid / logistic activation): O_j = 1 / (1 + e^{−I_j})**

**Step 2: Backpropagate the error**
- **Output unit:** **Err_j = O_j (1 − O_j)(T_j − O_j)**, where T_j is the target. O_j(1 − O_j) is the derivative of the sigmoid.
- **Hidden unit:** **Err_j = O_j (1 − O_j) Σ_k Err_k w_jk**, where k runs over the next layer.

**Step 3: Update the weights and biases**
- **Δw_ij = (l) Err_j O_i**, then **w_ij = w_ij + Δw_ij**
- **Δθ_j = (l) Err_j**, then **θ_j = θ_j + Δθ_j**
- Updating after every tuple is **case updating**. Accumulating over all tuples is **epoch updating**.

**Step 4: Terminate when**
- every Δw_ij in the last epoch is below a threshold, **or**
- the percentage of misclassified tuples is below a threshold, **or**
- a set number of epochs is reached.

### Small example (one step)
x = (1, 0, 1), target T = 1, l = 0.9. Suppose the output unit gives O₆ = 0.474.
- Err₆ = 0.474 × (1 − 0.474) × (1 − 0.474) = **0.1311**
- A weight w₄₆ = −0.3 from hidden unit 4 (O₄ = 0.332) becomes −0.3 + 0.9 × 0.1311 × 0.332 = **−0.261**

### Pros and cons
- **Pros:** tolerates noisy data; classifies patterns it was not trained on; works with continuous values; can run in parallel.
- **Cons:** **long training time**; needs parameters set by experiment (topology, learning rate); **poor interpretability** (a black box), although rules can be extracted.

---

# MODULE 3

## Q12. ⭐ Basics, requirements and methods of clustering

**Asked:** 2024 Part A (requirements), 2024 Part B

### Basics
- **Cluster analysis** partitions a set of objects into **clusters** so that objects in a cluster are **similar** to each other and **dissimilar** to objects in other clusters.
- It is **unsupervised learning**: learning by observation, with no class labels.
- Uses: business (customer segmentation), biology (taxonomy), image recognition, web search (grouping results), and **outlier detection**.

### Requirements of clustering in data mining
1. **Scalability**: works on millions of objects, not just a sample.
2. **Handles different attribute types**: numeric, binary, nominal, ordinal and mixed.
3. **Discovers clusters of arbitrary shape**, not only spherical ones.
4. **Needs little domain knowledge to set input parameters** (such as k).
5. **Handles noisy data** and outliers.
6. **Incremental clustering and insensitivity to input order.**
7. **Handles high-dimensional data.**
8. **Constraint-based clustering**: respects user constraints.
9. **Interpretability and usability** of the results.

### Comparison aspects
Partitioning criteria (single-level or hierarchical); separation of clusters (exclusive or overlapping); similarity measure (distance or density); clustering space (full space or subspace).

### Major clustering methods

| Method | Idea | Algorithms | Features |
|---|---|---|---|
| **Partitioning** | Split n objects into k groups; improve by **iterative relocation** | k-means, k-medoids (PAM), CLARA | Spherical clusters, distance-based, needs k |
| **Hierarchical** | Build a tree (dendrogram), either **agglomerative** (bottom-up) or **divisive** (top-down) | AGNES, DIANA, BIRCH, Chameleon | Merges or splits can't be undone |
| **Density-based** | Grow a cluster while the neighbourhood **density** exceeds a threshold | **DBSCAN**, OPTICS, DENCLUE | **Arbitrary shapes**, filters noise |
| **Grid-based** | Quantize the space into a **grid of cells** and cluster the cells | STING, CLIQUE, WaveCluster | **Very fast**: depends on the number of cells, not objects |

**DBSCAN in brief:** parameters ε (radius) and MinPts.
- A **core object** has at least MinPts neighbours within ε.
- Points are **density-reachable** if connected through a chain of core objects.
- A cluster is a maximal set of **density-connected** points. Points that are not reachable are noise.

---

## Q13. ⭐⭐ k-means partitioning method with example

**Asked:** 2024 Part B, Test paper

**Partitioning method:** given n objects and k, build k partitions (clusters) where each cluster has at least one object and each object belongs to exactly one cluster. It optimizes an objective function, the within-cluster variation.

### k-means (centroid-based)
**Objective (sum of squared error):** **E = Σ_{i=1}^{k} Σ_{p∈C_i} dist(p, c_i)²**, where c_i is the centroid (mean) of cluster C_i.

**Algorithm:**
1. Choose k objects at random as the initial cluster centres.
2. **repeat**
3. (Re)assign each object to the cluster with the **nearest centre** (Euclidean distance).
4. Update each cluster mean: c_i = mean of the objects in C_i.
5. **until** no change.

**2-D worked example** (k = 2): points A(1,1), B(1.5,2), C(3,4), D(5,7), E(3.5,5), F(4.5,5), G(3.5,4.5). Initial centres: A(1,1) and D(5,7).

| Point | dist to (1,1) | dist to (5,7) | Cluster |
|---|---|---|---|
| A(1,1) | 0 | 7.21 | 1 |
| B(1.5,2) | 1.12 | 6.10 | 1 |
| C(3,4) | 3.61 | 3.61 | 1 (tie, go to the first) |
| D(5,7) | 7.21 | 0 | 2 |
| E(3.5,5) | 4.72 | 2.50 | 2 |
| F(4.5,5) | 5.31 | 2.06 | 2 |
| G(3.5,4.5) | 4.30 | 2.92 | 2 |

New centres:
- C1 = mean(A, B, C) = ((1 + 1.5 + 3)/3, (1 + 2 + 4)/3) = **(1.83, 2.33)**
- C2 = mean(D, E, F, G) = (16.5/4, 21.5/4) = **(4.12, 5.38)**

Reassign: C(3,4) is now 2.03 from C1 and 1.78 from C2, so **C moves to cluster 2**.
- C1 = mean(A, B) = **(1.25, 1.5)**
- C2 = mean(C, D, E, F, G) = **(3.9, 5.1)**

Repeating gives no further change, so the final clusters are **{A, B}** and **{C, D, E, F, G}**.

**Complexity:** O(nkt), with t iterations. Efficient.
**Limits:**
- k must be given beforehand
- sensitive to the initial centres and to **outliers**
- only finds convex or spherical clusters
- needs a mean, so it suits numeric data only

**Variants:**
- **k-modes** for nominal data
- **k-medoids (PAM)** uses actual objects as centres, which is robust to outliers (Notes M3 §2b)
- **CLARA / CLARANS** for large datasets

---

## Q14. ⭐ Outliers: types and detection techniques

**Asked:** 2024 Part A ("types of outliers")

An **outlier** is a data object that **deviates significantly** from the rest, as if generated by a different mechanism. It is different from noise, which is random error.

### Types of outliers
1. **Global outlier (point anomaly)**: deviates significantly from the **whole dataset**. *Example:* a very large transaction in credit card fraud. The simplest type to detect.
2. **Contextual (conditional) outlier**: deviates only **within a specific context**. *Example:* 28 °C is normal in summer but an outlier in a Kashmir winter.
   - Attributes split into *contextual* attributes (time, location) and *behavioural* attributes (temperature).
3. **Collective outlier**: a **subset** of objects that together deviate from the whole dataset, even though each one on its own may not be an outlier. *Example:* many computers sending denial-of-service packets together; a run of delayed orders.

### Detection techniques
- **By supervision:** supervised (labelled normal/outlier), semi-supervised and unsupervised.
- **Statistical (model-based):** assume a distribution, and objects in low-probability regions are outliers.
  - *Parametric*: Grubbs' test, z-score beyond ±3σ
  - *Non-parametric*: histograms, kernel density
- **Proximity-based:**
  - *Distance-based*: an object is an outlier if fewer than a fraction π of objects lie within distance r of it (a DB(r, π) outlier).
  - *Density-based*: **LOF (local outlier factor)** compares an object's density with its neighbours'. LOF ≫ 1 means an outlier.
- **Clustering-based:** objects that belong to no cluster, are far from the nearest cluster centre, or belong to tiny clusters.
- **Classification-based:** train a one-class model of normal data.

---

## Q15. ⭐ Data mining applications and software

**Asked:** 2024 Part B, Test paper

### Applications
1. **Financial data analysis (banking)**
   - Loan payment prediction and **credit policy** analysis
   - Classification and clustering of customers for targeted marketing
   - Detecting **money laundering** and financial crime
2. **Retail and telecommunications**
   - **Market basket analysis** (association rules) for store layout and cross-selling
   - Customer retention: **churn prediction**
   - Multidimensional analysis of sales, customers and time
   - Fraud detection (unusual calling patterns)
3. **Science and engineering**
   - Bioinformatics: gene sequence and **DNA analysis**
   - Climate data, astronomy, earth sciences
   - Fault detection in engineering systems
4. **Intrusion detection and prevention**
   - **Signature-based** detection (known attacks) and **anomaly-based** detection (deviation from normal)
5. **Recommender systems**
   - **Content-based** (similar items) and **collaborative filtering** (similar users), as on Amazon or Netflix
6. **Healthcare**: disease prediction and treatment effectiveness. **Education**: student performance.
7. **Web and social media**: web search ranking (PageRank), sentiment analysis, community detection.

### Data mining software

| Software | Type | Highlights |
|---|---|---|
| **WEKA** | Open source (Java) | GUI; classification, clustering and association; used in academia |
| **RapidMiner** | Free / commercial | Drag-and-drop workflows |
| **KNIME** | Open source | Visual analytics pipelines |
| **Orange** | Open source (Python) | Visual programming, education |
| **R** | Open source | Statistical packages (rpart, cluster) |
| **Python (scikit-learn, pandas)** | Open source | The most popular ML/DM library |
| **SAS Enterprise Miner** | Commercial | Enterprise analytics |
| **IBM SPSS Modeler** | Commercial | Statistical modelling |
| **Oracle Data Mining, MS SQL Server Analysis Services** | Commercial | Mining inside the database |

**How to choose a data mining system:** data types supported; system issues (OS, client-server); data sources (ODBC); the mining functions and methods offered; coupling with the DB or warehouse; scalability; visualization tools; query language and GUI.

### Data mining and society (short)
Ubiquitous and invisible data mining (search, recommendations, shopping); **privacy, security and social impact**; privacy-preserving mining (randomization, k-anonymity, l-diversity, distributed mining).

### Trends
Application exploration; scalable and interactive methods; integration with search engines, databases, warehouses and the cloud; mining **social and information networks**; mining spatiotemporal, cyber-physical and **multimedia, text and web data**; biological data mining; real-time and **stream mining**; privacy protection; visual and audio data mining.

---

# MORE 8-MARK ANSWERS (from the Dec 2021 and Oct 2023 papers and the 2023 assignment)

## Q16. ⭐ Bayes theorem and Bayesian (naive Bayes) classification

**Asked:** Oct 2023 Part B (Module 1), 2023 assignment

### Bayes theorem
Let X be a data tuple (the "evidence") and H the hypothesis that X belongs to class C.

**P(H|X) = P(X|H) · P(H) / P(X)**

| Term | Name | Meaning |
|---|---|---|
| P(H\|X) | **Posterior** probability | Probability of H after seeing X |
| P(H) | **Prior** probability | Probability of H before seeing any data |
| P(X\|H) | **Likelihood** | Probability of seeing X when H is true |
| P(X) | **Evidence** | Probability of X (the same for every class) |

*Simple example:* 1% of customers are fraudsters (P(H) = 0.01). The fraud alert fires for 90% of fraudsters (P(X|H) = 0.9) and for 5% of honest customers.
- P(X) = 0.9 × 0.01 + 0.05 × 0.99 = 0.0585
- P(H|X) = 0.009/0.0585 = **0.154**: only about 15% of alerts are real fraud.

### Naive Bayesian classifier
1. D is a training set of tuples X = (x₁, x₂, …, xₙ) with m classes C₁ … Cₘ.
2. Predict the class with the **highest posterior**: X belongs to Cᵢ if P(Cᵢ|X) > P(Cⱼ|X) for all j ≠ i.
3. P(X) is the same for every class, so only **maximize P(X|Cᵢ) · P(Cᵢ)**.
4. **Naive assumption (class-conditional independence):** **P(X|Cᵢ) = Π_k P(x_k|Cᵢ)**
5. For categorical attributes, P(x_k|Cᵢ) = (tuples of Cᵢ with value x_k) / |Cᵢ|. For continuous attributes, use a **Gaussian**: g(x, μ, σ) = (1/√(2π)σ) e^{−(x−μ)²/2σ²}.

### Worked example (buys_computer data, 14 tuples: 9 yes, 5 no)
Classify **X = (age = youth, income = medium, student = yes, credit = fair)**.

| | P(·\|yes) | P(·\|no) |
|---|---|---|
| Prior | 9/14 = 0.643 | 5/14 = 0.357 |
| age = youth | 2/9 = 0.222 | 3/5 = 0.600 |
| income = medium | 4/9 = 0.444 | 2/5 = 0.400 |
| student = yes | 6/9 = 0.667 | 1/5 = 0.200 |
| credit = fair | 6/9 = 0.667 | 2/5 = 0.400 |
| **P(X\|C)** | 0.222×0.444×0.667×0.667 = **0.044** | 0.6×0.4×0.2×0.4 = **0.019** |
| **P(X\|C)·P(C)** | 0.044 × 0.643 = **0.028** | 0.019 × 0.357 = **0.007** |

0.028 > 0.007, so **buys_computer = yes**.

**Zero-probability problem:** if a count is 0, the whole product becomes 0. The fix is the **Laplacian correction**: add 1 to every count. With large data this hardly changes the estimates.

**Advantages:** simple and fast; works well in practice (spam filtering, text classification); handles missing values.
**Disadvantages:** the independence assumption is often false (dependent attributes such as age and income). **Bayesian belief networks** fix this by modelling dependencies as a DAG with conditional probability tables.

---

## Q17. ⭐ Data reduction methods ("any four")

**Asked:** Dec 2021 Part B

**Data reduction** gives a **smaller representation of the data that produces the same (or almost the same) mining results**. It saves storage and makes mining faster.

### 1. Dimensionality reduction (fewer attributes)
- **Wavelet transform (DWT):** turns the data into wavelet coefficients and keeps only the strongest ones. Good for sparse and skewed data.
- **Principal component analysis (PCA):**
  - Normalize the data
  - Compute k orthonormal vectors (principal components) that capture the most variance
  - Sort them by variance and keep the top few
  - The new axes are combinations of the original attributes
- **Attribute subset selection:** remove irrelevant or redundant attributes using greedy methods:
  - *Stepwise forward selection*: start empty and add the best attribute each time
  - *Stepwise backward elimination*: start with all attributes and remove the worst each time
  - *Combined forward and backward*
  - *Decision tree induction*: attributes that don't appear in the tree are irrelevant

### 2. Numerosity reduction (fewer or smaller values)
- **Parametric: regression and log-linear models.** Store only the model parameters, for example y = wx + b instead of all the points.
- **Histograms:** split the data into buckets (equal-width or equal-frequency) and store the bucket counts.
- **Clustering:** store the cluster representatives (centroid, diameter) instead of the raw data.
- **Sampling** (s tuples out of N):
  - *SRSWOR*: simple random sample without replacement
  - *SRSWR*: simple random sample with replacement
  - *Cluster sample*: choose whole clusters or pages at random
  - *Stratified sample*: sample within each stratum (good for skewed data, such as by age group)
- **Data cube aggregation:** store summarized data, for example yearly totals instead of quarterly ones.

### 3. Data compression
- **Lossless** (the original can be fully rebuilt, as with string compression) or **lossy** (wavelets, PCA).

**Conclusion:** the time spent reducing the data should not be more than the time it saves during mining.

---

## Q18. ⭐ Different kinds of data and patterns that are mined

**Asked:** Dec 2021 Part B, Oct 2023 Part A

### Kinds of data
1. **Database data:** relational tables (rows are tuples, columns are attributes). Mined for trends and deviations, for example "which items sell less than last year?"
2. **Data warehouse data:** integrated, historical, summarized data in data cubes. Supports OLAP and multidimensional mining.
3. **Transactional data:** each record is a transaction (trans_ID plus a list of items). Used for **market basket analysis**.
4. **Other kinds:**
   - time-series and sequence data (stock prices)
   - data streams (sensors)
   - spatial data (maps)
   - engineering design data
   - hypertext and multimedia
   - graph and network data (social networks)
   - text and **web data**

### Kinds of patterns (data mining functionalities)
1. **Class / concept description:**
   - *Characterization*: summarize the general features of a target class (for example, the profile of big spenders)
   - *Discrimination*: compare the target class with contrasting classes
2. **Frequent patterns, associations and correlations:**
   - Itemsets, sequences and substructures that occur often
   - Example: `buys(X, "computer") ⇒ buys(X, "software") [support = 1%, confidence = 50%]`
3. **Classification and regression:**
   - Build a model (decision tree, Bayes, neural network) that predicts a **class label**
   - Regression predicts **continuous values**
4. **Cluster analysis:** group objects without labels, maximizing intra-class similarity and minimizing inter-class similarity.
5. **Outlier analysis:** find objects that don't fit the general behaviour (fraud detection).

**Are all patterns interesting?** No. A pattern is **interesting** if it is easily understood, valid on new data, potentially useful and novel. Objective measures are support and confidence; subjective measures are unexpectedness and actionability.

---

## Q19. ⭐ Data warehouse design (with example) and its usage

**Asked:** Dec 2021 Part B, Oct 2023 Part B

### Business analysis framework: four views
1. **Top-down view**: chooses the information the business needs.
2. **Data source view**: the information captured and stored by operational systems.
3. **Data warehouse view**: fact tables and dimension tables.
4. **Business query view**: the data as the end user sees it.

### Design approaches
- **Top-down:** overall design and planning first. Good when the business problems are clear and the technology is mature.
- **Bottom-up:** start with experiments and prototypes (data marts). Cheap and fast to show results.
- **Combined:** both together.
- Software process: **waterfall** (structured, step by step) or **spiral** (fast, iterative prototypes, better for changing requirements).

### Steps in the design process (Kimball)
1. **Choose a business process to model**, for example sales, orders or shipments. If the process covers the whole organization, model a data warehouse; if it is departmental, model a **data mart**.
2. **Choose the grain** (the atomic level of data), for example an individual sales transaction or daily snapshots.
3. **Choose the dimensions** for each fact-table record, for example time, item, customer, branch, location.
4. **Choose the measures** (numeric additive quantities), for example dollars_sold and units_sold.

### Example: a sales data warehouse (star schema)
```
 time_dim                 item_dim
 (time_key, day,          (item_key, item_name,
  month, quarter, year)    brand, type)
          \                 /
           \               /
          +------------------+
          |   SALES_FACT     |
          | time_key         |
          | item_key         |
          | branch_key       |
          | location_key     |
          | dollars_sold  ←measure
          | units_sold    ←measure
          +------------------+
           /               \
 branch_dim                 location_dim
 (branch_key, name, type)   (location_key, street, city, state, country)
```
- Business process: **sales**. Grain: **one row per item per transaction per day**.
- A query such as "total sales of laptops in Kerala in Q1 2024" becomes a slice and dice on this cube.

### Usage of the data warehouse
1. **Information processing:** queries, basic statistics and **reports** using tables, charts and graphs.
2. **Analytical processing:** **OLAP** operations (slice, dice, drill-down, roll-up, pivot) on historical, summarized data.
3. **Data mining:** **knowledge discovery** of hidden patterns, associations, classification and prediction, with results shown through visualization tools.

**OLAM (online analytical mining)** combines OLAP with data mining on the warehouse: the data is already clean and integrated, OLAP lets users explore it, and mining functions can be switched on the fly.

---

## Q20. ⭐ How a data warehouse is implemented (ways to implement); data cube materialization

**Asked:** Dec 2021 Part B; 2023 assignment ("data cube materialization"); Oct 2023 Part B ("data cube technology")

Answer using **Q8** (efficient cube computation, indexing, OLAP query processing). Add the following:

**Ways to implement (build) the warehouse:**
- **Top-down (Inmon)**: the enterprise warehouse first, then dependent data marts.
- **Bottom-up (Kimball)**: data marts first, integrated later through conformed dimensions.
- **Hybrid / incremental**: a corporate data model first, then data marts and the enterprise warehouse in parallel, then a multitier warehouse.

**Data cube materialization (precomputation): three choices**
1. **No materialization:** compute every query from the base cuboid on demand. Very slow.
2. **Full materialization:** precompute **all cuboids**. Fastest, but needs a huge amount of memory (Π(L_i + 1) cuboids).
3. **Partial materialization:** precompute **a chosen subset**. This is the trade-off between storage and response time. Options include:
   - an **iceberg cube**, keeping only cells with count ≥ min_sup
   - a **shell fragment**, precomputing only small-dimension cuboids and computing the others on the fly
   - choosing cuboids by **query frequency, access cost and update cost**
- Materialized cuboids must be **refreshed** when the source data changes.

---

## Q21. ⭐ Hierarchical clustering methods (incl. BIRCH and CHAMELEON)

**Asked:** 2023 assignment ("explain hierarchical methods", "BIRCH", "CHAMELEON"); Dec 2021 Part A (agglomerative vs divisive)

A **hierarchical method** groups the data objects into a **tree of clusters** (a hierarchy).

### 1. Agglomerative (bottom-up), e.g. AGNES
Start with **each object as its own cluster**, then **merge the two closest clusters** repeatedly until one cluster remains or a stop condition is met.

### 2. Divisive (top-down), e.g. DIANA
Start with **all objects in one cluster**, then **split** repeatedly until each object stands alone or a stop condition is met.

```
Step:  0     1      2       3        4      (agglomerative →)
       a ─┐
          ├─ ab ─┐
       b ─┘      │
       c ────────┼─────────┐
       d ─┐      │         ├── abcde
          ├─ de ─┴── cde ──┘
       e ─┘
Step:  4     3      2       1        0      (← divisive)
```
The tree is drawn as a **dendrogram**. Cutting it at a chosen level gives the clusters.

### Distance between clusters (linkage measures)
- **Single link (minimum distance):** the closest pair of points. Can produce long chains.
- **Complete link (maximum distance):** the farthest pair. Gives compact clusters.
- **Average link:** the average over all pairs.
- **Centroid distance:** the distance between the cluster means.

**Weakness:** a merge or split **can never be undone**, and the basic method scales poorly (O(n²) or worse). The methods below address this.

### 3. BIRCH (Balanced Iterative Reducing and Clustering using Hierarchies)
- Designed for **very large datasets**.
- **Clustering feature (CF):** CF = ⟨n, LS, SS⟩
  - n = number of points
  - LS = linear sum of the points
  - SS = square sum of the points
  - The centroid, radius and diameter can all be computed from the CF. CFs are **additive**: CF₁ + CF₂ = CF of the merged cluster.
- **CF-tree:** a height-balanced tree that stores the CFs. It has two parameters: the **branching factor B** (maximum children) and the **threshold T** (maximum diameter of a leaf subcluster).
- **Phases:**
  1. Scan the data once and build an in-memory CF-tree, which is a multi-level compression of the data.
  2. Apply any clustering algorithm (such as k-means) to the leaf nodes.
- **Pros:** **one scan, O(n)**, incremental.
- **Cons:** only one point per leaf; tends to find **spherical** clusters only; sensitive to the order of the data.

### 4. CHAMELEON (dynamic modelling)
- Hierarchical clustering that finds **clusters of arbitrary shape and density**.
- **Steps:**
  1. Build a **k-nearest-neighbour graph**, where each point is linked to its k most similar points.
  2. **Partition** the graph into many small subclusters with a graph-partitioning algorithm (hMETIS), cutting the weakest edges.
  3. **Merge** subclusters agglomeratively, merging two clusters only when both of these are high:
     - **Relative interconnectivity (RI):** how connected the two clusters are, compared with their internal connectivity
     - **Relative closeness (RC):** how close the two clusters are, compared with their internal closeness
- **Pros:** adapts to each cluster's internal characteristics, so it handles shapes that k-means and BIRCH can't.
- **Cons:** costly, O(n²) in high dimensions.

---

## Q22. ⭐ Temporal mining methods ("any two")

**Asked:** Oct 2023 Part B

**Temporal (time-related) data mining** finds patterns in data where **time** matters: time-series and sequence data. Examples include stock prices, sales, sensor readings and web clickstreams.

### Method 1: trend analysis of time series
A time series Y = {y₁, y₂, …} is broken into **four components**:
1. **Trend (T):** the long-term upward or downward movement (sales growth over years)
2. **Cyclic (C):** long, irregular oscillations (business cycles)
3. **Seasonal (S):** patterns that repeat at fixed periods (festival sales every October)
4. **Irregular / random (I):** sudden, unpredictable changes

Y = T × C × S × I (multiplicative model)

**Techniques:**
- **Moving average:** smooth by averaging over a window, for example the 3-month average (y₁ + y₂ + y₃)/3, which removes irregular variation.
- **Least squares method:** fit a trend line y = a + bx.
- **Seasonal index:** removes the seasonal effect (deseasonalization).
- **Forecasting:** ARIMA and exponential smoothing to predict future values.

### Method 2: similarity search in time series
- Find series that are **similar** to a given query series, for example stocks that move like a given stock.
- **Steps:**
  1. **Dimensionality reduction:** keep only the first few **DFT or DWT** coefficients, or use PAA or SAX representations.
  2. **Indexing:** a multidimensional index (R-tree) on the reduced features.
  3. **Matching** with a distance measure: **Euclidean distance**, or **dynamic time warping (DTW)**, which allows shifts and stretches in time.
- Subsequence matching and whole matching.

### Method 3: sequential pattern mining
- Find **frequently occurring ordered sequences**, for example customers who buy a laptop, then a printer, then ink within 3 months.
- A sequence is an ordered list of itemsets. **Support** is the fraction of sequences that contain the pattern.
- **Algorithms:** **GSP** (Apriori-based, candidate generation), **SPADE** (vertical format), **PrefixSpan** (pattern growth, no candidate generation).
- **Uses:** customer shopping sequences, web clickstreams, DNA sequences.

### Method 4: periodicity analysis
- Find **recurring patterns**, either full periodic (every week) or partial periodic (only Mondays).
- Uses: seasonal sales, power consumption, astronomy.

---

## Q23. ⭐ Data mining and society + data mining trends

**Asked:** Oct 2023 Part B ("data mining with society"), Dec 2021 Part B ("outline data mining trends")

### Data mining and society
**1. Ubiquitous and invisible data mining**
- *Ubiquitous*: data mining is part of daily life, in shopping, search, healthcare and banking.
- *Invisible*: it is built into systems without users knowing, for example Amazon recommendations, Google search ranking, personalized ads and credit scoring.

**2. Privacy, security and social impact**
- Mining personal data can reveal private information (health, location, buying habits).
- There is a risk of **misuse**: profiling, discrimination (biased lending or hiring), surveillance, identity theft.
- Most data mining doesn't involve personal data (weather, science). The concern is mainly about **person-specific** data.

**3. Privacy-preserving data mining (PPDM)**: get valid results without revealing the underlying sensitive data.
- **Randomization / perturbation:** add noise to the data while keeping the overall distribution.
- **k-anonymity:** each record cannot be told apart from at least k−1 others on the quasi-identifiers (age, zip code, gender).
- **l-diversity:** each group has at least l distinct values of the sensitive attribute.
- **Distributed privacy preservation:** data is split across sites, and parties compute results without sharing the raw data (secure multiparty computation).
- **Downgrading mining results:** hide or generalize sensitive rules and outputs.
- **Security measures:** encryption, access control, auditing.

**4. Legal and ethical framework:**
- **Consent** and transparency
- Data protection laws (GDPR in the EU; India's **IT Act** and **DPDP Act 2023**)
- The right to be forgotten
- Fair and unbiased models

### Data mining trends
1. **Application exploration**: new domains (finance, healthcare, telecom, counter-terrorism).
2. **Scalable and interactive methods**: handle huge data efficiently; constraint-based mining with user interaction.
3. **Integration with search engines, databases, data warehouses and cloud computing**: mining as a built-in service.
4. **Mining social and information networks**: link prediction, community detection, influence analysis.
5. **Mining spatiotemporal, moving-object and cyber-physical data**: GPS, sensors, IoT.
6. **Mining multimedia, text and web data**: images, video, audio, social media.
7. **Biological and biomedical data mining**: genomics, protein analysis, drug discovery.
8. **Software engineering and system data mining**: bug detection, log analysis.
9. **Visual and audio data mining**: showing patterns as images and sound.
10. **Distributed, real-time and data stream mining**: mining data as it arrives (sensor and network traffic).
11. **Privacy protection and information security** in data mining.
12. **Big data and deep learning**: Hadoop and Spark, deep neural networks.

---

# PART A — Short answers (3 marks each)

**Data integration** — combining data from **multiple sources** (databases, files) into one coherent store. It handles schema integration (cust_id = cust_no), **redundancy** (found by correlation analysis, χ² test) and conflicting values (different units or currencies).

**Data cleaning** — filling in missing values, smoothing noisy data (binning, regression, clustering), finding and removing outliers, and fixing inconsistencies. It is the first step of preprocessing.

**Data warehouse vs database (OLTP)** — a database is operational, holds current detailed data, has frequent updates and is application-oriented. A warehouse is **subject-oriented, integrated, time-variant, non-volatile**, holds historical summarized data, is read-mostly and supports decisions.

**Uses of decision trees in a data warehouse** — classification and prediction (customer churn, credit risk); finding relevant attributes (attribute selection); generating IF-THEN rules; segmentation for targeted marketing. Easy for managers to understand.

**OLAP and OLAP tools** — Online Analytical Processing: interactive, multidimensional analysis of warehouse data with roll-up, drill-down, slice, dice and pivot. **Tools / servers:** ROLAP, MOLAP, HOLAP; products include Microsoft SSAS, Oracle OLAP, IBM Cognos, SAP BW, Tableau and Power BI.

**Data mining software** — WEKA, RapidMiner, KNIME, Orange, R, Python (scikit-learn), SAS Enterprise Miner, IBM SPSS Modeler (see Q15).

**Outlier analysis in clustering** — clustering-based outlier detection: objects that belong to **no cluster**, are **far from the nearest centroid**, or form **very small clusters** are outliers. For example, DBSCAN labels points that are not density-reachable as noise.

**Binary vs ordinal attribute** — Binary: only 2 states (0/1), either symmetric (gender) or asymmetric (test positive). Ordinal: values have a **meaningful order** but the gaps between them are unknown (small < medium < large; grades).

**Define data cube; 3-D representation** — a data cube models data in n dimensions with measures in the cells. For example, sales by **time (Q1–Q4) × item (TV, phone, computer) × location (Chennai, Delhi, Mumbai)**: each cell holds dollars_sold for one combination (see Q6 diagram).

**Bitmap indexing vs join indexing** — Bitmap: one bit vector per attribute value, fast for low-cardinality attributes and AND/OR operations. Join index: stores **precomputed joins** between the fact table and dimension rows, suited to star schemas (see Q8).

**Cluster analysis** — grouping objects into clusters with high intra-cluster similarity and low inter-cluster similarity; unsupervised learning (see Q12).

**Agglomerative vs divisive** — agglomerative is bottom-up (each object starts as its own cluster and the closest are merged), e.g. AGNES. Divisive is top-down (all objects start in one cluster, which is split), e.g. DIANA (see Q21).

**Three areas of web mining** — **web content mining** (text and images of pages), **web structure mining** (the hyperlink graph, e.g. PageRank), **web usage mining** (server logs and clickstreams for personalization and recommendations).

**KDD stages** — data cleaning → data integration → data selection → data transformation → data mining → pattern evaluation → knowledge presentation.

**OLTP vs OLAP (features)** — users: clerks vs analysts; function: daily operations vs decision support; data: current and detailed vs historical and summarized; access: read/write vs mostly read; unit of work: short transaction vs complex query; DB size: MB–GB vs GB–TB.

**BIRCH** — hierarchical clustering for large data using clustering features CF = ⟨n, LS, SS⟩ stored in a CF-tree; one scan, O(n) (see Q21).

**CHAMELEON** — hierarchical clustering using a k-NN graph that merges subclusters by relative interconnectivity and closeness; finds arbitrary shapes (see Q21).

**What is data mining / KDD?** The process of discovering interesting, useful, previously unknown patterns from large data. KDD steps: cleaning → integration → selection → transformation → **data mining** → pattern evaluation → knowledge presentation.

**Major issues (any two)** — see Q5. For example, *handling noisy and incomplete data* (noise distorts the patterns, so it needs cleaning and robust methods) and *privacy-preserving mining* (finding patterns without revealing individuals' data).

**Ways to fill missing values** — ignore the tuple, fill manually, a global constant, the attribute mean/median, the class-wise mean, or the most probable value (regression, decision tree, Bayesian).

**Need for data preprocessing** — real data is incomplete, noisy and inconsistent; quality data gives quality results; it improves accuracy, efficiency and mining time (see Q4).

**Features of two warehouse models** — Enterprise warehouse: organization-wide, all subjects, terabytes, takes years. Data mart: department-level, a subset, star schema, takes weeks. (Virtual warehouse: views over operational DBs.)

**Properties of the metadata repository** — describes the structure (schema, dimensions, hierarchies); operational metadata (lineage, currency, monitoring); summarization algorithms; source-to-warehouse mapping; performance data; business metadata (see Q7).

**Decision tree induction for classification** — a top-down recursive tree using the attribute with the highest information gain at each node. New tuples are classified by following the path from the root to a leaf (see Q9).

**Requirements of clustering** — scalability, varied attribute types, arbitrary shapes, few input parameters, robust to noise, insensitive to input order, high dimensionality, interpretability (see Q12).

**Applications of web mining** — search engine ranking (PageRank), e-commerce recommendations, personalization, website design improvement from usage logs, targeted advertising, opinion mining. Three types: web content, web structure and web usage mining.

**Types of outliers** — global, contextual and collective (see Q14).

**OLAP vs OLTP** — OLTP: day-to-day transactions, current detailed data, many short updates, ER model. OLAP: analysis and decision support, historical summarized data, read-mostly complex queries, star schema.

**Roll-up vs drill-down** — roll-up aggregates by climbing a concept hierarchy (city → country) or dropping a dimension. Drill-down goes to more detail (quarter → month).

**Five-number summary** — Minimum, Q1, Median, Q3, Maximum. Shown as a **box plot**. IQR = Q3 − Q1, and an outlier is a value more than 1.5 × IQR beyond the quartiles.

**Naive Bayes** — P(C|X) = P(X|C)P(C)/P(X), assuming class-conditional independence. Predicts the class with the highest posterior (see Notes M2 §9).

**Text mining** — extracting knowledge from unstructured text: tokenization, stop-word removal, stemming, TF-IDF, then classification or clustering (see Notes M3 §6b).

**Spatial and temporal mining** — spatial: patterns in geographic data (disease hotspots). Temporal: patterns over time (trends, seasonality, sequences).
