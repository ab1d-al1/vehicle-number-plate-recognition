# Vehicle Number Plate Detection and Recognition

A deep-learning-based **Automatic License Plate Recognition (ALPR)** project that detects vehicle number plates and recognizes their characters using computer vision and transformer-based OCR.

This project compares three object detection models — **YOLOv8, Faster R-CNN, and SSD300** — and uses **PARSeq Transformer OCR** for number plate text recognition.

## Project Overview

The system follows a two-stage pipeline:

1. **License Plate Detection:** Detects and localizes number plates using YOLOv8, Faster R-CNN, or SSD300.
2. **Number Plate Recognition:** Extracts detected plate regions and recognizes their characters using PARSeq OCR.

The project evaluates individual detection models and the complete detection-plus-recognition pipeline.

## Models Used

| Task | Model |
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

The detector and end-to-end results below were obtained using a **100-image evaluation subset containing 100 ground-truth plate boxes**. These are evaluation-subset results, not full-dataset results.

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

**Note:** OCR-only results use ground-truth plate crops. They are separate from end-to-end results, where PARSeq receives plate regions produced by the detection models.

## Results and Observations

- **YOLOv8:** Provides a strong balance of precision, recall, F1-score, and inference speed in the reported evaluation.
- **Faster R-CNN:** Achieves the highest recall, AP metrics, and end-to-end exact plate match, but has higher inference time and more false positives.
- **SSD300:** Shows lower recall and overall performance in this evaluation and requires further improvement.
- **PARSeq:** Achieves 76.50% exact plate match and 93.16% character accuracy on the separate ground-truth crop evaluation.

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
- PyTorch
- TorchVision
- OpenCV
- NumPy
- Pandas
- Matplotlib
- Ultralytics YOLOv8
- Faster R-CNN
- SSD300
- PARSeq Transformer
- Optical Character Recognition (OCR)

## Repository Structure

```text
vehicle-number-plate-recognition/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── FasterRCNN.ipynb
│   ├── SSD300_PARSeq.ipynb
│   ├── UFPR_ALPR_Three_Model_100_Image_Evaluation (1).ipynb
│   └── Yolo_PARseq.ipynb
│
├── docs/
│   └── methodology.md
│
├── examples/
│   ├── README.md
│   └── demo/
│       ├── vehicle_01.png
│       ├── vehicle_02.png
│       └── vehicle_03.png
│
└── results/
    ├── README.md
    ├── model_comparison.csv
    └── parseq_ocr_results.csv
```

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/ab1d-al1/vehicle-number-plate-recognition.git
cd vehicle-number-plate-recognition
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install PyTorch and TorchVision

Install compatible versions of PyTorch and TorchVision using the official installation selector:

[PyTorch Installation Guide](https://pytorch.org/get-started/locally/)

Choose the configuration appropriate for your operating system and CPU/CUDA environment.

### 4. Install the remaining dependencies

```bash
pip install -r requirements.txt
```

### 5. Open the notebooks

```bash
jupyter notebook
```

Open the required notebook from the `notebooks/` directory.

**Reproducibility note:** The notebooks may require dataset files, trained model checkpoints, and environment-specific paths from the original training environment. These assets are not currently included in this repository. Configure the required paths and obtain the necessary data and model files before running the notebooks.

## Current Scope and Limitations

- The reported detector comparison is based on a 100-image evaluation subset, not the complete UFPR-ALPR dataset.
- The UFPR-ALPR dataset is not distributed in this repository.
- Trained model checkpoints are not currently included.
- A standalone inference script and upload-based demo application are not yet included.
- The notebooks may require additional configuration to run outside the original training environment.
- Performance may vary with lighting, image quality, viewing angle, and plate visibility.
- Real-world deployment requires further testing, validation, and appropriate authorization.

## Future Improvements

- Improve SSD300 detection performance.
- Optimize model inference speed.
- Improve OCR accuracy under challenging image conditions.
- Evaluate on larger and more diverse test sets.
- Develop a standalone inference pipeline.
- Build an interactive application for image upload and number plate recognition.

## Disclaimer

This project is intended for educational and research purposes. License plate recognition may involve personal data. Use the system only where legally authorized and handle collected data responsibly.

## Acknowledgements

Thanks to the researchers who developed and made the UFPR-ALPR dataset available for academic research.
