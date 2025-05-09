# 📊 Anomalyzer: Interactive Anomaly Detection with Streamlit

A simple web app for detecting anomalies in datasets using **Isolation Forest**. Upload your CSV with features like `time` and `loc`, run unsupervised anomaly detection, visualize results, and download the labeled dataset.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

---

## 🔧 Features

- Upload CSV file with numerical features (`time`, `loc`)
- Uses **Isolation Forest** to detect outliers
- Assigns labels:  
  `1` → Normal data  
  `-1` → Anomaly  
- View results in an interactive table
- Download labeled dataset as CSV

---

## 🧠 Machine Learning Used

### ✅ Isolation Forest (Unsupervised Learning)
An ensemble-based anomaly detection algorithm. It isolates anomalies instead of profiling normal data.

#### 🧮 Anomaly Score Formula:
For a point **x** in a forest of trees **t**, the anomaly score is:

<img width="483" alt="image" src="https://github.com/user-attachments/assets/cb2315aa-4185-4902-85d6-f9b357ad785f" />

Where:
- **E(h(x))** = average path length of point x
- **c(n)** = average path length of unsuccessful search in a Binary Search Tree (BST)
- **n** = number of samples

Interpretation:
- **Score ≈ 1** → anomaly
- **Score ≈ 0.5** → normal

---

## 📦 Installation

```bash
pip install streamlit pandas scikit-learn
```



