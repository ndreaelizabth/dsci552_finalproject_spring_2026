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
│   ├── Colab_Training_VGG16_ResNet50.ipynb
│   ├── Kaggle_Training_ResNet101_EfficientNetB0_DenseNet201.ipynb
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
```

## Notebook Files

The main final project notebook is:
```text
notebook/Andrea_FernandezCruz_Final_Project.ipynb
```

This notebook presents the full final project workflow, including dataset organization, preprocessing, augmentation, transfer learning model setup, saved training plots, evaluation metrics, and final model comparison.

Because local CPU training was too slow, model training was completed across GPU notebook environments:

- Colab_Training_VGG16_ResNet50.ipynb contains the Google Colab training workflow for VGG16 and ResNet50.
- Kaggle_Training_ResNet101_EfficientNetB0_DenseNet201.ipynb contains the Kaggle GPU training workflow for ResNet101, EfficientNetB0, and DenseNet201.
- The Kaggle notebook was also used to generate the final metrics summary table.

The main final notebook loads the saved .keras checkpoints, plots, history files, and metrics_summary.csv so the project can be reviewed without requiring all models to be retrained from scratch.

## Dataset

The raw dataset image folders are not included in this repository due to size. The dataset contains 9,114 images across five fungi classes.

The original image filenames use prefix labels. These were mapped into five class folders as follows:

| Filename Prefix | Class Folder |
|---|---|
| H1 | C1 |
| H2 | C2 |
| H3 | C3 |
| H5 | C4 |
| H6 | C5 |

The class counts are:

| Class | Number of Images |
|---|---:|
| C1 | 4,404 |
| C2 | 2,334 |
| C3 | 819 |
| C4 | 818 |
| C5 | 739 |

The dataset was randomly split within each class using the required split:

| Split | Percentage |
|---|---:|
| Training | 75% |
| Validation | 15% |
| Test | 10% |

## Runtime Note

Training was completed using **Google Colab and Kaggle GPU environments** because local CPU training in VS Code was too slow for five transfer learning models.

The full training code is included in the submitted notebooks. Because full training is time-intensive, the main final notebook loads the saved .keras checkpoints, training histories, plots, and metrics for reproducible evaluation without requiring retraining during grading.

## Methodology

Each pretrained model was loaded with ImageNet weights and used as a frozen feature extractor. The pretrained base model layers were frozen, and a new classification head was added for the five fungi classes.

The classification head includes:

- Dense layer with ReLU activation
- L2 regularization
- Batch normalization
- Dropout with rate 0.20
- Final softmax output layer for five-class classification

The models were compiled using:

- Adam optimizer
- Categorical cross entropy loss
- Accuracy as the training metric

## Image Preprocessing and Augmentation

All images were resized to 224 x 224 pixels.

The training set used image augmentation, including:

- Random crop
- Random zoom
- Random rotation
- Random horizontal flip
- Random contrast
- Random translation

Augmentation was applied only during training, not during validation or testing.

## Training Procedure

Each model was trained for at least 50 epochs. Early stopping was introduced only after the required 50 epochs, following the course clarification.

The best model checkpoint was saved based on the lowest validation loss.

Saved model files are located in:
text
notebook/saved_models/
```
Training/validation loss plots are located in:
```text
notebook/plots/
```
Training history files and metrics outputs are located in:
```text
notebook/results/
```

## Evaluation

Each trained model was evaluated on the training, validation, and test sets.

The reported metrics are:

- Precision
- Recall
- F1 Score
- AUC

Because this is a multi-class classification problem, weighted averaging was used for Precision, Recall, F1, and AUC.

The final metrics table is saved as:
```text
notebook/results/metrics_summary.csv
```

## Final Model Comparison

Based on the test set results, **ResNet101** was the strongest overall model.

ResNet101 achieved the highest test F1 score and highest test AUC while maintaining strong precision and recall. Although ResNet50 had slightly higher test precision, ResNet101 performed better overall because F1 score balances precision and recall, and AUC reflects stronger multi-class discrimination.

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/ndreaelizabth/dsci552_finalproject_spring_2026.git
cd dsci552_finalproject_spring_2026
```
### 2. Install dependencies
```bash
pip install -r requirements.txt
```
### 3. Get Git LFS files

The trained .keras model checkpoints are tracked using Git LFS.
```bash
git lfs install
git lfs pull
```
### 4. Open the main notebook

Open:
```text
notebook/Andrea_FernandezCruz_Final_Project.ipynb
```
The notebook includes the final project workflow and loads saved trained models/results for evaluation and comparison.

## Reproducing Training From Scratch

To rerun training from scratch, place the DeFungi dataset locally and follow the dataset organization steps in the notebook.

Expected local dataset structure after organization:
```text
data/
├── C1/
├── C2/
├── C3/
├── C4/
└── C5/
```
The notebook then creates the train/validation/test split:
```text
data/split/
├── train/
├── val/
└── test/
```
To reproduce the original training runs, use the supporting GPU notebooks:
```text
notebook/Colab_Training_VGG16_ResNet50.ipynb
notebook/Kaggle_Training_ResNet101_EfficientNetB0_DenseNet201.ipynb
```
## Notes

- ResNet101 was used as the approved substitute for ResNet100.
- The raw dataset image folders and zip files are excluded from GitHub due to size.
- The trained .keras files are included through Git LFS.
- The main notebook can load saved models and results so graders do not need to retrain all models from scratch.
- Full training code remains included in the submitted notebooks for transparency and reproducibility.

## AI Disclosure

I used ChatGPT as a learning assistant for this project. It helped me understand the assignment requirements, organize the notebook, debug environment issues, structure the training workflow, and prepare documentation.

I reviewed, tested, and worked through the code to the best of my ability.