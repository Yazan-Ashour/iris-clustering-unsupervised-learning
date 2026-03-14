# Iris Clustering — Unsupervised Learning

## Project Overview
This project applies three unsupervised clustering algorithms to the classic Iris dataset to discover hidden patterns without using class labels during training. The labels are used only at the evaluation stage to assess how well each algorithm recovers the true species structure.

### Objectives
- Implement and compare K-Means, Hierarchical, and DBSCAN clustering
- Evaluate clusters using Silhouette Score, Accuracy, and F1-Score
- Interpret and compare results against true Iris species labels

---

## Dataset
The [Iris dataset](https://archive.ics.uci.edu/dataset/53/iris) contains:
- **150 samples** (149 after removing duplicates)
- **4 numerical features**: Sepal Length, Sepal Width, Petal Length, Petal Width
- **3 classes**: Setosa, Versicolor, Virginica

Features were normalized using `StandardScaler` before clustering.

---

## Algorithms & Results

### K-Means
- Optimal k=3 determined via the Elbow Method (SSE/WCSS)
- **Silhouette Score**: 0.4607
- **Accuracy**: 83.89% | **F1-Score**: 0.8388
- Perfectly identified all 50 Setosa samples
- Minor overlap between Versicolor and Virginica (expected)

### Hierarchical Clustering (Agglomerative)
- Tested Single, Average, and Complete linkage methods
- Best method: **Average linkage** with k=2 (highest Silhouette)
- **Silhouette Score**: 0.5810
- **Accuracy**: 67.11% | **F1-Score**: 0.5608
- Dendrograms used to visualize merge hierarchy and select optimal cut

### DBSCAN
- Optimal parameters found using **K-Distance Plot** + grid search
- Best parameters: **eps=0.75, min\_samples=5**
- Found **2 clusters**, **6 noise points**
- **Silhouette Score**: 0.6042 (computed excluding noise points)
- **Accuracy**: 68.79% | **F1-Score**: 0.5803
- Successfully separated Setosa but merged Versicolor and Virginica

---

## Final Comparison

| Algorithm | Clusters | Noise Points | Silhouette | Accuracy | F1-Score |
|-----------|----------|--------------|------------|----------|----------|
| K-Means | 3 | 0 | 0.4607 | 83.89% | 0.8388 |
| Hierarchical (Average) | 2 | 0 | 0.5810 | 67.11% | 0.5608 |
| DBSCAN | 2 | 6 | 0.6042 | 68.79% | 0.5803 |

*DBSCAN Silhouette computed on non-noise points only — not directly comparable.

### Conclusion
**K-Means** is the best overall algorithm for this dataset — it correctly identifies 3 clusters, achieves the highest accuracy and F1-score, and produces clean visually interpretable results. DBSCAN's higher Silhouette Score is misleading as it only finds 2 clusters and discards noise points from evaluation.

---

## Repository Structure
```
iris-clustering-unsupervised-learning/
│
├── iris_clustering.ipynb        # Main Jupyter notebook
├── Iris-KMeans.csv              # K-Means cluster assignments
├── IrisAgglomerativeClustering.csv  # Hierarchical cluster assignments
├── Iris-DBSCAN.csv              # DBSCAN cluster assignments
└── README.md                    # Project documentation
```

## Requirements
```
numpy
pandas
matplotlib
seaborn
scikit-learn
scipy
```
