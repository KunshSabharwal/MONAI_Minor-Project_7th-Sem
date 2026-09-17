# 🧠 An Explainable MONAI-Based Deep Learning Framework for Multi-Class Brain Tumor Classification from MRI Images

Deep learning project for **4-class brain tumor classification from MRI images**, comparing a CNN-based model with a Vision Transformer and using Explainable AI (XAI) to visualize model predictions.

## 🟠 Models

- **MONAI DenseNet121**: CNN-based classifier
- **ViT-Base (`vit_base_patch16_224`)**: Transformer-based classifier
- **Grad-CAM**: explanation method for DenseNet121
- **Patch-level relevance (Gradient × Activation)**: XAI method for ViT

## 🏛️ Classes

```text
glioma
meningioma
no_tumor
pituitary
```

## 💿 Dataset

- Dataset: Brain Tumor MRI Classification Dataset (Merged)
- Source: https://huggingface.co/datasets/usamaJabar/brain-tumor-mri-classification-merged

| Split      |   Images |
| ---------- | -------: |
| Train      |     8306 |
| Validation |      488 |
| Test       |      246 |
| **Total**  | **9040** |

Dataset structure:

```text
data/
└── brain-tumor-mri-classification/
    └── merged_dataset_v3/
        └── images/
            ├── train/
            │   ├── glioma/
            │   ├── meningioma/
            │   ├── no_tumor/
            │   └── pituitary/
            ├── val/
            └── test/
```

## 🛳️ Pipeline

```text
MRI Image
    ↓
Preprocessing (224 × 224)
    ↓
┌───────────────────┬───────────────────┐
│   DenseNet121     │        ViT         │
│      (MONAI)      │      (timm)        │
└─────────┬─────────┴─────────┬─────────┘
          ↓                   ↓
     Prediction           Prediction
          ↓                   ↓
       Grad-CAM         Patch Relevance
          ↓                   ↓
      XAI Heatmap        XAI Heatmap
```

## 📊 Evaluation

Models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- Classification Report

| Model       | Accuracy | Precision |   Recall |       F1 |
| ----------- | -------: | --------: | -------: | -------: |
| DenseNet121 | `94.72%` |  `95.22%` | `94.72%` | `94.63%` |
| ViT-Base    | `97.97%` |  `98.01%` | `97.97%` | `97.97%` |

## 🔎 Explainable AI

### DenseNet121

Grad-CAM is applied to the final DenseNet feature block to generate spatial heatmaps showing regions associated with the predicted class.

### ViT

The ViT divides the 224 × 224 image into 16 × 16 patches:

```text
224 / 16 = 14
14 × 14 = 196 patches
```

Patch-level relevance is calculated from gradient × activation, producing a 14 × 14 relevance map that is resized and overlaid on the MRI.

## 📩 Installation

### Option 1: Conda

Create the environment from the provided `environment.yml`:

```bash
conda env create -f environment.yml
conda activate brain-tumor
```

If the environment already exists:

```bash
conda env update -f environment.yml --prune
conda activate brain-tumor
```

### Option 2: Python Virtual Environment

Create and activate a virtual environment:

Windows:

```powershell
python -m venv .venv
.venv\Scripts\activate
```

Linux/macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the dependencies from `requirements.txt`:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

## ⚙️ Hardware

Tested on:

```text
GPU: NVIDIA RTX 5070 12GB
CPU: AMD Ryzen 5 7600X
RAM: 32GB
```

## 📃 License

[MIT LICENSE](./LICENSE)
