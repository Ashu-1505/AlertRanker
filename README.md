# AlertRanker
Alert Prioritization System using Learning-to-Rank (RankNet, LambdaRank, LambdaMART) A machine learning–based alert ranking framework that prioritizes network intrusion alerts using CIC-IDS 2017 data and LightGBM learning-to-rank algorithms, simulating real-world SOC alert triage.

# Alert Prioritization using Learning-to-Rank

This repository implements an **alert ranking system** for cybersecurity intrusion alerts using **learning-to-rank algorithms**. Instead of focusing on attack detection, the project prioritizes **which alerts should be investigated first**, closely mirroring real-world **Security Operations Center (SOC)** workflows.

The system is built using **LightGBM ranking models** (RankNet, LambdaRank, and LambdaMART) and evaluated on the **CIC-IDS 2017 dataset**.

---

## 📌 Problem Statement

Traditional Intrusion Detection Systems (IDS) generate a large number of alerts, overwhelming security analysts. Most systems focus on **binary classification (benign vs malicious)** but do not answer a critical operational question:

> **Which alerts are the most critical and should be handled first?**

This project addresses that gap by **ranking malicious alerts by severity/importance**, enabling efficient alert triage and reduced analyst fatigue.

---

## 🎯 Project Objectives

- Prioritize network intrusion alerts instead of only detecting them
- Apply **learning-to-rank algorithms** to cybersecurity data
- Compare RankNet, LambdaRank, and LambdaMART performance
- Simulate realistic SOC alert queues
- Visualize alert criticality and ranking behavior

---

## 📊 Dataset

- **Source:** CIC-IDS 2017
- **File Used:** `Wednesday-workingHours.pcap_ISCX.csv`
- **Type:** Flow-based network traffic dataset
- **Labels:** Multiple attack types and benign traffic

### Dataset Processing
- Only **malicious traffic** is retained (`BENIGN` samples are removed)
- Each row represents a **network flow**
- Features include flow duration, packet statistics, timing metrics, and protocol-level indicators

This setup assumes alerts are already generated and focuses purely on **alert prioritization**, aligning with real SOC pipelines.

---

## 🧠 Models Used

The following **learning-to-rank algorithms** are implemented using LightGBM:

### 1. RankNet
- Pairwise ranking model
- Optimizes cross-entropy loss over document pairs
- Baseline learning-to-rank approach

### 2. LambdaRank
- Extension of RankNet
- Uses gradients derived from ranking metrics (NDCG)
- Faster convergence and better ranking quality

### 3. LambdaMART (DART)
- LambdaRank combined with gradient-boosted decision trees
- Uses DART (Dropouts meet Additive Regression Trees)
- Best performance and robustness among the three

---

## ⚙️ Methodology

1. Load and preprocess CIC-IDS traffic data
2. Filter only attack samples
3. Encode attack labels as relevance scores
4. Clean and normalize feature space
5. Construct ranking groups to simulate alert batches
6. Train ranking models with NDCG optimization
7. Score and rank alerts based on predicted criticality
8. Compare models using ranking behavior and training time

---

## 📈 Evaluation & Visualization

The system provides:
- **Top-K critical alerts**
- **Score distribution analysis**
- **Rank vs Score scatter plots**
- **Overlay comparison across ranking algorithms**

Evaluation is based on:
- Normalized Discounted Cumulative Gain (NDCG@1, @3, @5)
- Ranking stability and separation
- Training efficiency

---

## 🛠️ Tech Stack

- **Python**
- **LightGBM**
- **Pandas / NumPy**
- **Scikit-learn**
- **Plotly (Interactive Visualizations)**

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/alert-ranking-ltr.git
   cd alert-ranking-ltr
