# 👤 Face Recognition Visualizer — Gaussian Naive Bayes

An **interactive, beautiful visualization** of face recognition using **Gaussian Naive Bayes** on the Olivetti Faces dataset. Watch the model classify **64×64 grayscale face images** in real-time with live probability distributions, confusion matrices, and per-class accuracy charts.

## 🌐 Live Demo

**[➡️ View Live Demo](https://deepthi-tr05.github.io/Gaussian-Naive-Bayes/)**

![React](https://img.shields.io/badge/React-19-61dafb?style=flat&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178c6?style=flat&logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-4.0-38bdf8?style=flat&logo=tailwindcss)
![Vite](https://img.shields.io/badge/Vite-7-646cff?style=flat&logo=vite)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-deployed-success?style=flat&logo=github)

---

## 🎯 Overview

This dashboard demonstrates **Gaussian Naive Bayes** for face classification. Each face is a **64×64 grayscale image** (4096 pixel features). The model learns the mean and variance of each pixel per subject and uses Bayes' theorem for classification — all implemented in pure TypeScript without any ML library.

### Key Stats
| Property | Value |
|---|---|
| Dataset | Olivetti Faces (simulated) |
| Image size | 64×64 pixels |
| Total features | 4096 |
| Number of subjects | 10 |
| Images per subject | 10 |
| Train / Test split | 80% / 20% |

---

## ✨ Features

### 🖼️ Interactive Face Gallery
- **2×5 grid** of test samples (mirrors sklearn matplotlib output)
- **Canvas-rendered** grayscale face images with anti-aliasing
- **Color-coded borders**: 🟢 Green for correct, 🔴 Red for wrong
- **Label overlays** showing actual → predicted subject ID

### 🔍 Sample Explorer
- Navigate through all test samples with Prev / Next buttons or a **range slider**
- **Large 192×192 face preview**
- Three-panel display: Result, Actual Subject ID, Predicted Subject ID
- **Top-5 class probability bars** with color-coded confidence
- **Confidence score** for the top prediction

### 🎭 Mean Faces per Subject
- **Average face** computed for each subject from training images
- Shows what the model's Gaussian mean "looks like" per class

### 📊 Confusion Matrix
- **10×10 heatmap** of predictions vs ground truth
- Color-coded: green diagonal (correct), red off-diagonal (errors)
- Intensity encodes count magnitude
- Tooltips with exact values on hover

### 📈 Per-Class Accuracy
- Bar chart showing accuracy per subject
- Gradient bars (amber → orange → rose)

### 💻 Python Code Preview
- Toggle to view equivalent Python/sklearn source code
- Line-numbered display

### 🎨 Beautiful Design
- **Warm amber/orange/rose** theme
- **Animated gradient orbs** in background
- **Canvas-rendered** faces with smooth scaling
- Full **dark theme** with glassmorphism panels

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/deepthi-tr05/Gaussian-Naive-Bayes.git
cd Gaussian-Naive-Bayes

# Install dependencies
npm install

# Start development server
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

### Build for Production

```bash
npm run build
```

---

## 📚 The Algorithm

### Gaussian Naive Bayes

For each class `c` and feature `j`, the model learns:

```
μ_cj  = mean of feature j across all training samples in class c
σ²_cj = variance of feature j across all training samples in class c
```

**Prediction** using Bayes' theorem (in log-space for numerical stability):

```
log P(class | x) ∝ log P(class) + Σ_j log P(x_j | class)
```

Where each `P(x_j | class)` follows a **Gaussian (Normal) distribution**:

```
P(x_j | c) = (1 / √(2π σ²_cj)) × exp(-(x_j - μ_cj)² / (2 σ²_cj))
```

### Why Naive Bayes for Faces?
- ⚡ **Fast training** — closed-form solution, no iterations
- 📐 **Scales to high dimensions** — handles 4096 features easily
- 🎯 **Surprisingly good** despite the feature-independence assumption
- 🔢 **Probabilistic outputs** — gives confidence scores per class

### Python Equivalent (sklearn)

```python
from sklearn.datasets import fetch_olivetti_faces
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score

d = fetch_olivetti_faces()
X_train, X_test, y_train, y_test = train_test_split(
    d.data, d.target, test_size=0.2, random_state=42
)

model = GaussianNB().fit(X_train, y_train)
predictions = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, predictions))
```

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **React 19** | UI framework |
| **TypeScript** | Type safety |
| **Vite 7** | Build tool |
| **Tailwind CSS 4** | Styling |
| **Lucide React** | Icons |
| **HTML5 Canvas** | Face image rendering |
| **Custom GaussianNB** | Pure TypeScript ML implementation |

---

## 📁 Project Structure

```
Gaussian-Naive-Bayes/
├── .github/
│   └── workflows/
│       └── deploy.yml         # GitHub Pages auto-deploy
├── src/
│   ├── data/
│   │   └── olivettiFaces.ts   # Dataset generator + GaussianNB implementation
│   ├── utils/
│   │   ├── cn.ts              # Class name utility
│   │   └── pca.ts             # PCA implementation
│   ├── App.tsx                # Main dashboard UI
│   ├── main.tsx               # React entry point
│   └── index.css              # Global styles (Tailwind)
├── index.html                 # HTML entry point
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

---

## 🔬 Algorithm Complexity

| Operation | Complexity |
|---|---|
| Training | O(n · d) — n samples, d features |
| Prediction | O(c · d) — c classes, d features |
| Space | O(c · d) — stores means & variances |

---

## 🎓 Educational Value

### Learn About
- **Image classification** fundamentals
- **Gaussian distributions** in machine learning
- **Bayes' theorem** applied to real data
- **Confusion matrices** and their interpretation
- **Feature independence** assumption and when it works
- **Generative vs discriminative** models

### Key Insights
- Naïve Bayes works well even for correlated features (pixels)
- Mean faces reveal what the model "memorizes" per class
- Confidence scores expose model uncertainty
- Confusion matrix shows systematic misclassifications

---

## 🤝 Contributing

Contributions are welcome! Some ideas:

- [ ] Load real Olivetti dataset via API
- [ ] Add data augmentation visualization
- [ ] Compare with KNN, SVM, or Neural Nets
- [ ] PCA visualization for dimensionality reduction
- [ ] Interactive feature (pixel) selection
- [ ] Eigenfaces / PCA implementation

---

## 📝 License

MIT License — feel free to use, modify, and distribute.

---

## 🙏 Acknowledgments

- Dataset inspired by the [Olivetti Faces dataset](https://scikit-learn.org/stable/datasets/real_world.html#olivetti-faces-dataset) from AT&T Laboratories Cambridge
- Algorithm reference: sklearn's [GaussianNB](https://scikit-learn.org/stable/modules/naive_bayes.html#gaussian-naive-bayes)

---

**Made with ❤️ for educational purposes**

*Understanding face recognition through beautiful, interactive visualizations*
