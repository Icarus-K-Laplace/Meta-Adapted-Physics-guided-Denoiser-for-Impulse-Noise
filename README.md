# Meta-Adapted-Physics-guided-Denoiser-for-Impulse-Noise
MAPD is a hybrid impulse noise restoration framework. It fuses a lightweight MetaParameterNet for adaptive hyperparameter prediction, fractional spectral priors for texture preservation, and structure-aware clustering to achieve robust, high-fidelity denoising (PSNR >30dB at 60% noise) without end-to-end deep learning.
# MAPD-Denoiser 🧬
> **A hybrid restoration framework combining meta-learning, fractional spectral priors, and structure-aware clustering.**
> Designed for high-performance impulse noise removal in infrared/grayscale images.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

---

## 🔬 Key Innovations

MAPD goes beyond traditional filtering by introducing adaptive mechanisms:

1. **🧠 Meta-Parameter Network**: A lightweight CNN predicts optimal restoration hyperparameters (e.g., fractional order, relaxation factor) from the input image structure.
2. **🌊 Fractional Spectral Prior**: Utilizes fractional-order frequency domain filtering to distinguish noise from fine textures.
3. **🧩 Structure-Aware Clustering**: Groups pixels by local intensity and structural features to apply region-specific restoration weights.
4. **🔄 Multi-Scale Consistency**: Enforces structural consistency across scales during iterative restoration.

---

## 📊 Performance

Tested on `scene1.png` (512×640 infrared image):

| Noise Density | PSNR (dB) | SSIM   | FSIM   | Time (s) |
|:-------------:|:---------:|:------:|:------:|:--------:|
| **20%**       | **39.84** | **0.9857** | **0.999** | ~16s     |
| **40%**       | **34.84** | **0.9605** | **0.998** | ~25s     |
| **60%**       | **31.19** | **0.9130** | **0.994** | ~43s     |

*> Note: Results demonstrate high robustness even under extreme noise conditions.*

---

## 💡 Algorithm Overview

The MAPD pipeline consists of four stages:

1. **Feature Extraction**: Computes local intensity, edge strength, and variance.
2. **Meta-Prediction**: The MetaParameterNet predicts global hyperparameters ($\alpha$, relaxation, etc.).
3. **Clustering & Prior**: Pixels are clustered based on features + fractional spectral response.
4. **Iterative Restoration**:
   - For each noisy pixel, compute an adaptive weight $w$ based on cluster and local features.
   - Apply the core restoration rule (polynomial fit vs. median).
   - Update with relaxation and multi-scale consistency check.

---

## 🚀 Quick Start

### 1. Installation

```bash
pip install -r requirements.txt
