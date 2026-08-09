# Rotor Unbalance Classification using Machine Learning

## Objective
This project identifies the location and distribution of unbalance in a two-disk flexible rotor system. By analyzing lateral shaft displacement amplitude and phase data, the system bypasses conventional, time-consuming trial-mass balancing methods in favor of a real-time, non-invasive diagnostic tool.

## Dataset & Features
The dataset consists of 20,736 experimental observations. 

**Input Features (X):**
The model utilizes four lateral shaft displacement components as the sole inputs:
*   `disp x1(m)`: Displacement along X-axis for Disk-1
*   `disp y1(m)`: Displacement along Y-axis for Disk-1
*   `disp x2(m)`: Displacement along X-axis for Disk-2
*   `disp y2(m)`: Displacement along Y-axis for Disk-2

**Target Variable (y):**
The overall unbalance class (`status`) is categorized into 4 discrete states (0, 1, 2, 3) based on the combined phase angles (ψ1, ψ2) of the two disks:
*   **0:** Disk 1 < 180°, Disk 2 < 180°
*   **1:** Disk 1 < 180°, Disk 2 >= 180°
*   **2:** Disk 1 >= 180°, Disk 2 < 180°
*   **3:** Disk 1 >= 180°, Disk 2 >= 180°

## Model Performance
Several supervised machine learning models were trained and evaluated on the displacement features using a 75/25 train-test split. 

| Model | Accuracy | Precision Range | Recall Range |
| :--- | :--- | :--- | :--- |
| **Linear SVM** | **96%** | 0.95 - 0.98 | 0.95 - 0.97 |
| **Random Forest** | 93% | 0.90 - 0.95 | 0.91 - 0.95 |
| **Logistic Regression** | 92% | 0.91 - 0.94 | 0.91 - 0.93 |
| **Decision Tree** | 91% | 0.91 - 0.92 | 0.91 - 0.92 |
| **Kernel SVM (RBF)** | 86% | 0.78 - 0.96 | 0.75 - 0.96 |
| **K-Nearest Neighbors** | 77% | 0.72 - 0.85 | 0.60 - 0.94 |

*Principal Component Analysis (PCA) was applied to reduce the 4D displacement clusters into a 2D space for decision boundary visualization.*

## Key Findings
*   **Linear Separability:** The high accuracy of the Linear SVM (96%) and Logistic Regression (92%) confirms that rotor unbalance zones are linearly separable.
*   **Geometric Overfit:** Non-linear kernels (like RBF) introduced curved boundaries that struggled to map the naturally linear unbalance zones, dropping accuracy to 86%.
*   **Feature Efficiency:** Successful classification was achieved using only displacement data (dx, dy), proving that complex angular sensors are not strictly necessary for real-time unbalance monitoring.

## Dependencies
*   `pandas`
*   `scikit-learn`
*   `matplotlib`
*   `numpy`
