# CSE 144 Final Project

## Team Members

* Tianai Shang
* Esther Cui

## About This Project

This is our final project for CSE 144 Applied Machine Learning.

For this project, we worked on the Kaggle image classification challenge provided by the class. The dataset has 100 classes, with only about 10 training images for each class. Because the dataset is small, we used transfer learning instead of training a model from scratch.

Our final model uses EfficientNet-B3 with pretrained ImageNet weights. We fine-tuned the model on the given training images and used it to predict labels for the test images.

## Files in This Repository

```text
.
├── CSE144FinalProject.ipynb
├── CSE144_Report_Final.pdf
└── README.md
```

## Model Weights

The trained model weight file is too large to upload directly to GitHub, so we uploaded it to Google Drive.

Model weights link:

```text
https://drive.google.com/file/d/19sFCznpR9kceL_UEgxkTZOjkF3RlydR6/view?usp=drive_link
```

## Dataset

The dataset comes from the Kaggle competition page:

```text
https://www.kaggle.com/competitions/ucsc-cse-144-spring-2026-final-project
```

The training data is organized into 100 class folders, labeled from `0` to `99`. The test folder contains 1000 unlabeled images.

The goal is to predict one label from `0` to `99` for each test image.

## Model

We used a pretrained EfficientNet-B3 model from TorchVision.

Basic setup:

```text
Model: EfficientNet-B3
Pretrained weights: ImageNet
Number of classes: 100
Image size: 224 x 224
Optimizer: AdamW
Loss: Cross Entropy Loss
Scheduler: Cosine Annealing LR
```

We resized the images to the same size and used data augmentation during training to help reduce overfitting.

## Hyperparameters

```python
IMAGE_SIZE = 224
BATCH_SIZE = 32
NUM_EPOCHS = 30
LR_HEAD = 1e-3
LR_BACKBONE = 1e-4
WEIGHT_DECAY = 1e-4
NUM_CLASSES = 100
VAL_SPLIT = 0.15
SEED = 42
```

## How to Run the Code

This project was run in Google Colab.

### 1. Open the notebook

Open this file in Google Colab:

```text
CSE144FinalProject.ipynb
```

### 2. Mount Google Drive

Run:

```python
from google.colab import drive
drive.mount('/content/drive')
```

### 3. Prepare the dataset

Put the Kaggle zip file in Google Drive. In our notebook, the dataset path is:

```text
/content/drive/MyDrive/ucsc-cse-144-spring-2026-final-project.zip
```

Then unzip it:

```python
!mkdir -p /content/cse144_data
!unzip -q "/content/drive/MyDrive/ucsc-cse-144-spring-2026-final-project.zip" -d /content/cse144_data
```

After unzipping, the notebook uses:

```python
BASE_DIR = "/content/cse144_data"
TRAIN_DIR = "/content/cse144_data/train"
TEST_DIR = "/content/cse144_data/test"
```

### 4. Train the model

Run the training cells in the notebook.

The best model is saved as:

```text
/content/best_model.pth
```

### 5. Make predictions

After training, run the prediction section in the notebook.

It will generate:

```text
/content/submission_fixed.csv
```

This is the file we uploaded to Kaggle.

## Label Mapping

One important part of this project is keeping the label order correct.

The folders are named from `0` to `99`, and Kaggle expects the labels to match those numbers. For example:

```text
folder "0"  -> label 0
folder "1"  -> label 1
folder "99" -> label 99
```

If the label order is wrong, the Kaggle score can become very low even if the model is learning. In the notebook, we fixed the label mapping before creating the final submission file.

## Result

Our final Kaggle public score was:

```text
0.74545
```

This is above the required baseline score of `0.60`.

Kaggle leaderboard screenshot:

<img width="888" height="606" alt="Kaggle leaderboard screenshot" src="https://github.com/user-attachments/assets/4b9ade3a-fc92-4e7c-b66f-af1c2299a398" />

## Report

The final report is included in this repository:

```text
CSE144_Report_Final.pdf
```
