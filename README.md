# Automated Malaria Cell Detection

**Deep Learning · Computer Vision · Transfer Learning · Explainable AI**

An image-classification project exploring how deep learning can distinguish parasitized from uninfected red blood cell images, using EfficientNetB0 transfer learning and Grad-CAM for visual interpretability.

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-Deep%20Learning-orange?logo=tensorflow)](https://www.tensorflow.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)

---

## Overview

Malaria diagnosis commonly involves examining blood smear samples under a microscope to identify parasites in red blood cells. This project explores a computer-vision approach to classifying microscopic cell images into two categories:

- **Parasitized** — images labelled as containing malaria parasites.
- **Uninfected** — images labelled as uninfected.

The project uses transfer learning with EfficientNetB0 to investigate image classification, model evaluation and visual explanation techniques.

Beyond classification, the goal is to understand how a deep-learning pipeline is developed, evaluated and prepared for potential lightweight deployment.

## Objectives

- Develop a binary image-classification pipeline using TensorFlow and Keras.
- Explore transfer learning with a pretrained EfficientNetB0 backbone.
- Apply image preprocessing and data augmentation.
- Evaluate predictions using classification metrics and visualizations.
- Use Grad-CAM to investigate image regions influencing model predictions.
- Explore TensorFlow Lite as a route toward lightweight inference.

## Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| TensorFlow / Keras | Model development and training |
| EfficientNetB0 | Transfer-learning backbone |
| NumPy | Numerical operations |
| Matplotlib | Training curves and evaluation plots |
| Scikit-learn | Classification metrics and evaluation utilities |
| Jupyter Notebook | Experimentation and documentation |
| Grad-CAM | Visual interpretation of model predictions |
| TensorFlow Lite | Exploration of lightweight model inference |

The table describes the intended project stack; individual dependencies and deployment components should be verified against the current notebook before running the complete workflow.

## Dataset

The project is being developed around the [NIH/NLM Malaria Cell Images Dataset](https://lhncbc.nlm.nih.gov/publication/pub9932), which contains labelled microscopic cell images for parasitized and uninfected classes.

**Dataset source:** National Library of Medicine (NLM), National Institutes of Health (NIH).

The dataset must be obtained and extracted separately before running the real-data pipeline. The dataset itself is not included in this repository.

### Data preparation

The intended data pipeline includes:

1. Loading images and their labels.
2. Checking class distributions and image dimensions.
3. Creating reproducible training, validation and test splits.
4. Applying augmentation to training images only.
5. Preparing images for the selected model's input requirements.

To avoid overly optimistic evaluation, the final experiment should use a held-out test set that is not used for model selection. Patient-level separation should be used where reliable patient identifiers are available.

## Model Architecture

### EfficientNetB0 and Transfer Learning

EfficientNetB0 is used as the starting point for transfer learning. A pretrained convolutional neural network can provide useful visual features, reducing the need to learn every image feature from scratch.

The planned training workflow is:

1. Load and preprocess labelled cell images.
2. Initialize EfficientNetB0 with pretrained weights.
3. Attach a classification head for the two target classes.
4. Train the classification head.
5. Fine-tune selected backbone layers where appropriate.
6. Evaluate the selected model on held-out data.

The effectiveness of transfer learning and fine-tuning must be established through experiments rather than assumed from the architecture alone.

## Explainable AI with Grad-CAM

Grad-CAM (Gradient-weighted Class Activation Mapping) is used to visualize image regions that contribute to a model's prediction.

These heatmaps can help investigate whether the classifier focuses on plausible cellular structures or relies on irrelevant visual patterns.

Grad-CAM is an interpretability aid, not proof that a prediction is medically correct. Heatmaps should be examined alongside correct predictions, false positives and false negatives.

## Evaluation

Model evaluation should go beyond accuracy, particularly when the application involves identifying potentially infected cells.

The evaluation report will include:

- **Accuracy:** Overall proportion of correct predictions.
- **Precision:** Proportion of predicted parasitized cells that are labelled parasitized.
- **Recall:** Proportion of labelled parasitized cells correctly identified.
- **F1-score:** Harmonic mean of precision and recall.
- **Confusion matrix:** Breakdown of correct and incorrect predictions.
- **ROC-AUC:** Ability to distinguish between classes across classification thresholds, where applicable.

Training and validation curves will also be used to investigate overfitting and training stability.

> **Results status:** Previously saved notebook runs reported approximately 95–96% validation accuracy. Those results must not be interpreted as validated performance on the real NIH/NLM dataset unless they are reproduced using the real images and a correctly separated evaluation set. Final metrics will be documented here after that experiment is completed.

## Repository Structure

```text
Automated-malaria-detection/
├── Malaria_Cell_Classification.ipynb
├── README.md
└── ...
```

The notebook contains the main experiment, including code cells, outputs and visualizations. Additional scripts, model files and application components may be added as the project develops.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/swastikkaa/Automated-malaria-detection.git
cd Automated-malaria-detection
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

Install Jupyter and the libraries required by the notebook:

```bash
python -m pip install --upgrade pip
python -m pip install jupyter notebook tensorflow numpy pandas matplotlib scikit-learn pillow
```

The exact TensorFlow version should be selected based on compatibility with your Python version and hardware.

### 4. Obtain the dataset

Download the dataset from the official [NIH/NLM source](https://lhncbc.nlm.nih.gov/publication/pub9932) and extract it locally.

Update the dataset path in the notebook to match your local directory. Do not commit the full dataset to this repository.

### 5. Launch Jupyter

```bash
jupyter notebook
```

Open `Malaria_Cell_Classification.ipynb` and follow the notebook sections in order.

**Note:** Training time depends on hardware, dataset size, preprocessing and model configuration. A GPU may substantially accelerate training, but CPU execution is possible with appropriately sized experiments.

## Reproducibility

For meaningful comparisons between experiments:

- Fix random seeds where supported.
- Save the training, validation and test assignments.
- Keep test data separate from model selection.
- Record the model configuration and dependency versions.
- Report metrics from the same held-out test set when comparing models.
- Document any changes to preprocessing, augmentation or classification thresholds.

## Limitations

- Performance depends on the quality, representativeness and labelling of the dataset.
- Image-level evaluation may overestimate generalization if related samples appear in multiple splits.
- Grad-CAM visualizations do not establish causal reasoning or clinical correctness.
- A model evaluated on one dataset may not generalize to different laboratories, microscopes or staining conditions.
- Results from a validation set do not establish real-world diagnostic performance.

**This is an educational machine-learning project, not a clinically validated diagnostic system. Predictions must not be used as a substitute for professional medical assessment.**

## Future Improvements

- Establish a reproducible baseline using real microscopy images.
- Compare a simple CNN with frozen and fine-tuned EfficientNetB0.
- Investigate false positives, false negatives and potential data leakage.
- Evaluate Grad-CAM outputs on correctly and incorrectly classified images.
- Measure inference latency and model size.
- Validate TensorFlow Lite conversion.
- Develop and test an interactive image-classification interface.

## References

1. National Library of Medicine, NIH — [Malaria Cell Images Dataset](https://lhncbc.nlm.nih.gov/publication/pub9932).
2. Tan, M. and Le, Q. V. — [EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks](https://arxiv.org/abs/1905.11946).
3. Selvaraju, R. R. et al. — [Grad-CAM: Visual Explanations from Deep Networks via Gradient-Based Localization](https://arxiv.org/abs/1610.02391).
4. TensorFlow — [Official documentation](https://www.tensorflow.org/).

---

**Author:** [Swastika Man Singh](https://github.com/swastikkaa)

