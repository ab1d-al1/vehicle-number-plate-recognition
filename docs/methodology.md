# Project Methodology

## 1. Introduction

This project implements an Automatic License Plate Recognition (ALPR) system using deep learning and computer vision.

The objective is to detect vehicle number plates and recognize the characters present on them.

Three object detection models are compared:
- YOLOv8
- Faster R-CNN
- SSD300

PARSeq Transformer is used for optical character recognition (OCR).

## 2. Dataset

The project uses the UFPR-ALPR dataset.

- Original dataset: 4,500 annotated images.
- OCR training samples: 1,800.
- OCR validation samples: 900.
- OCR testing samples: 1,800.

The dataset is not distributed with this repository.

Official dataset:
https://web.inf.ufpr.br/vri/databases/ufpr-alpr/

## 3. System Architecture

The system consists of two primary stages.

### Stage 1: License Plate Detection

The input vehicle image is processed by an object detection model.

The project compares:
- YOLOv8
- Faster R-CNN
- SSD300

Each detector identifies the license plate region and produces bounding-box coordinates.

### Stage 2: Character Recognition

The detected plate region is used as input to the PARSeq Transformer OCR model.

PARSeq processes the plate image and predicts the text sequence representing the vehicle number.

## 4. Model Evaluation

The object detection models are compared using:

- Precision
- Recall
- F1-score
- Average Precision (AP@0.50)
- Mean Average Precision (mAP@0.50:0.95)
- Mean Intersection over Union (IoU)
- Mean inference time

The complete detection and recognition pipeline is evaluated using:

- Exact plate match
- Mean character accuracy

The detector comparison uses a 100-image evaluation subset containing 100 ground-truth plate boxes.

PARSeq is also evaluated separately using ground-truth plate crops.

## 5. Evaluation Summary

### YOLOv8

Provides a strong balance of detection performance and inference speed.

### Faster R-CNN

Achieves the highest recall and AP metrics in the reported evaluation, with higher inference time.

### SSD300

Shows lower detection performance in the reported evaluation and requires further improvement.

### PARSeq

Achieves 76.50% exact plate match and 93.16% character accuracy in the separate OCR-only evaluation.

## 6. Project Workflow

1. Dataset preparation and preprocessing.
2. Object detection model training.
3. License plate localization.
4. Plate region extraction.
5. PARSeq OCR recognition.
6. Model evaluation.
7. Performance comparison.

## 7. Technologies

- Python
- PyTorch
- TorchVision
- Ultralytics YOLOv8
- Faster R-CNN
- SSD300
- PARSeq Transformer
- OpenCV
- NumPy
- Pandas
- Matplotlib

## 8. Limitations

- The reported detector comparison is based on a 100-image evaluation subset.
- Evaluation results may not represent performance across the complete dataset.
- Performance can vary with lighting, image quality, viewing angle, and plate visibility.
- Real-world deployment requires further testing and validation.

## 9. Future Improvements

- Improve SSD300 detection performance.
- Optimize model inference speed.
- Improve OCR performance under challenging image conditions.
- Evaluate on larger and more diverse datasets.
- Develop a real-time ALPR application.

## 10. Dataset and Usage Notice

The UFPR-ALPR dataset is not included in this repository.

Users must obtain the dataset directly from its official source and comply with its license agreement.

Dataset:
https://web.inf.ufpr.br/vri/databases/ufpr-alpr/

License:
https://web.inf.ufpr.br/vri/databases/ufpr-alpr/license-agreement/
