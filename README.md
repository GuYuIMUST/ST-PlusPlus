# ST-EAS+DRF

Official PyTorch implementation of:

> **ST-EAS+DRF: Enhancing Semi-Supervised Semantic Segmentation through Unique Self-Training and Improved DeepLabV3+ Network**
>
> Xiaodong Wu, Yu Gu,Shuaikang Yang Lidong Yang, Baohua Zhang, Jing Wang, Xiaoqi Lu, Jianjun Li, Xin Liu, Dahua Yu, Ying Zhao, Siyuan Tang, Ru Shi, Nan Wang, Qun He

------

## Introduction

Semantic segmentation usually requires a large amount of pixel-level annotations, which are expensive and time-consuming to obtain.

This work proposes **ST-EAS+DRF**, an enhanced self-training framework for semi-supervised semantic segmentation. Based on the ST++ framework, we introduce:

- **Entropy Selection (ES)** for more reliable pseudo-label ranking
- **Adaptive Data Augmentation (ADA)** using dynamic Gaussian noise
- **Self-Correcting Loss (SCL)** for robust optimization
- **Division Rate and Factorized Convolutions (DRF)** for improving DeepLabV3+

The proposed method improves segmentation accuracy while reducing model complexity and training time.

------

## Main Contributions

### Entropy Selection (ES)

A novel pseudo-label quality evaluation strategy based on entropy estimation is introduced to rank unlabeled samples more accurately.

### Adaptive Data Augmentation (ADA)

Dynamic Gaussian noise with adaptive variance is added according to pseudo-label quality, improving robustness and diversity.

### Self-Correcting Loss (SCL)

A self-correcting loss function is proposed to alleviate class imbalance and noisy pseudo-label effects during training.

### DRF Module

The ASPP module in DeepLabV3+ is redesigned by:

- Factorized convolutions
- Additional dilation-rate branches
- Larger receptive fields
- Fewer parameters

resulting in higher accuracy and shorter training time.

------

## Network Architecture

```text
Input Image
      │
      ▼
 Teacher Network
      │
      ▼
Pseudo Label Generation
      │
      ▼
Entropy Selection
      │
 ┌────┴────┐
 │         │
High-quality  Low-quality
Samples       Samples
 │             │
 ▼             ▼
Adaptive Data Augmentation
      │
      ▼
Student Network
      │
      ▼
Self-Correcting Loss
      │
      ▼
DeepLabV3+ DRF
      │
      ▼
Segmentation Output
```

------

## Dataset

### Pascal VOC 2012

Download:

- JPEGImages
- SegmentationClass

Dataset structure:

```text
dataset/
├── VOC2012
│   ├── JPEGImages
│   ├── SegmentationClass
│   └── ImageSets
```

------

## Project Structure

```text
├── dataset
├── model
├── outdir
├── pretrained
│
├── LICENSE
├── main.py
├── myloss.py
├── revise.py
├── utils.py
└── README.md
```

------

## Environment

```bash
Python 3.9+
PyTorch 2.0+
CUDA 11.8+
```

Install dependencies:

```bash
pip install -r requirements.txt
```

------

## Training

### Supervised Pretraining

```bash
python main.py \
    --dataset pascal \
    --batch-size 16 \
    --backbone resnet101
```

### ST-EAS Training

```bash
python main.py \
    --dataset pascal \
    --batch-size 16 \
    --use_es \
    --use_ada \
    --use_scl
```

### ST-EAS+DRF Training

```bash
python main.py \
    --dataset pascal \
    --batch-size 16 \
    --use_es \
    --use_ada \
    --use_scl \
    --use_drf
```

------

## Experimental Results

### Pascal VOC 2012

| Method     | 1/16      | 1/8       | 1/4       |
| ---------- | --------- | --------- | --------- |
| ST++       | 73.07     | 74.60     | 74.66     |
| ST-EAS     | 74.06     | 75.19     | 75.66     |
| ST-EAS+DRF | **74.39** | **76.11** | **76.29** |

------

## Ablation Study

| Module | Description                               |
| ------ | ----------------------------------------- |
| ES     | Entropy Selection                         |
| ADA    | Adaptive Data Augmentation                |
| SCL    | Self-Correcting Loss                      |
| DRF    | Division Rate and Factorized Convolutions |

All modules contribute positively to segmentation performance.

------

## Advantages

- Higher pseudo-label quality
- Stronger data robustness
- Better segmentation accuracy
- Fewer network parameters
- Faster training speed

------

## Citation

```bibtex
@article{st_eas_drf,
  title={ST-EAS+DRF: Enhancing Semi-Supervised Semantic Segmentation through Unique Self-Training and Improved DeepLabV3+ Network},
  author={Yang, Shuaikang and Gu, Yu and others},
  year={2025}
}
```

------

## Contact

**Xiaodong Wu**

Email: [eastonvv@163.com](mailto:最好是学校官邮@stu.imust.edu.cn)

**Yu Gu (Corresponding Author)**

Email: [guyu2010023@imust.edu.cn](mailto:guyu2010023@imust.edu.cn)
