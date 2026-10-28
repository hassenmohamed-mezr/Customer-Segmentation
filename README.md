# Customer Segmentation

An introductory unsupervised machine-learning project that groups customers using
their income, spending score, and age. The notebook implements and compares
**KMeans** and **DBSCAN** clustering.

## Project Overview

The project explores how different clustering algorithms identify customer
segments without a target label:

- **KMeans** assigns each customer to the nearest centroid.
- **DBSCAN** groups customers by local density and can identify noise points.

All three input features are standardized before clustering so that income,
spending score, and age contribute on comparable scales.

## Dataset

`Customer Segmentation Dataset.csv` contains 40 customers with these columns:

| Column | Description |
| --- | --- |
| `Income (k$)` | Annual income in thousands of dollars |
| `Spending Score (1-100)` | Customer spending score |
| `Age` | Customer age |

The CSV also contains an index column (`Unnamed: 0`), which is removed during
data preparation. The notebook checks for missing values and duplicates before
scaling the features.

## Methods

### KMeans

The notebook:

1. Fits KMeans with four clusters as an initial experiment.
2. Uses the elbow method to compare inertia for `k = 1` through `k = 10`.
3. Fits a five-cluster model after reviewing the inertia curve.
4. Visualizes the resulting segments in two and three dimensions.

KMeans requires the number of clusters in advance and works best when clusters
are relatively compact and roughly spherical.

### DBSCAN

DBSCAN is evaluated with several combinations of `eps` and `min_samples`:

```text
(0.3, 3), (0.5, 3), (0.7, 3), (1.0, 3),
(0.5, 5), (0.7, 5), (1.0, 5),
(0.7, 8), (1.0, 8)
```

For each experiment, the notebook records the number of clusters and noise
points, then visualizes selected configurations in 2D and 3D. DBSCAN does not
require the number of clusters beforehand and can label outliers as noise
(`-1`), but its results are sensitive to feature scaling and parameter choices.

## Repository Contents

- [Customer Segmentation Dataset.csv](./Customer%20Segmentation%20Dataset.csv) -
  customer data used by the notebooks.
- [Customer Segmentation Task.ipynb](./Customer%20Segmentation%20Task.ipynb) -
  compact task notebook.
- [Customer_Segmentation_Task.ipynb](./Customer_Segmentation_Task.ipynb) -
  expanded notebook containing the complete workflow, experiments, and plots.

## Requirements

Use Python 3.9 or newer with the following packages:

- `pandas`
- `numpy`
- `matplotlib`
- `scikit-learn`
- Jupyter Notebook or JupyterLab

Install the dependencies with:

```bash
python -m pip install pandas numpy matplotlib scikit-learn jupyter
```

## Running the Project

1. Clone or download this repository.
2. Open a terminal in the project directory.
3. Install the dependencies listed above.
4. Start Jupyter:

   ```bash
   jupyter notebook
   ```

5. Open `Customer_Segmentation_Task.ipynb`.
6. Run the cells from top to bottom.

The notebook expects `Customer Segmentation Dataset.csv` to be in the same
directory as the notebook.

## Expected Outputs

Running the notebook produces:

- Data inspection and descriptive statistics.
- Standardized feature values.
- KMeans cluster assignments and cluster centers.
- An elbow-method inertia table and plot.
- 2D and 3D KMeans visualizations.
- A DBSCAN parameter-summary table.
- 2D and 3D DBSCAN visualizations, with noise points marked separately.
- A comparison of KMeans and DBSCAN requirements and behavior.

## Notes

Cluster labels are numeric identifiers, not business meanings. A cluster should
be interpreted by examining its feature values and centroid rather than by the
label number itself. For production use, the selected number of clusters and
DBSCAN parameters should be validated with domain knowledge and appropriate
clustering-quality metrics.
