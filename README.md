# Explainable AI-Guided Informative MRI Slice Selection for Autism Spectrum Disorder Classification Using Deep Learning

## Overview

This project presents an Explainable AI (XAI)-guided approach for selecting informative MRI slices for Autism Spectrum Disorder (ASD) classification.

Instead of using all slices from a structural MRI volume, the proposed approach uses a deep learning model to evaluate individual 2D MRI slices and Integrated Gradients (IG) to identify the regions that contribute to the model's predictions. The most informative slices are then selected and aggregated for subject-level ASD/Control classification.

## Methodology

The overall workflow is:

**3D MRI Volume → 2D MRI Slices → SqueezeNet Classification → Integrated Gradients → Slice Importance Ranking → Informative Slice Selection → Subject-Level Classification**

The main components of the project are:

* **Dataset:** ABIDE structural MRI data
* **Deep Learning Model:** SqueezeNet
* **Explainability Method:** Integrated Gradients
* **Slice Selection:** XAI-based ranking and Top-K selection
* **Final Classification:** Subject-level aggregation of selected slice predictions

## Dataset

The experiments use structural MRI data from the **Autism Brain Imaging Data Exchange (ABIDE)** dataset.

The raw MRI dataset is not included in this repository due to its size and data-distribution considerations.

The reported validation experiments use **1,054 MRI slices from 6 subjects**:

* 3 ASD subjects
* 3 Control subjects

Therefore, the reported subject-level accuracy results should be interpreted as validation results on this small subject-level sample.

## Experiments

Several experiments were conducted to evaluate different deep learning models and XAI-based slice selection strategies.

| Experiment              | Approach                                 | Validation Accuracy |
| ----------------------- | ---------------------------------------- | ------------------: |
| EfficientNet Baseline   | All-slice classification                 |              16.67% |
| EfficientNet + XAI      | SHAP/Permutation-based selection         |              33.33% |
| ResNet50 Baseline       | All-slice classification                 |              50.00% |
| ResNet50 + XAI          | XAI-based selection                      |              50.00% |
| SqueezeNet Baseline     | All-slice classification                 |              66.67% |
| SqueezeNet + Initial IG | Integrated Gradients-based selection     |              50.00% |
| IG Regional Selection   | Region-based informative slice selection |              66.67% |
| IG Top-K Selection      | Top-K informative slices                 |          **83.33%** |

### Top-K Slice Selection

The final experiments evaluated different numbers of selected slices using Integrated Gradients.

| Top-K | Selected Slices | Subject-Level Accuracy |
| ----: | --------------: | ---------------------: |
|     5 |              30 |             **83.33%** |
|     8 |              48 |                 66.67% |
|    10 |              60 |             **83.33%** |
|    15 |              90 |                 66.67% |
|    20 |             120 |             **83.33%** |

The results indicate that selecting a smaller set of informative MRI slices using XAI can achieve competitive subject-level classification while reducing the number of slices used for final aggregation.

> **Note:** The reported validation results are based on 6 subjects (3 ASD and 3 Control). Since each subject contributes 16.67 percentage points to subject-level accuracy, these results should be interpreted as preliminary validation results rather than large-scale clinical performance.


## Project Structure

```text
ASD-XAI-MRI-Slice-Selection/
│
├── data/
│   └── README.md
│
├── experiments/
│   ├── experiment_02_weight_optimization/
│   ├── experiment_04_resnet50/
│   ├── experiment_05_squeezenet/
│   ├── experiment_06_squeezenet_gradcam_ig/
│   ├── experiment_07_ig_regional_selection/
│   ├── experiment_08_squeezenet_aggregation/
│   └── experiment_09_slice_count_comparison/
│
├── models/
│   └── README.md
│
├── notebooks/
│   ├── 01_XAI_Slice_Selection.ipynb
│   ├── 02_Weight_Optimization.ipynb
│   ├── 03_Weighted_Aggregation.ipynb
│   ├── 04_ResNet50.ipynb
│   ├── 05_SqueezeNet.ipynb
│   ├── 06_SqueezeNet_GradCAM_IG.ipynb
│   ├── 07_IG_Regional_Selection.ipynb
│   ├── 08_SqueezeNet_Aggregation_Comparison.ipynb
│   ├── 09_IG-Guided_Diverse_Slice_Selection.ipynb
│   └── 10_Final_Project_Results_Summary.ipynb
│
├── results/
│   └── CSV result files
│
├── .gitignore
└── README.md
```

## Technologies Used

* Python
* TensorFlow / Keras
* SqueezeNet
* Integrated Gradients
* NiBabel
* OpenCV
* NumPy
* Pandas
* Scikit-learn
* Matplotlib
* Jupyter Notebook

## Reproducibility

The notebooks contain the preprocessing, model evaluation, explainability, slice ranking, selection, and aggregation steps used throughout the experiments.

Raw MRI data and trained model weights are not included in this repository.

## Authors

**Beulah Angeline Yasby J**

Karunya Institute of Technology and Sciences
