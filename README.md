# Customer Segmentation Using RFM Analysis and K-Means Clustering

by **Hans Darmawan**

*This project is dedicated to the memory of the late Mr. Paulus Weli Gunawan (1973–2025).*

# Project Overview

Understanding customer purchasing behavior is essential for developing effective marketing strategies in the retail industry. Businesses often collect large volumes of transaction data, but without proper analysis it can be difficult to identify valuable insights about customer behavior.

This project performs **customer segmentation using RFM (Recency, Frequency, Monetary) analysis combined with K-Means clustering** to group customers based on their purchasing behavior. The goal is to identify meaningful customer segments that can support **data-driven marketing strategies, customer retention programs, and revenue optimization**.

The analysis results in **four customer segments** — Bronze, Silver, Gold, and Platinum — representing increasing levels of customer value.

# Dataset

This project uses the **Online Retail II dataset**, which contains transactional data from an online retail store.

The dataset includes:

* Invoice identifiers
* Product information
* Quantity purchased
* Price per item
* Transaction timestamps
* Customer identifiers
* Country information

After preprocessing and cleaning, the dataset contains:

* **638,249 transaction records**
* **5,654 unique customers**

# Methodology

The project follows a structured data science workflow:

### 1. Data Understanding

* Load and inspect the dataset
* Analyze dataset structure and data types
* Check for missing values and duplicate records

### 2. Data Cleaning

* Remove duplicate transactions
* Filter invalid transactions:

  * negative quantities
  * negative prices
  * canceled transactions
  * guest purchases
  * price and quantity outliers

### 3. Feature Engineering

Customer-level **RFM features** are calculated:

* **Recency** – days since last purchase
* **Frequency** – number of transactions
* **Monetary** – total spending amount

### 4. Data Transformation

To improve clustering performance:

* **Log transformation (log1p)** is applied to reduce skewness
* **RobustScaler** is used to normalize feature scales

### 5. Determining Optimal Clusters

Two methods are used:

* **Elbow Method**
* **Silhouette Score**

Both methods indicate that **4 clusters** provide a good balance between model simplicity and clustering quality.

### 6. Customer Segmentation

Customers are segmented using **K-Means clustering**, and clusters are labeled according to their median monetary value:

* Bronze
* Silver
* Gold
* Platinum

### 7. Cluster Evaluation

Clusters are evaluated using:

* **Cluster profiling**
* **RFM median comparison**
* **Kruskal–Wallis statistical test**

Statistical testing confirms that the clusters are **significantly different in terms of Recency, Frequency, and Monetary behavior**.

### 8. Visualization

Customer segments are visualized using:

* Distribution plots
* Cluster heatmaps
* Donut charts
* Interactive **3D cluster visualization**

# Customer Segments

| Segment      | Characteristics                                                   |
| ------------ | ----------------------------------------------------------------- |
| **Bronze**   | Long inactivity, low purchase frequency, low spending             |
| **Silver**   | Recent purchases with moderate spending                           |
| **Gold**     | High historical spending but less recent activity                 |
| **Platinum** | Highly active customers with frequent purchases and high spending |

These segments can help businesses design **targeted marketing strategies**.

# Example Customer Prediction

The trained clustering model can classify new customers based on their RFM values.

Example input:

```
Recency = 10 days
Frequency = 5 purchases
Monetary = $120
```

The pipeline applies:

1. Log transformation
2. Feature scaling
3. K-Means cluster prediction

The result is mapped to the corresponding **customer segment label**.

# Project Structure

```
OR2MRFM-1
│
├── datasets
│   └── online-retail-ii-cleaned.csv.zstd
│
├── environments
│   └── environment.yml
│
├── notebooks
│   └── code.ipynb
│
├── outputs
│   ├── kmeans_rfm_model.pkl
│   ├── rfm_cluster_heatmap.png
│   ├── rfm_cluster_map.pkl
│   ├── rfm_cluster_profile.csv
│   ├── rfm_customer_segmentation.csv
│   └── rfm_scaler.pkl
│
└── README.md
```

### Folder Description

**datasets/**
Contains the cleaned transaction dataset used for the analysis.

**environments/**
Stores the environment configuration file (`environment.yml`) to reproduce the project dependencies.

**notebooks/**
Contains the main Jupyter notebook (`code.ipynb`) where the entire data analysis and modeling pipeline is implemented.

**outputs/**
Stores all generated artifacts from the analysis, including:

* trained **K-Means model**
* **feature scaler**
* **cluster mapping**
* **cluster profiling results**
* **customer segmentation results**
* **visualization outputs**

**README.md**
Project documentation explaining the methodology, dataset, analysis workflow, and results.

# Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* SciPy
* Seaborn
* Matplotlib
* Plotly
* Joblib

# Key Insights

* Customer behavior in retail data is **highly skewed**, requiring transformation before clustering.
* **Platinum customers contribute the highest value** through frequent purchases and high spending.
* A significant portion of customers fall into the **Bronze segment**, indicating opportunities for engagement strategies.
* RFM segmentation combined with clustering provides a **simple yet powerful framework for customer analytics**.

# Future Improvements

Possible improvements include:

* Incorporating **Customer Lifetime Value (CLV)**
* Adding **product category analysis**
* Testing other clustering algorithms:

  * DBSCAN
  * Hierarchical Clustering
  * Gaussian Mixture Models
* Building a **dashboard for marketing teams**
* Deploying the model into a **real-time segmentation pipeline**