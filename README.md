# 🧠 An Explainable MONAI-Based Deep Learning Framework for Multi-Class Brain Tumor Classification from MRI Images

A deep learning research project for **4-class brain tumor classification from MRI images**, comparing CNNs and Vision Transformers and exploring Explainable AI (XAI) techniques.

## 🟠 Models

- **MONAI DenseNet121**: CNN-based classifier
- **MONAI EfficientNet**: CNN-based classifier
- **ViT-Base (timm)**: Vision Transformer classifier
- **ViT (MONAI)**: Vision Transformer classifier
- **Swin Transformer-Tiny (timm)**: Swin Transformer classifier
- **Custom CNN + ViT Hybrid**: Proposed hybrid architecture; implementation and training are planned

### Explainable AI (XAI)

- **Grad-CAM**: Planned for conventional CNN-based models, including DenseNet121 and EfficientNet.
- **Attention Rollout**: Planned for transformer-based models, including ViT and Swin Transformer.

> The transformer-based Attention Rollout implementation is not yet complete. MONAI Swin Transformer training has not been completed, and the proposed CNN + ViT hybrid has not yet been implemented or evaluated.

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
┌──────────────────┬──────────────────┬──────────────────┐
│   DenseNet121    │    EfficientNet   │    ViT-Base      │
│     (MONAI)      │      (MONAI)      │     (timm)       │
└────────┬─────────┴────────┬─────────┴────────┬─────────┘
         ↓                  ↓                  ↓
    Prediction         Prediction         Prediction
         ↓                  ↓                  ↓
       Grad-CAM           Grad-CAM       Attention Rollout
         (Planned)          (Planned)          (Planned)

                  ViT (MONAI)
                       ↓
                  Prediction
                       ↓
                Attention Rollout
                    (Planned)

             Swin Transformer-Tiny
                     (timm)
                       ↓
                  Prediction
                       ↓
                Attention Rollout
                    (Planned)

         Proposed Custom CNN + ViT Hybrid
                (Planned, not trained)
```

## 📊 Evaluation

Models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- Classification Report

| Model                   | Accuracy | Precision |  Recall | F1-score |
| ----------------------- | -------: | --------: | ------: | -------: |
| DenseNet121 (MONAI)     |   94.72% |    95.22% |  94.72% |   94.63% |
| ViT-Base (timm)         |   97.97% |    98.01% |  97.97% |   97.97% |
| ViT (MONAI)             |   80.08% |    84.40% |  80.08% |   75.71% |
| EfficientNet (MONAI)    |   78.46% |    80.82% |  78.46% |   76.69% |
| Swin Transformer (timm) |  100.00% |   100.00% | 100.00% |  100.00% |

> Note: These are the currently reported results. The 100% Swin Transformer result has not been independently verified. Further checks for data leakage, split independence, and evaluation correctness are necessary before drawing conclusions. Results across implementations may also differ because of pretrained weights, preprocessing, and training configurations.

## 🔎 Explainable AI

### Grad-CAM for CNN-Based Models

Grad-CAM is planned for conventional CNN-based architectures such as DenseNet121 and EfficientNet. It will generate spatial heatmaps highlighting image regions that contribute to a model's predictions.

### Attention Rollout for Transformer-Based Models

Attention Rollout is planned for transformer-based architectures, including ViT and Swin Transformer. The implementation and visualization pipeline have not yet been completed.

Swin Transformer uses hierarchical, window-based attention, so its explanation method will need to account for its architecture.

### Proposed CNN + ViT Hybrid

A custom CNN branch and a ViT branch will be combined through feature fusion for four-class classification. The architecture, training, evaluation, and suitable XAI methods remain future work.

## 📩 Installation

### Option 1: Conda

Create the environment from the provided `environment.yml`:

```bash
conda env create -f environment.yml
conda activate monai
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
