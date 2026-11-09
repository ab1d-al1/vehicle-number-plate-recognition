# Vehicle Number Plate Detection and Recognition

A deep-learning-based **Automatic License Plate Recognition (ALPR)** project that detects vehicle number plates and recognizes their characters using computer vision and transformer-based OCR.

This project compares three object detection models — **YOLOv8, Faster R-CNN, and SSD300** — and uses **PARSeq Transformer OCR** for number plate text recognition.

## Project Overview

The system follows a two-stage pipeline:

1. **License Plate Detection:** Detects and localizes vehicle number plates using YOLOv8, Faster R-CNN, or SSD300.
2. **Number Plate Recognition:** Extracts and recognizes the characters from detected plate regions using PARSeq OCR.

The project evaluates individual detection models and the complete detection-plus-recognition pipeline.

## Models Used

| Task | Models |
|---|---|
| Object Detection | YOLOv8 |
| Object Detection | Faster R-CNN |
| Object Detection | SSD300 |
| Text Recognition (OCR) | PARSeq Transformer |

## Dataset

This project uses the **UFPR-ALPR dataset**.

- Original dataset: 4,500 annotated images.
- OCR training samples: 1,800.
- OCR validation samples: 900.
- OCR testing samples: 1,800.

**Important:** The dataset is not included in this repository. Obtain it directly from the official source and follow its license conditions.

- [Official UFPR-ALPR Dataset](https://web.inf.ufpr.br/vri/databases/ufpr-alpr/)
- [Dataset License Agreement](https://web.inf.ufpr.br/vri/databases/ufpr-alpr/license-agreement/)

## Model Evaluation Results

The following detector and end-to-end results were obtained using a **100-image evaluation subset containing 100 ground-truth plate boxes**. These results represent the evaluation subset, not the complete dataset.

### 1. Object Detection Performance

| Metric | YOLOv8 | Faster R-CNN | SSD300 |
|---|---:|---:|---:|
| True Positives | 97 | 100 | 57 |
| False Positives | 4 | 31 | 10 |
| False Negatives | 3 | 0 | 43 |
| Precision | 96.04% | 76.34% | 85.07% |
| Recall | 97.00% | 100.00% | 57.00% |
| F1-Score | 96.52% | 86.58% | 68.26% |
| AP@0.50 | 96.92% | 99.92% | 55.16% |
| mAP@0.50:0.95 | 72.26% | 79.26% | 28.02% |
| Mean Matched IoU | 87.38% | 89.07% | 75.19% |
| Mean Inference Time / Image | 85.51 ms | 280.17 ms | 109.65 ms |

### 2. End-to-End Detection and Recognition

| Metric | YOLOv8 | Faster R-CNN | SSD300 |
|---|---:|---:|---:|
| Exact Plate Match | 73% | 75% | 46% |
| Mean Character Accuracy | 89.43% | 92.86% | 57.71% |

### 3. PARSeq OCR-Only Evaluation

PARSeq was also evaluated separately using ground-truth plate crops.

| Metric | Result |
|---|---:|
| Exact Plate Match | 1,377 / 1,800 (76.50%) |
| Character Accuracy | 93.16% |

**Note:** The PARSeq OCR-only results use ground-truth plate crops. They are separate from the end-to-end results, where the OCR model receives plate regions produced by the detection models.

## Results and Observations

- **YOLOv8:** Achieved a strong balance of precision, recall, F1-score, and inference speed in the evaluation.
- **Faster R-CNN:** Achieved the highest recall, AP metrics, and end-to-end exact plate match, but had higher inference time and more false positives.
- **SSD300:** Showed lower recall and overall performance in this evaluation and requires further improvement.
- **PARSeq:** Achieved 76.50% exact plate match and 93.16% character accuracy on the separate ground-truth crop evaluation.

Based on these results, YOLOv8 provides a strong balance between detection performance and speed, while Faster R-CNN provides higher detection coverage at a greater computational cost.

## Project Workflow

1. Dataset preparation and preprocessing.
2. Training and evaluation of YOLOv8.
3. Training and evaluation of Faster R-CNN.
4. Training and evaluation of SSD300.
5. Fine-tuning and evaluation of PARSeq OCR.
6. License plate detection and text recognition.
7. Performance comparison using evaluation metrics.

## Technologies Used

- Python
- Deep Learning
- Computer Vision
- YOLOv8
- Faster R-CNN
- SSD300
- PARSeq Transformer
- Optical Character Recognition (OCR)

## Repository Structure

The repository will be organized as follows as the project files are added:

```text
vehicle-number-plate-recognition/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── yolo_training.ipynb
│   ├── faster_rcnn_training.ipynb
│   ├── ssd_training.ipynb
│   └── parseq_ocr_training.ipynb
│
├── src/
│   ├── detection/
│   ├── recognition/
│   └── evaluation/
│
├── configs/
├── weights/
├── results/
│   ├── metrics/
│   └── visualizations/
│
└── docs/
    └── methodology.md
```

Only files actually added to the repository should be considered available.

## Future Improvements

- Improve SSD300 detection performance.
- Further optimize inference speed.
- Improve OCR accuracy under challenging lighting and image conditions.
- Evaluate on larger and more diverse test sets.
- Develop a complete real-time ALPR application.

## Disclaimer

This project is intended for educational and research purposes. License plate recognition may involve personal data. Use the system only where legally authorized and handle collected data responsibly.

## Acknowledgements

Thanks to the researchers who developed and made the UFPR-ALPR dataset available for academic research.

