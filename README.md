# INNOCENT ZERO — Spam Message Detection System

## Project Overview

**INNOCENT ZERO** is an interactive spam message detection system that classifies text as **Spam** or **Ham (Legitimate)**. It combines a web dashboard with a Flask API and a machine-learning model built using TF-IDF text features and logistic regression.

## Objectives

- Classify messages as spam or legitimate.
- Use word and character patterns to analyze message text.
- Adjust the spam decision threshold using a sensitivity control.
- Display risk indicators for urgency, financial language, suspicious links, and unusual formatting.
- Provide an interactive interface for testing messages.

## Technologies Used

- **Frontend:** HTML, CSS, JavaScript
- **Frontend development server:** Vite
- **Backend API:** Python, Flask, Flask-CORS
- **Machine Learning:** Scikit-learn
- **Text features:** TF-IDF word and character n-grams
- **Data processing:** Pandas
- **Model storage:** Joblib

## Key Features

- Interactive dashboard for scanning messages.
- Spam probability and classification results.
- Adjustable threat-sensitivity threshold.
- Rule-based heuristic analysis when the model API is unavailable.
- Risk indicators for urgency, money-related language, links, and unusual formatting.
- Temporary quarantine list for messages classified as spam.
- Animated traffic visualization and optional audio effects.
- Scripts to train and evaluate the machine-learning model.

> **Note:** The traffic visualization is a demo and does not monitor live network traffic. Dashboard statistics such as engine accuracy, load, and latency are simulated. The spam probability for each scanned message comes from the trained model when the API is available.

## Model

The classifier uses a scikit-learn pipeline with:

- Word-level TF-IDF features using n-grams from 1 to 3 words.
- Character-level TF-IDF features using character n-grams from 2 to 5 characters.
- Logistic regression with balanced class weights.

The model is trained using `dataset/spam.csv`. The included pre-trained model is stored in `models/spam_model.joblib`.

## Model Performance

The saved model metadata reports the following results on a held-out test split of 1,115 messages, using a spam threshold of `0.35`:

| Metric | Result |
|---|---:|
| Accuracy | 99.28% |
| Spam Precision | 98.62% |
| Spam Recall | 95.97% |
| Spam F1-score | 97.28% |

These results are for the included dataset and evaluation split; they do not guarantee performance on new messages.

## Project Structure

```text
.
├── app.js
├── index.html
├── style.css
├── vite.config.js
├── predict_server.py
├── train_spam_model.py
├── requirements.txt
├── package.json
├── dataset/
│   └── spam.csv
└── models/
    ├── spam_model.joblib
    └── spam_model_metadata.json
```

## Installation and Execution

### 1. Install frontend dependencies

```bash
npm install
```

### 2. Create a Python virtual environment and install dependencies

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

**macOS / Linux:**

```bash
python3 -m venv .venv
./.venv/bin/python -m pip install -r requirements.txt
```

### 3. Start the Flask API

Run this command from the project root.

**Windows (PowerShell):**

```powershell
.\.venv\Scripts\python.exe predict_server.py
```

**macOS / Linux:**

```bash
./.venv/bin/python predict_server.py
```

The API runs at `http://127.0.0.1:5001`.

### 4. Start the frontend

Open a second terminal in the project root and run:

```bash
npm run dev
```

Open the URL printed by Vite. By default, the frontend is available at `http://localhost:3000`. Vite proxies API requests to the Flask server.

## Train the Model

A pre-trained model is included, so training is not required to run the application. To train a new model using the included dataset:

**Windows (PowerShell):**

```powershell
.\.venv\Scripts\python.exe train_spam_model.py
```

**macOS / Linux:**

```bash
./.venv/bin/python train_spam_model.py
```

The script evaluates the model on a held-out split, trains a final model using the full dataset, and saves the model and evaluation metadata in the `models/` directory.

## Build the Frontend

```bash
npm run build
```

The production frontend files are generated in the `dist/` directory.

## Future Enhancements

- Evaluate the classifier on additional SMS and scam-message datasets.
- Add more detailed explanations for individual predictions.
- Improve phishing-link and fraudulent-message detection.
- Add persistent storage for quarantined messages.
- Deploy the frontend and prediction API for public access.
