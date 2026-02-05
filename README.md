# 🏦 Banknote Authentication with PyTorch

A beginner-friendly machine learning project that uses a neural network to classify whether a banknote is **authentic or fake** based on image-extracted features.

## 📖 Overview

This project demonstrates fundamental concepts in deep learning and data science:

- Loading and exploring data with Pandas
- Building a custom PyTorch Dataset and DataLoader
- Creating a simple feedforward neural network
- Training with binary cross-entropy loss and Adam optimizer
- Evaluating with precision, recall, F1-score, and confusion matrix

## 📊 Dataset

The [Banknote Authentication Dataset](https://archive.ics.uci.edu/ml/datasets/banknote+authentication) contains 1,372 samples with 4 features extracted from banknote images:

| Feature   | Description                           |
| --------- | ------------------------------------- |
| Variance  | Variance of Wavelet Transformed image |
| Skewness  | Skewness of Wavelet Transformed image |
| Kurtosis  | Kurtosis of Wavelet Transformed image |
| Entropy   | Entropy of image                      |
| **Class** | 0 = authentic, 1 = fake               |

## 🛠️ Installation

This project uses [uv](https://github.com/astral-sh/uv) for dependency management.

```bash
# Clone the repository
git clone <repository-url>
cd ai-crash-course-1

# Install uv if you don't have already
curl -LsSf https://astral.sh/uv/install.sh | sh

# Install dependencies with uv
uv sync
```

## 🚀 Usage

Open and run the Jupyter notebook using the VS Code extension.

The notebook walks you through:

1. Data loading and exploration
2. Train/test split
3. Model architecture
4. Training loop
5. Evaluation and metrics

## 📁 Project Structure

```
ai-crash-course-1/
├── 01-Intro-Deep Learning with PyTorch.md
├── 02-basics.ipynb          # First training notebook with explanations
├── 03-banknotes.ipynb          # Main training notebook with explanations
├── data/
│   └── banknotes.csv    # Dataset
├── models/              # Saved model weights (.pth files)
├── pyproject.toml       # Project dependencies
└── README.md
```

## 🧠 Model Architecture

```
Input (4 features) → Linear(4, 10) → ReLU → Linear(10, 1) → Sigmoid → Output
```

- **Parameters**: 61 trainable weights
- **Loss**: Binary Cross-Entropy with Logits
- **Optimizer**: Adam (lr=0.001)

## 📈 Results

The model achieves high accuracy on the test set. Check the notebook for:

- Training/test loss curves
- Classification report (precision, recall, F1)
- Confusion matrix visualization

## 🔧 Requirements

- Python >= 3.13
- PyTorch >= 2.9
- Pandas, Matplotlib, Seaborn, Scikit-learn

## 📝 License

MIT License

## 👤 Author

Norbert Horgas

## Certificate of completion

[Follow the link](https://horbee-certs.netlify.app/)
