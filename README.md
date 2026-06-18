# Mood Detection Project

[![R](https://img.shields.io/badge/R-4.0%2B-blue)](https://www.r-project.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Dataset](https://img.shields.io/badge/Dataset-AMIGOS-orange)](http://www.eecs.qmul.ac.uk/mmv/datasets/amigos/)

> **Multimodal Affective Computing: Statistical Analysis of Emotional Responses in Individual and Group Contexts**

## Overview

This project addresses a critical gap in Affective Computing: the over-reliance on individual emotional experiences while ignoring social dynamics. Using the **AMIGOS dataset**, we conduct rigorous statistical analyses to understand how physiological signals (EEG, ECG, GSR) and emotional dimensions (valence, arousal, dominance) interact in both individual and group settings.

**Key Research Question:** How can we design emotion recognition systems that understand how social context influences and modifies emotional expression and experience?
## Dataset: AMIGOS

The **AMIGOS** (A Dataset for Affect, Personality and Mood Research on Individuals and GrOupS) dataset contains:

| Feature | Description |
|---------|-------------|
| **Observations** | 800 |
| **Participants** | 40 (ranked 1-20) |
| **Videos** | 20 (ranked 1-20) |
| **Video Types** | Short (640 obs) / Long (160 obs) |

### Target Variables (Scale 1-9)
- `valence` — Pleasant/unpleasant character
- `arousal` — Excitement level
- `dominance` — Feeling of control
- `liking` — Degree of appreciation
- `familiarity` — Familiarity level

### Physiological Signals
- **EEG**: 14 channels (cerebral activity)
- **ECG**: 2 channels (cardiac activity)
- **GSR**: 1 channel (galvanic skin response)

### Emotional Variables (Binary 0/1)
- `anger`, `disgust`, `fear`, `happiness`, `sadness`, `surprise`

## Project Structure
Mood-Detection/
├── data/
│   └──SelfAsessment.xlsx
│   ├── Patras AMIGOS A Dataset 2018.pdf
├── Modélisation/
│   ├── mood_detection_project-final-version.pdf
│   ├── mood_detection_project-final-version.rmd
├── docs/
│   ├── Mood detection Presentation
└── README.md                        # This file


## Methodology

### 1. Data Preparation
- Import and structure validation
- Duplicate detection: **None found**
- Missing values check: **None found**
- Outlier detection via boxplots: **No significant outliers**

### 2. Univariate Analysis
- **Normality Testing**: Shapiro-Wilk tests (all target variables rejected normality, p < 0.05)
- **Distribution Analysis**: Histograms, Q-Q plots, descriptive statistics
- **Encoding**: Categorical variables (video_type: short=0, long=1)
- **Key Finding**: Non-parametric methods required for all inferential analyses

### 3. Bivariate Analysis

| Test | Application | Key Results |
|------|-------------|-------------|
| **Chi-Square** | Qualitative vs Qualitative | No significant associations between emotions and video type |
| **Spearman Correlation** | Quantitative vs Quantitative | Weak overall correlations (-0.10 to +0.10) |
| **Mann-Whitney U** | Quantitative vs Binary Qualitative | Significant differences in EEG signals across emotions |

### 4. Multiple Linear Regression
**Models built for each target variable:**
- **Predictors**: EEG_1-14, ECG_1-2, GSR_1, emotional binaries, video_type
- **Results**: Very low explanatory power (R² adjusted near 0)
- **Significant predictors**: EEG_1 (valence), EEG_7 (arousal), anger (dominance), video_type (liking/familiarity)

### 5. Logistic Regression
- **Target**: Binary happiness classification
- **AUC**: 0.5587 (limited discriminative power)
- **Multicollinearity**: VIF values acceptable (< 1.02)

## Key Findings

1. **Data Quality**: Clean dataset with no missing values or duplicates
2. **Normality**: All continuous variables significantly deviate from normality
3. **Correlations**: Emotional dimensions are largely independent (weak correlations)
4. **Predictive Power**: Linear models show very low R², suggesting complex non-linear relationships
5. **Social Context**: Video type (short vs long) shows limited but significant effects on liking and familiarity

## Technologies Used

- **R** (primary language)
- Packages: `dplyr`, `ggplot2`, `corrplot`, `Hmisc`, `car`, `pROC`, `gridExtra`, `knitr`

## Results Summary
| Model    | Target      | R² Adjusted | Significant Predictors | Quality    |
| -------- | ----------- | ----------- | ---------------------- | ---------- |
| Linear   | Valence     | -0.011      | EEG\_1                 | Null       |
| Linear   | Arousal     | 0.000       | EEG\_7                 | Weak       |
| Linear   | Dominance   | -0.012      | Anger                  | Null       |
| Linear   | Liking      | 0.001       | EEG\_11, video\_type   | Weak       |
| Linear   | Familiarity | -0.009      | Video\_type            | Null       |
| Logistic | Happiness   | —           | —                      | AUC: 0.559 |

## Citation
If you use this work, please cite:
@project{mood_detection_2025,
  title={Projet de Détection d'Humeur: Analyse Statistique Multimodale},
  author={Abdelkefi, Hajer and Aloui, Oussema and Ben Abdallah, Ameni and 
          Ben Achour, Firas and Chtourou, Oumaima and Messaoudia, Sarra},
  year={2025},
  institution={University Project}
}

## Acknowledgments
AMIGOS Dataset: Queen Mary University of London
Inspiration: DEAP, MAHNOB-HCI datasets for affective computing research
