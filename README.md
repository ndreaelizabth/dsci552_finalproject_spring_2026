# DSCI 552 Final Project: Transfer Learning for Fungi Image Classification

## Project Overview

This project builds a transfer learning image classifier for five types of fungi. The goal is to compare multiple pretrained convolutional neural network architectures and evaluate their performance on a five-class fungi image classification task.

The project uses the following pretrained models:

- VGG16
- ResNet50
- ResNet101
- EfficientNetB0
- DenseNet201

Note: ResNet101 was used as the substitute for ResNet100 because ResNet100 is not available in Keras, and this substitution was approved in the course Q&A.

## Repository Structure

```text
dsci552_finalproject_spring_2026/
├── README.md
├── requirements.txt
├── Final Project.pdf
├── notebook/
│   ├── Andrea_FernandezCruz_Final_Project.ipynb
│   ├── saved_models/
│   │   ├── VGG16_best.keras
│   │   ├── ResNet50_best.keras
│   │   ├── ResNet101_best.keras
│   │   ├── EfficientNetB0_best.keras
│   │   └── DenseNet201_best.keras
│   ├── plots/
│   │   ├── VGG16_loss_curve.png
│   │   ├── ResNet50_loss_curve.png
│   │   ├── ResNet101_loss_curve.png
│   │   ├── EfficientNetB0_loss_curve.png
│   │   └── DenseNet201_loss_curve.png
│   └── results/
│       ├── VGG16_history.pkl
│       ├── ResNet50_history.pkl
│       ├── ResNet101_history.pkl
│       ├── EfficientNetB0_history.pkl
│       ├── DenseNet201_history.pkl
│       └── metrics_summary.csv

