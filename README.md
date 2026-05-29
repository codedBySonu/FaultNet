# FaultNet: Seismic Fault Detection and Model Analysis

## Overview

This repository contains experiments, inference scripts, and reverse-engineering notes for the pretrained FaultNet model used for 3D seismic fault detection.

The project explores:

* Running pretrained FaultNet models on seismic volumes
* Fault detection on F3 and Kerry seismic datasets
* Visualization of seismic sections and fault predictions
* Inspection and analysis of the TorchScript model architecture
* Comparison with custom 3D U-Net baselines trained on synthetic seismic data

---

## Repository Structure

```text
FaultNet/
│
├── docs/
│   ├── faultnet_structure.txt
│   └── faultnet_parameters.txt
│
├── pretrained_weights/
│   ├── FaultNet_Gamma0.5.pt
│   ├── FaultNet_Gamma0.6.pt
│   └── FaultNet_Gamma0.7.pt
│
├── prediction.py
├── utils.py
├── README.md
```

---

## Pretrained Models

The repository includes three pretrained FaultNet models:

* FaultNet_Gamma0.5.pt
* FaultNet_Gamma0.6.pt
* FaultNet_Gamma0.7.pt

These TorchScript models can be loaded directly using:

```python
import torch

model = torch.jit.load(
    "FaultNet_Gamma0.6.pt"
)
```

---

## Datasets

Experiments were performed on:

### Synthetic Seismic Dataset

* 3D seismic cubes
* Fault labels
* Cube size: 128 × 128 × 128

### Real Seismic Surveys

* F3 Dataset
* Kerry Dataset

These datasets were used to evaluate the generalization ability of the pretrained model and custom baseline networks.

---

## Results

The pretrained FaultNet model successfully detects fault structures on real seismic surveys and produces sparse fault interpretations suitable for geological analysis.

A custom 3D U-Net baseline was also trained on synthetic seismic data and achieved:

* Validation Dice Score: 0.689

Experiments highlight the challenges of synthetic-to-real generalization in seismic fault segmentation.

---

## Model Analysis

TorchScript inspection revealed that FaultNet contains:

* BasicBlock
* Bottleneck
* HighResolutionModule
* SegSEBlock
* MCF_Block

The architecture follows a high-resolution multi-branch design with multi-scale feature fusion for preserving fault-edge information.

---

## Future Work

* Reconstruct the complete FaultNet architecture
* Compare FaultNet with 3D U-Net
* Quantitative evaluation on F3 and Kerry datasets
* Synthetic-to-real domain adaptation
* 3D fault surface extraction and visualization

---

## License

This repository is intended for research and educational purposes.
