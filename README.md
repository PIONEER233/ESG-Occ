# ESG-Occ: Efficiency-First Satellite-Ground Fusion for 3D Occupancy Prediction

[![Paper](https://img.shields.io/badge/Paper-PDF-blue)](link-to-your-paper)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/yourname/ESG-Occ?style=social)](https://github.com/yourname/ESG-Occ)

Official PyTorch implementation of **"ESG-Occ: Efficiency-First Satellite-Ground Fusion for 3D Occupancy Prediction"**, accepted to *ICASSP 2025* 🎉.  

<div align="center">
  <img src="assets/framework.png" width="80%">
  <p><i>Overall framework of ESG-Occ. Our EfficientSatNet extracts lightweight overhead features, while the Adaptive Weight Generation Block (AWGB) fuses them with street-view BEV features in a scene- and visibility-aware manner.</i></p>
</div>

---

## 🌟 Highlights

- **Lightweight Satellite Branch**: Introduce **EfficientSatNet**, a MobileNetV3-based feature pyramid, reducing FLOPs while preserving overhead context.
- **Adaptive Fusion**: Propose **AWGB** that dynamically balances street-view vs. satellite contributions using:
  - ProbNet (visibility-aware weighting)  
  - Complexity-aware modulation  
- **Real-Time Ready**: Achieves **64.23 ms/frame** on RTX 4090 while improving mIoU by +1.4% over heavy fusion baselines.
- **Open & Reproducible**: Code, configs, and pretrained models are publicly released.

---

## 📊 Performance on Occ3D-nuScenes

| Method        | FLOPs (G) | Latency (ms) | mIoU (%) |
|---------------|-----------|--------------|----------|
| SGFormer      | 442.19    | 87.13        | 37.95    |
| SA-Occ        | 454.02    | 91.76        | 38.61    |
| **ESG-Occ**   | **373.06**| **64.23**    | **39.38**|

*Measured on NVIDIA RTX 4090, batch size 1.*

---

## 🚀 Installation

```bash
# clone repo
git clone https://github.com/yourname/ESG-Occ.git
cd ESG-Occ

# create environment
conda create -n esgocc python=3.9 -y
conda activate esgocc

# install dependencies
pip install -r requirements.txt
````

---

## 📂 Dataset Preparation

We follow [Occ3D](https://github.com/Tsinghua-MARS-Lab/Occ3D) for data preparation.

1. Download **nuScenes** dataset and corresponding **Occ3D annotations**.
2. Organize files as:

```
datasets/
  nuscenes/
    samples/
    sweeps/
    maps/
    occ3d_annotations/
```

3. Update dataset paths in `configs/dataset.yaml`.

---

## 🏃 Training & Evaluation

### Train from scratch

```bash
python tools/train.py --cfg configs/esgocc.yaml
```

### Evaluate pretrained model

```bash
python tools/test.py --cfg configs/esgocc.yaml \
                     --ckpt checkpoints/esgocc_pretrained.pth
```

### Inference demo

```bash
python tools/demo.py --cfg configs/esgocc.yaml \
                     --ckpt checkpoints/esgocc_pretrained.pth \
                     --input data/demo/ \
                     --output results/demo/
```

---

## 📸 Visualization

<div align="center">
  <img src="assets/vis_results.png" width="80%">
  <p><i>Qualitative comparison of ESG-Occ vs. baselines. Satellite cues help recover occluded regions and far-range occupancy.</i></p>
</div>

---

## 🛠 Project Structure

```
ESG-Occ/
├── configs/           # YAML configs for model/dataset
├── datasets/          # Dataset loading & preprocessing
├── models/            # EfficientSatNet, AWGB, fusion heads
├── tools/             # train/test/demo scripts
├── assets/            # figures for README
├── checkpoints/       # pretrained weights
└── requirements.txt
```

---

## 📖 Citation

If you find this work useful, please cite our paper:

```bibtex
@inproceedings{yourname2025esgocc,
  title     = {ESG-Occ: Efficient Satellite–Ground Fusion for Real-Time 3D Occupancy Prediction},
  author    = {Your Name and Others},
  booktitle = {ICASSP},
  year      = {2025}
}
```

---

## 📬 Contact

For questions or issues, feel free to open an [issue](https://github.com/yourname/ESG-Occ/issues) or contact **[your.email@domain.com](mailto:your.email@domain.com)**.

---

## 📜 License

This project is released under the [MIT License](LICENSE).

