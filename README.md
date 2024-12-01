# IUEXIST: Multilingual Pre-trained Language Models for Sexism Detection on Twitter in EXIST 2023

## Overview
This repository contains the code and resources for our paper: ["IUEXIST: Multilingual Pre-trained Language Models for Sexism Detection on Twitter in EXIST2023"](https://ceur-ws.org/Vol-3497/paper-081.pdf). Our work describes an approach to detect sexism in tweets as part of Task 1 of the ["EXIST 2023 shared task on sexism identification"](https://link.springer.com/chapter/10.1007/978-3-031-28241-6_68) . The dataset includes English and Spanish tweets, and the task involves binary classification to determine whether a given tweet contains sexist expressions or behaviors.

## Abstract
We explored various machine learning algorithms, including:
- Multinomial Naive Bayes
- Support Vector Machines (SVM)
- XGBoost
- Transformers such as DistilBERT, RoBERTa, XLM-RoBERTa, and TwHIN

The best performance was achieved using an ensemble of transformers (XLM-RoBERTa small/large and TwHIN-BERT base/large), combined with XGBoost for final classification. Additional training data from previous EXIST shared tasks (2021 and 2022) was incorporated to improve model performance.

## Methodology
### Dataset
The dataset includes:
- 3,660 Spanish tweets
- 3,260 English tweets

Additional training data from EXIST 2021 and 2022 resulted in 8,960 tweets total (5,593 sexist, 3,367 non-sexist).

### Pre-processing Steps
1. Replace URLs with 'URL'.
2. Remove retweets ('RT').
3. Replace usernames with 'USER'.
4. Convert emojis to text equivalents using the `emoji` Python library.
5. Remove non-alphanumeric characters except apostrophes and spaces.

### Classifiers and Models
- **Traditional Models**: Multinomial Naive Bayes, SVM, XGBoost (with hyperparameter tuning via GridSearchCV).
- **Transformer Models**: Fine-tuned using HuggingFace:
  - DistilBERT
  - RoBERTa (base)
  - XLM-RoBERTa (base and large)
  - TwHIN (base and large)

### Ensemble Model
The ensemble combines:
- XLM-RoBERTa (base and large)
- TwHIN-BERT (base and large)
- XGBoost for ensemble aggregation

### Evaluation Metrics
The primary evaluation metric was **Information Contrast Measure (ICM)**. Additional metrics included macro-averaged F1 scores.

## Results
### Official Task Results
The two submitted models were:
1. **IUEXIST_1**: XLM-RoBERTa Large trained on the official dataset.
2. **IUEXIST_2**: Ensemble model (transformers + XGBoost) trained on the extended dataset.

| Model      | Rank | ICM (Hard-Hard) | Macro F1 (Hard-Hard) |
|------------|------|-----------------|-----------------------|
| IUEXIST_1  | 16   | 0.5313          | 0.7734                |
| IUEXIST_2  | 15   | 0.5341          | 0.7717                |

### Development Set Results
| Classifier          | ICM (Hard-Hard) | Macro F1 |
|---------------------|-----------------|----------|
| Naive Bayes         | 0.1354          | 0.6729   |
| SVM                 | 0.2738          | 0.7180   |
| XGBoost             | 0.3220          | 0.7332   |
| DistilBERT          | 0.3822          | 0.7522   |
| XLM-RoBERTa (base)  | 0.5716          | 0.8120   |
| Ensemble            | 0.5873          | 0.8171   |

## Challenges
- **Sexism Definition**: Some dataset examples were ambiguous, requiring careful interpretation.
- **Large Information Space**: Directing attention to relevant problem-solving resources proved challenging.

## Future Work
- Investigate the impact of additional training data on model performance.
- Explore long-term evaluations to assess the impact of temporal differences between training and test data.

## Citation
If you use our work, please cite:
```
@inproceedings{abdo2023iuexist,
  title={IUEXIST: Multilingual Pre-trained Language Models for Sexism Detection on Twitter in EXIST 2023},
  author={Muhammed S. Abdo et al.},
  booktitle={CEUR Workshop Proceedings},
  year={2023},
  url={https://ceur-ws.org/Vol-3497/paper-081.pdf}
}
```
