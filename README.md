# Customer Segmentation Using RFM Analysis and K-Means

## Overview
This project segments customers of an online retail business using **RFM analysis** and **K-Means clustering**. The goal is to group customers according to their purchasing behavior and use the resulting segments to suggest suitable marketing actions.

The analysis is implemented in the Jupyter Notebook `CASE_STUDY_4.ipynb`.

## Dataset
The project uses the **Online Retail II** dataset, which contains transactions from a UK-based online retailer between December 2009 and December 2011.

- **Kaggle dataset:** https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci
- **Original UCI source:** https://archive.ics.uci.edu/dataset/502/online+retail+ii
- **Expected file name:** `online_retail_II.xlsx`

The dataset includes transaction details such as invoice number, product code and description, quantity, invoice date, unit price, customer ID, and country.

## Project Workflow
1. **Load the data** from the Excel file using Pandas.
2. **Explore the data** by checking its shape, data types, summary statistics, missing values, duplicate rows, and date range.
3. **Clean the data** by removing rows with missing values and duplicate records, then ensuring invoice dates are valid.
4. **Calculate transaction value** using `Quantity × Price`.
5. **Create customer-level RFM features:**
   - **Recency:** number of days since the customer's last purchase.
   - **Frequency:** number of distinct invoices/orders made by the customer.
   - **Monetary:** total transaction value attributed to the customer.
6. **Prepare features** by handling invalid values, applying `log1p` transformation, and standardizing the RFM features with `StandardScaler`.
7. **Select the number of clusters** by comparing K-Means inertia (Elbow method) and silhouette scores for different values of *k*.
8. **Cluster customers** using K-Means.
9. **Visualize clusters** in two dimensions using PCA. PCA is used for visualization; clustering uses all three scaled RFM features.
10. **Profile the clusters** and assign descriptive customer personas with suggested marketing actions.

## Technologies and Libraries
- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn (`StandardScaler`, `KMeans`, `PCA`, `silhouette_score`)

## Requirements
Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
```

`openpyxl` is included to support reading Excel files with Pandas.

## How to Run

### Option 1: Run locally
1. Download or clone this project and place `CASE_STUDY_4.ipynb` in your working folder.
2. Download `online_retail_II.xlsx` from the Kaggle dataset page linked above.
3. Put `online_retail_II.xlsx` in the location expected by the notebook, or update the loading cell to use your file path.
4. Install the required libraries.
5. Open Jupyter Notebook and run the cells from top to bottom.

### Option 2: Run in Google Colab
1. Upload `CASE_STUDY_4.ipynb` to Google Colab.
2. Upload `online_retail_II.xlsx` to the Colab runtime, or mount Google Drive and update the path.
3. Ensure the dataset-loading cell points to the correct location.
4. Select **Runtime → Run all**.

**Important:** The notebook currently loads the dataset from `/content/online_retail_II.xlsx`, which is a Google Colab path. If running locally, change it to the appropriate local path, for example:

```python
df = pd.read_excel("online_retail_II.xlsx")
```

## Outputs
When the notebook runs successfully, it produces:
- Dataset summaries and data-quality checks
- RFM feature summaries and distributions
- Elbow-method and silhouette-score plots for cluster selection
- Customer cluster labels and a final silhouette score
- PCA scatter plot showing customer segments
- Cluster profiles including customer counts, average recency, frequency and monetary value, revenue share, assigned persona, and recommended marketing actions

The number of clusters is selected from the tested range based on the silhouette score, so the final result may depend on the dataset and preprocessing.

## Customer Personas
The notebook maps cluster profiles to broad marketing personas, such as:
- Champions
- At-risk valuable customers
- High-spending potential customers
- Active regulars
- Recent / occasional customers
- Dormant / low-engagement customers

Each cluster is also associated with a suggested marketing action. These labels are heuristic interpretations of cluster averages, not ground-truth labels produced by a supervised model.

## Notes and Limitations
- This is an **unsupervised learning** project; there is no target label used to train K-Means.
- RFM features summarize past purchasing behavior and do not guarantee future customer behavior.
- The notebook removes rows with missing values and duplicates. Depending on the data, this may remove a substantial number of transactions.
- Review the data-cleaning rules for cancellations, negative quantities, and non-positive prices before using the segments for business decisions.
- Cluster IDs are arbitrary numeric labels. Compare cluster profiles rather than assuming a particular cluster number always represents the same persona.

## Dataset Citation
Chen, D. (2012). *Online Retail II* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D

Please follow the dataset page's license and attribution requirements when redistributing the data.
