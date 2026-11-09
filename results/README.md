# Model Evaluation Results

This directory contains the evaluation results of the Vehicle Number Plate Detection and Recognition project.

## 1. Detector Comparison

File: `model_comparison.csv`

Compares three object detection models:

- YOLOv8
- Faster R-CNN
- SSD300

The evaluation uses a 100-image subset containing 100 ground-truth plate boxes.

Metrics include:

- True Positives
- False Positives
- False Negatives
- Precision
- Recall
- F1-score
- AP@0.50
- mAP@0.50:0.95
- Mean Matched IoU
- Mean Inference Time
- End-to-End Exact Plate Match
- End-to-End Mean Character Accuracy

## 2. PARSeq OCR Evaluation

File: `parseq_ocr_results.csv`

PARSeq was evaluated separately using ground-truth plate crops.

Results:

- Exact Plate Matches: 1,377 / 1,800
- Exact Plate Match: 76.50%
- Character Accuracy: 93.16%

These OCR-only results must not be confused with end-to-end detection and recognition results.

## 3. Observations

- YOLOv8 provides a strong balance of detection performance and inference speed.
- Faster R-CNN achieves the highest recall and AP metrics but has higher inference time.
- SSD300 requires further improvement in detection performance.

## Evaluation Scope

The detector comparison represents a 100-image evaluation subset, not the complete UFPR-ALPR dataset. Results should be interpreted within this evaluation scope.

The UFPR-ALPR dataset is not included in this repository.
