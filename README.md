# Datasets

This repository contains two datasets used for fine-tuning and evaluating defect-classification performance in this study:

- **#3DBenchy Dataset** — a custom FDM 3D-printing dataset created using controlled printing defects.
- **MVTec AD — Screw Subset** — a standard industrial anomaly-detection benchmark widely used in manufacturing research.

Both datasets were preprocessed, split, and augmented consistently to support incremental fine-tuning experiments and comparative evaluation.

---

## #3DBenchy Dataset

### Overview

The **#3DBenchy dataset** was created specifically for this project using a **Bambu Lab X1C** 3D printer with green ABS and turquoise PLA filaments. Controlled surface defects were intentionally introduced by adjusting print parameters. Each print was photographed from **left** and **right** viewpoints using a **Logitech C922 Pro webcam** (800×600 px) under ring-light illumination against a black background.

### Classes

Five defect classes were defined:

- **no_anomaly** — flawless prints
- **blobs** — small raised plastic deposits (“zits”)
- **cracks** — small separations or surface fissures
- **stringing** — thin filament strands across openings
- **warping** — curling/lifting at hull edges

### Dataset Size

- 15 printed models per class
- 2 views per model
- **30 images per class** (150 total)

### Splits

| Set | Images per class |
|-----|------------------|
| Train | 15 → augmented to 30 |
| Validation | 5 |
| Test | 10 |

### Augmentation

- Horizontal flip (y-axis)

### Preprocessing

- **Preserved original resolution** (800×600) to avoid losing fine defect detail
- **Converted to greyscale** to standardise ABS/PLA colour differences

---

## MVTec AD — Screw Subset

### Overview

The **screw subset** of the **MVTec Anomaly Detection (AD)** dataset was used due to its industrial relevance and widespread use in anomaly-detection literature. Images are high-resolution (1024×1024 px) and include a defect-free baseline plus multiple types of screw surface anomalies.

### Classes

Six classes were used:

- **good** — defect-free screws
- **manipulated_front** — bent or cut tips
- **scratch_head** — scratches on screw head
- **scratch_neck** — scratches around the neck
- **thread_top** — worn or flattened upper thread region
- **thread_side** — dents or cuts on the thread side

### Class Imbalance

The full dataset contains:

- **361** good samples
- **119** defective samples across five classes

To maintain consistency across classes, only the **first 23 images per class** were used.

### Splits

| Set | Images per class |
|-----|------------------|
| Train | 8 → augmented to 30 |
| Validation | 5 |
| Test | 10 |

### Augmentation

- Horizontal flip
- 180° rotation

### Preprocessing

Following OpenAI vision-model recommendations:

- **Images downscaled from 1024×1024 to 512×512 px**
  (reduces token usage and processing time without major quality loss)

Minimal preprocessing ensured anomaly details remained intact.


## Directory Structure (Example)

```
datasets/
│
├── benchy/
│   ├── blobs/
│   ├── cracks/
│   ├── no_anomaly/
│   ├── stringing/
│   └── warping/
│
└── mvtec_screw/
    ├── good/
    ├── manipulated_front/
    ├── scratch_head/
    ├── scratch_neck/
    ├── thread_side/
    └── thread_top/
```

---

## Citations

**MVTec AD Dataset**  
Bergmann, P. et al. (2021). *The MVTec Anomaly Detection Dataset: A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection.*

**#3DBenchy model**  
Creative Commons Attribution — https://www.3dbenchy.com
