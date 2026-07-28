# Assignment 7 — Customer Segmentation using K-Means Clustering and PCA

## Objective
A shopping mall wants to divide its customers into different groups based on their annual income and spending behavior, in order to run more effective targeted marketing campaigns. This project builds a K-Means clustering model to segment customers and applies Principal Component Analysis (PCA) to visualize the resulting clusters in two dimensions.

## Dataset Link
Mall Customer Segmentation Dataset (Kaggle):
https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python

The dataset contains 200 customer records with 5 columns: `CustomerID`, `Gender`, `Age`, `Annual Income (k$)`, and `Spending Score (1-100)`. It is not included in this repository — download it from the Kaggle link above, or fetch it via `kagglehub` as shown in the notebook.

## Libraries Used
- pandas
- numpy
- scikit-learn (`KMeans`, `PCA`, `StandardScaler`)
- matplotlib
- kagglehub (for dataset download in Colab)

## Methodology
1. **Data Understanding** — Loaded the dataset (200 rows x 5 columns), inspected the first five records, and confirmed the feature types: `Age`, `Annual Income (k$)`, and `Spending Score (1-100)` are numerical, while `Gender` is categorical. `describe()` showed the dataset spans ages 18-70, income $15k-$137k, and spending scores 1-99, with no missing values.
2. **Data Preprocessing** — Confirmed there were zero missing values across all columns. Dropped `CustomerID` (a non-informative identifier). Encoded `Gender` as 0 (Male) / 1 (Female). Standardized `Gender`, `Age`, `Annual Income (k$)`, and `Spending Score (1-100)` using `StandardScaler` so all features contribute equally to distance calculations.
3. **Model Development** — Ran the Elbow Method across K = 1-10 and selected **K = 5** as the optimal number of clusters based on where the WCSS curve bends. Trained a `KMeans` model with K=5, assigned a cluster label to every customer, then applied PCA to compress the four standardized features into 2 principal components for visualization.
4. **Visualization and Evaluation** — Plotted the elbow curve, a scatter plot of clusters by Annual Income vs. Spending Score, and a PCA-based 2D visualization of the clusters, then computed the average Age, Income, and Spending Score per cluster to interpret each segment.

## Results

**PCA variance explained:**
- Principal Component 1: 33.69% of variance
- Principal Component 2: 26.23% of variance
- **Total variance retained in 2D: 59.92%**

**Cluster profiles** (average values per cluster):

Cluster 0 — Age: 32.7, Income: $86.5k, Spending Score: 82.1
  → High income, high spenders (premium/target customers for loyalty programs)

Cluster 1 — Age: 36.5, Income: $89.5k, Spending Score: 18.0
  → High income, low spenders (price-sensitive despite having money to spend)

Cluster 2 — Age: 49.8, Income: $49.2k, Spending Score: 40.1
  → Mid income, mid-low spenders (older, moderate/standard segment)

Cluster 3 — Age: 24.9, Income: $39.7k, Spending Score: 61.2
  → Lower income, high spenders (younger, impulsive spending behavior)

Cluster 4 — Age: 55.7, Income: $53.7k, Spending Score: 36.8
  → Mid income, lower-mid spenders (oldest, more conservative segment)

### Observations

1. **Optimal number of clusters:** The elbow curve showed WCSS dropping sharply through the first few values of K and flattening out around K = 5, indicating that 5 clusters capture the meaningful structure in the data without overfitting to noise.
2. **How PCA helps visualize high-dimensional data:** The clustering used four standardized features (Gender, Age, Income, Spending Score), which can't be plotted directly. PCA compressed this into two components that together retain about 60% of the total variance, making it possible to see the cluster separation on a single 2D scatter plot.
3. **Characteristics of the identified customer groups:** The clusters clearly separate by income and spending combination rather than by income alone — for example, Cluster 0 (high income, high spending) and Cluster 1 (high income, low spending) have almost identical average income (~86-89k) but completely different spending behavior (82 vs 18), showing that income alone would not have distinguished these two very different customer types.
4. **Age as a secondary pattern:** Younger customers (Cluster 3, avg. age ~25) tend to have lower income but higher spending scores, while older customers (Clusters 2 and 4, avg. age ~50-56) show more moderate, conservative spending regardless of income — suggesting age-related spending habits alongside the income/spending split.

## Conclusion
This project applied K-Means clustering to segment 200 mall customers based on age, gender, annual income, and spending score, using standardized features and PCA for visualization. The Elbow Method identified K = 5 as the optimal number of clusters, revealing distinct customer segments — most notably two high-income groups with opposite spending behavior (82.1 vs. 18.0 average spending score) and a younger, lower-income group with disproportionately high spending (61.2). PCA reduced the four-dimensional feature space to two components while retaining about 60% of the total variance, enabling clear visualization of cluster separation. These segments have direct business value: the mall could design loyalty and premium offers for high-income, high-spending customers, targeted incentives to convert high-income, low-spending customers, and budget-friendly promotions for the older, lower-spending segments. One limitation of K-Means is that it assumes roughly spherical, similarly-sized clusters and requires K to be chosen in advance, which may not reflect the true shape of customer groups. A key advantage of PCA is that it condenses multiple correlated features into a small number of components that capture most of the meaningful variance, making complex customer data interpretable without needing to manually pick which two raw features to plot.
