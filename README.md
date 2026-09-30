# Spam Mail Detector

## Objective

Build a machine learning classifier that identifies whether an email is spam or ham (non-spam) using email text.

## Dataset

The project uses `emails.csv`, a labeled email dataset with two columns:

- `text`: email content
- `spam`: target label where `0` means ham and `1` means spam

The dataset contains 5,728 emails. After removing 33 duplicate messages, 5,695 unique emails remained.

## Project Structure

```text
spam-mail-detector/
├── data/
│   └── emails.csv
├── models/
│   └── spam_mail_detector.joblib
├── notebooks/
│   ├── spam_mail_detector.ipynb
│   └── saved_model_testing.ipynb
├── .venv/
├── requirements.txt
└── README.md
```

## Setup

Create and activate a virtual environment:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install the required packages:

```powershell
python -m pip install -r requirements.txt
```

Download NLTK resources:

```powershell
python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt'); nltk.download('punkt_tab')"
```

Start JupyterLab:

```powershell
jupyter lab
```

Select the `Python (Spam Mail Detector)` kernel in both notebooks.

## Workflow

1. Load the labeled email dataset.
2. Inspect data types, missing values, duplicate messages, and class distribution.
3. Remove duplicate emails.
4. Preprocess email text:
   - convert to lowercase
   - remove punctuation and symbols
   - tokenize text into words
   - remove English stopwords
5. Split the data into training and testing sets using an 80/20 stratified split.
6. Convert cleaned text into 5,000 TF-IDF features.
7. Train a Multinomial Naive Bayes classifier.
8. Evaluate the classifier using accuracy, precision, recall, F1 score, and a confusion matrix.
9. Save the trained model and TF-IDF vectorizer using Joblib.
10. Load the saved model in a separate notebook and test new emails.

## Model Results

| Metric | Score |
|---|---:|
| Accuracy | 98.51% |
| Spam precision | 98.49% |
| Spam recall | 95.26% |
| Spam F1 score | 96.85% |

The classifier correctly predicted 1,122 of 1,139 test emails.

## Confusion Matrix Results

| Actual label | Predicted ham | Predicted spam |
|---|---:|---:|
| Ham | 861 | 4 |
| Spam | 13 | 261 |

The model produced 4 false positives and 13 false negatives.

## Saved Model

The trained Naive Bayes model and fitted TF-IDF vectorizer are saved together in:

```text
models/spam_mail_detector.joblib
```

The `saved_model_testing.ipynb` notebook loads this file and predicts spam or ham for new email text without retraining the model.

## Future Improvements

- Compare Multinomial Naive Bayes with Logistic Regression.
- Experiment with TF-IDF settings such as n-grams and number of features.
- Train with a larger and more diverse email dataset.
- Build a web interface for user-entered email text.