# 🌬️ Predictive Maintenance for Wind Turbines using Deep Learning

**Project ReneWind**  
Date: June 13, 2025

## 📌 Overview

Wind turbines are essential for sustainable energy generation but are prone to costly breakdowns. This project builds a deep learning-based predictive maintenance system to anticipate generator failures using sensor data from wind turbines, aiming to reduce downtime and maintenance costs.

---

## 🎯 Project Goals

- Predict turbine generator failures using anonymized sensor data.
- Enable **proactive maintenance** by detecting early signs of failure.
- Build and evaluate multiple deep learning models, selecting the most robust for deployment.

---

## 🔍 Data Description

- **Input**: 40 anonymized sensor features (`V1` to `V40`).
- **Target**: Binary (0 = No Failure, 1 = Failure).
- **Imbalance**: Only ~5.5% of samples are failures.
- **Preprocessing**:
  - Missing value imputation using median strategy.
  - Outlier detection (no treatment applied).
  - No feature engineering or encoding needed.

---

## 📊 Exploratory Data Analysis

### Univariate Analysis:
- Distribution, skewness, and outliers visualized using custom `histogram_boxplot()` function.

### Bivariate Analysis:
- Correlation heatmaps to assess redundancy.
- V18, V21, V15, V7, V16 showed moderate correlation with failure.

---

## 🧠 Model Development

Framework: **TensorFlow / Keras (Sequential API)**

### Evaluation Metric Focus:
- **Recall** for Class 1 (Failures) prioritized over Accuracy due to class imbalance.

### Models Built:
- **Model 0 to Model 6**: Progressed from simple architectures to deeper networks with dropout and advanced optimizers.

| Model | Layers/Optimizer | Recall (Val) | F1 Score (Val) | Notes |
|-------|------------------|---------------|----------------|-------|
| 0     | 1 layer / SGD    | 0.81          | 0.88           | Baseline |
| 3     | Shallow / No reg.| 0.94          | 0.94           | Underfit |
| 4     | Deep / No dropout| 0.96          | 0.96           | Overfit risk |
| **5** | 3 layers / Adam + Dropout | **0.94** | **0.96** | ✅ Best Generalization |
| 6     | No reg / shallow | 0.49          | 0.49           | Poor learning |

---

## 🏆 Final Model - Model 5

**Architecture**:
- 3 Hidden Layers: `[128, 64, 32]`
- Activation: `ReLU`
- Dropout: `0.5`
- Optimizer: `Adam`
- Output Layer: `Sigmoid`

### Performance:
| Dataset | Accuracy | Precision | Recall | F1 Score |
|---------|----------|-----------|--------|----------|
| Train   | 0.99     | 0.99      | 0.96   | 0.97     |
| Val     | 0.99     | 0.99      | 0.94   | 0.96     |
| Test    | 0.99     | 0.99      | 0.95   | 0.97     |

### Why Model 5?
- Best trade-off between performance and generalization.
- Smooth and stable training curves with no overfitting.
- High recall = early failure detection.
- High precision = fewer false alarms.

---

## 📌 Actionable Insights

- **Deeper architectures** with dropout yield better performance.
- **Adam optimizer** significantly improves training efficiency.
- **Class imbalance** mitigation via class weighting proved essential.
- **Model 5** is deployment-ready with minimal tuning required.

---

## 🛠 Suggested Next Steps

1. 🚀 **Deploy Model 5** for live turbine failure prediction.
2. 🔄 **Set up automated retraining** to handle data drift.
3. ⚙️ **Monitor false positives/negatives** for ongoing improvement.
4. 🧪 **Incorporate additional data**:
   - Failure types
   - Environmental stressors
   - Vibration/acoustic sensors
   - Technician notes (for future NLP integration)

---

## 💼 Business Impact

- Up to **94% reduction** in missed failure predictions.
- Significant reduction in **unplanned downtime** and **maintenance costs**.
- Foundation laid for **scalable predictive maintenance systems** in wind energy.

---

## 🙌 Acknowledgments

Thanks to the ReneWind team and all contributors for providing data, domain insights, and model evaluation support.

---

## 📁 Folder Structure

```bash
├── data/                # Sensor datasets
├── notebooks/           # EDA and modeling notebooks
├── models/              # Saved model weights
├── reports/             # Performance and evaluation visuals
└── README.md            # Project overview
