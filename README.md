# MSCS-634 Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering

This lab explores unsupervised clustering techniques using the Wine dataset from the sklearn library. The objective was to understand how Hierarchical Clustering and DBSCAN behave when applied to real-world, multivariate data, and to evaluate their performance using visualization and clustering metrics. The work included data preparation, standardization, dendrogram analysis, cluster visualization in PCA-transformed space, and the use of intrinsic metrics such as Silhouette, Homogeneity, and Completeness scores.

## Clustering Results

**1. Hierarchical Clustering**

Hierarchical (Agglomerative) Clustering produced well-formed and meaningful clusters, especially when using n_clusters = 3, which aligns closely with the natural three-class structure of the Wine dataset. The PCA scatter plot showed distinct, compact cluster groupings, and the dendrogram revealed clear separation between the major branches.

Key observations:

- Best silhouette score occurred at 3 clusters (≈0.277), reflecting well-separated clusters.

- Homogeneity and completeness were also strong for n_clusters = 3, suggesting alignment with true class distribution.

- The dendrogram displayed clear hierarchical structure and justified selecting around 3 clusters.

Overall, hierarchical clustering successfully captured the natural grouping patterns in the wine chemical attributes.

**2. DBSCAN Clustering**

DBSCAN did not perform well on this dataset for the tested ranges of eps and min_samples. Across all parameter combinations, DBSCAN detected zero clusters and labeled all 178 points as noise.

This outcome suggests that the Wine dataset does not exhibit density-based cluster structure under common hyperparameter values.

Reasons why DBSCAN failed here:

- The dataset is high-dimensional (13 features), making density estimation more difficult.

- After scaling, the distances between points were still too uniform for DBSCAN to detect dense regions.

- DBSCAN typically works best with clusters of varying density or non-linear shapes; the Wine dataset clusters are more compact and globular.

Despite tuning across multiple parameter values, DBSCAN was unable to form clusters, resulting in NaN metrics for all evaluations.

## Insights from Results & Visualizations

- Hierarchical Clustering PCA Plot showed clear, visually interpretable separation among clusters, confirming that the dataset’s structure is compatible with distance-based partitioning.

- Dendrogram displayed clear branching, with three major cluster regions forming at reasonable linkage distances.

- DBSCAN PCA Plot: All points were displayed as noise (-1), confirming DBSCAN's inability to identify any meaningful clusters under typical parameters.

## Challenges

Challenges and Decisions Made

1. DBSCAN Parameter Sensitivity
DBSCAN is highly sensitive to eps. Even after trying multiple values (0.5, 0.8, 1.0, 1.2) and min_samples (3, 5, 8), the algorithm still returned all noise. This required careful interpretation since the algorithm did not fail—rather, the dataset was simply unsuitable for DBSCAN under standard parameter ranges.

2. High-Dimensional Density Clustering Difficulty
DBSCAN generally struggles in high-dimensional space due to the "curse of dimensionality," where distance-based density measures become less meaningful. Understanding this helped explain why DBSCAN produced no clusters despite multiple tuning attempts.

3. PCA Visualization Choices
PCA was used for 2D plotting, but dimensionality reduction inevitably distorts some relationships. The decision was made to rely on PCA strictly for visualization—not for clustering itself.

## Conclusion

This lab demonstrated that Hierarchical Clustering is well-suited for the Wine dataset, producing coherent clusters aligned with true class labels. In contrast, DBSCAN struggled due to the dataset’s structure and dimensionality, highlighting that clustering performance is highly dependent on the nature of the data and appropriate parameter choices. The exercise provided practical insight into algorithm selection, metric interpretation, and the challenges of applying density-based clustering to structured, high-dimensional datasets.
