# Clustering Methods Analysis

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/release/python-390/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains a detailed Jupyter Notebook, `Analysis.ipynb`, that explores and applies several fundamental clustering algorithms. The project serves as a practical demonstration of K-Means and Agglomerative Hierarchical Clustering on different types of datasets.

## Project Overview

The analysis is divided into three core sections:

1.  **Image Color Quantization using K-Means:** Compressing an image by reducing its color palette. This analysis explores clustering on both 3D (RGB) and 5D (RGB + XY coordinates) feature spaces to compare the results.
2.  **Optimal Cluster Number Determination:** Applying the Elbow, Silhouette, and Calinski-Harabasz methods to a 2D dataset to find the optimal number of clusters (`k`).
3.  **Hierarchical Clustering of Nutritional Data:** Using Agglomerative Clustering to group both food items (objects) and their nutritional attributes (features) to uncover natural groupings and relationships.

## Key Findings

### 1. Image Clustering & Compression

K-Means was successfully used to perform color quantization on a high-resolution image of a parrot (`parrot3.jpg`).

*   **RGB Clustering:** Grouping pixels based solely on color resulted in a "posterized" effect, creating large, flat areas of uniform color.
*   **RGB+XY Clustering:** Including normalized pixel coordinates in the features encouraged spatially close pixels to cluster together. This produced a more "painterly" effect with contiguous, blob-like regions, effectively performing a basic form of image segmentation.
*   **Memory Compression:** By representing the image as a set of `k` centroid colors and an index map, significant memory savings were achieved. A programmatic analysis confirmed the effectiveness of this technique, achieving a **3.00x compression ratio** for k=16 when using memory-efficient data types.

| Metric                        | Original Image | Compressed (k=16) | Compression Ratio |
| ----------------------------- | :------------: | :---------------: | :---------------: |
| Size (Optimized)              |  `5167.97 KB`  |   `1722.84 KB`    |     **3.00x**     |

### 2. Optimal Number of Clusters

Three different metrics were used to determine the optimal `k` for the `elbow.txt` dataset. The analysis revealed a slight divergence in recommendations, which is common in practice.

*   **Elbow Method:** Showed a distinct "elbow" at **`k=4`**, after which the reduction in inertia diminishes.
*   **Silhouette Score:** Peaked at **`k=5`**, indicating the best balance of intra-cluster cohesion and inter-cluster separation.
*   **Calinski-Harabasz Score:** Also peaked at **`k=5`**, suggesting the strongest cluster definition at this value.

**Conclusion:** The optimal number of clusters for this dataset is likely **5**, as supported by two of the three metrics. `k=4` also presents a reasonable alternative.

### 3. Hierarchical Clustering

Agglomerative Clustering was applied to a food nutrition dataset.

*   **Clustering Food Items (Objects):** The `average` and `complete` linkage methods produced highly interpretable clusters that align with common food categories:
    1.  **Red Meats:** (e.g., `BEEF STEAK`, `LAMB LEG ROAST`)
    2.  **Processed/Canned Meats:** (e.g., `BEEF CANNED`, `SMOKED HAM`)
    3.  **Poultry & Lean Fish:** (e.g., `CHICKEN BROILED`, `HADDOCK FRIED`)
    4.  **Shellfish & Canned Fish:** (e.g., `CLAMS RAW`, `SARDINES CANNED`)
*   **Clustering Nutrients (Features):** Transposing the data to cluster the features revealed logical nutritional relationships. The analysis showed a very tight cluster between **'Fat' and 'Calories'**, indicating that fat content is the primary driver of calories in this dataset. 'Protein' and the micronutrients ('Calcium', 'Iron') formed their own distinct groups.

## Repository Structure

```
.
├── images/
│   └── parrot3.jpg        # Image used for Part 1 analysis
├── Analysis.ipynb         # Main Jupyter Notebook with all code and analysis
├── elbow.txt              # Dataset for Part 2
└── nutrient.dat           # Dataset for Part 3
```
*Note: The original `images` directory contained numerous other files; they have been omitted from this structure for clarity as they are not used in the analysis.*

## How to Run

To run this analysis yourself, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Clustering-Methods-Analysis.git
    cd Clustering-Methods-Analysis
    ```

2.  **Install the required libraries:**
    This project requires a standard scientific Python environment. You can install the necessary packages using pip:
    ```bash
    pip install numpy pandas matplotlib seaborn scikit-learn scipy imageio jupyter
    ```

3.  **Launch Jupyter and run the notebook:**
    Open and run the `Analysis.ipynb` notebook in a Jupyter environment (like Jupyter Lab or Jupyter Notebook) to see the code, visualizations, and detailed explanations.
    ```bash
    jupyter lab
    ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
