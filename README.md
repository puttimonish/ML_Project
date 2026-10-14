# 🛡️ PhishingLens — AI-Powered Phishing URL Detection

**An intelligent web-based security tool that analyzes URLs, estimates phishing probability, and provides contextual risk assessments to help users identify potentially malicious links.**

![Python](https://img.shields.io/badge/Python-3.14-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Random%20Forest-green)
![Backend](https://img.shields.io/badge/Backend-FastAPI-009688)
![Frontend](https://img.shields.io/badge/Frontend-HTML%20%7C%20CSS%20%7C%20JavaScript-orange)
![Status](https://img.shields.io/badge/Status-Academic%20Project-blue)

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Problem Statement](#-problem-statement)
3. [Project Objectives](#-project-objectives)
4. [Key Features](#-key-features)
5. [System Architecture](#-system-architecture)
6. [Machine Learning Methodology](#-machine-learning-methodology)
7. [Technology Stack](#-technology-stack)
8. [Project Structure](#-project-structure)
9. [Installation and Setup](#-installation-and-setup)
10. [Running the Application](#-running-the-application)
11. [Using PhishingLens](#-using-phishinglens)
12. [API Documentation](#-api-documentation)
13. [Dataset and Preprocessing](#-dataset-and-preprocessing)
14. [Risk Assessment](#-risk-assessment)
15. [Security and Privacy](#-security-and-privacy)
16. [Limitations](#-limitations)
17. [Future Enhancements](#-future-enhancements)
18. [Troubleshooting](#-troubleshooting)
19. [Contributing](#-contributing)
20. [License](#-license)

---

## 📖 Project Overview

PhishingLens is a machine-learning-based phishing URL detection project designed to help users evaluate suspicious links before interacting with them.

Phishing attacks commonly use deceptive URLs, misleading subdomains, unusual character combinations, and imitation login pages to trick users into revealing sensitive information.

PhishingLens addresses this problem by extracting numerical and structural characteristics from a submitted URL and processing them through a trained machine-learning classifier.

The application combines a Random Forest classification model with a contextual risk-assessment layer and a web interface that presents the analysis in an understandable format.

The system provides:

- A predicted classification of **LEGITIMATE** or **PHISHING**.
- Estimated phishing and legitimate probabilities.
- An application-level risk score and risk category.
- Explanations and URL characteristics that help users interpret the result.
- Additional security tools for URL comparison, batch scanning, QR-code extraction, and domain intelligence.

The project is intended for educational use, cybersecurity awareness, and experimentation with machine learning. It is not a guarantee that a website is safe.

## 🎯 Problem Statement

Phishing websites imitate trusted services to obtain passwords, financial information, personal details, and other sensitive data.

Traditional approaches, such as manually inspecting URLs or relying exclusively on known malicious-domain lists, have limitations. A newly created phishing domain may not yet appear in a reputation database, while a legitimate URL can contain unusual-looking characters or complex paths.

The problem addressed by PhishingLens is:

**How can machine learning and URL-structure analysis be combined to identify potentially malicious links and communicate their estimated risk to users?**

PhishingLens evaluates URL characteristics without requiring the classifier to open the submitted webpage. Optional intelligence tools can provide additional information when their backend integrations are available.

## 🎯 Project Objectives

1. Develop a machine-learning system for binary phishing URL classification.
2. Prepare and validate a labeled dataset of legitimate and phishing URLs.
3. Extract meaningful structural and numerical features from URL strings.
4. Train a Random Forest classifier to distinguish phishing URLs from legitimate URLs.
5. Generate probability estimates for both classes.
6. Add a separate risk-assessment layer that considers model output and selected contextual indicators.
7. Build a user-friendly web interface for interactive analysis.
8. Provide explanations, reports, and additional URL-analysis utilities.
9. Expose backend functionality through a REST API.
10. Demonstrate the practical application of machine learning in cybersecurity.

## ✨ Key Features

### 1. AI-Powered URL Scanner

Submit a URL to receive a prediction from the trained machine-learning model.

The scanner returns the predicted class, phishing probability, legitimate probability, risk score, risk level, and supporting analysis.

### 2. Probability Estimates

PhishingLens displays the model's estimated probability for both classes rather than presenting only a binary label.

These values describe the model's output and should not be interpreted as a guarantee of actual website safety.

### 3. Contextual Risk Assessment

A separate assessment layer combines the model output with selected contextual indicators to produce a user-facing risk assessment.

This helps distinguish the raw model prediction from the final application-level assessment.

### 4. URL Feature Analysis

The model uses engineered URL characteristics, including features associated with:

- URL length and hostname length.
- Hostname and subdomain structure.
- Path and query characteristics.
- Character composition and entropy.
- Protocol indicators.
- Suspicious keywords.
- Percent encoding and hexadecimal patterns.
- Port and fragment information.

### 5. Bulk URL Scanner

Analyze multiple URLs in one workflow, review individual results, and export batch-analysis results.

### 6. URL Comparison

Compare two URLs side by side using their model predictions, probability estimates, and risk scores.

This can help illustrate how differences in URL structure relate to the classifier's output.

### 7. Email and File Link Extractor

Extract URLs from supported pasted text or files before sending the extracted links to the scanner.

This is a link-extraction utility; it does not independently prove that an email or file is malicious.

### 8. QR URL Extractor

Upload an image containing a QR code to extract its encoded content.

When the backend QR endpoint and its dependencies are available, the extracted URL can be passed to the scanner for further analysis.

### 9. Domain Intelligence

The optional domain-intelligence endpoint can retrieve available information such as:

- DNS information.
- Domain registration information through RDAP.
- TLS certificate information.
- Redirect information.
- Optional URLhaus threat-intelligence results, when configured.

Availability depends on network access, external services, and the submitted domain.

### 10. Known Breach Lookup

An optional email breach-check endpoint can query a configured breach-data provider.

The integration requires the appropriate provider configuration and API key. Email checks should only be performed with the account holder's consent.

### 11. Scan History and Domain Watchlist

Review locally saved scan history and maintain a watchlist of domains in the browser.

Browser-local features depend on the browser's local storage and do not automatically synchronize between devices.

### 12. Reports and Exports

Export supported analysis results in formats such as JSON and text, and use the browser's print functionality to produce a printable report.

### 13. Interactive Web Interface

The frontend provides a dark-themed interface with navigation, analysis tools, results, and supporting information.

### 14. REST API

The FastAPI backend exposes endpoints for URL analysis, health checks, QR decoding, domain intelligence, and optional breach checking.

---

## 🏗️ System Architecture

PhishingLens uses a modular architecture that separates the web interface, API, machine-learning inference, and optional intelligence services.

```text
                     USER
                       |
                       v
               Web Interface
           HTML / CSS / JavaScript
                       |
                       v
                  FastAPI
                 Backend
                       |
          +------------+-------------+
          |                          |
          v                          v
    URL Analysis API          Additional Tools
          |                    |     |     |
          v                    v     v     v
    URL Validation            QR   Domain  Breach
          |                  Decode Intel  Lookup
          v
    Feature Extraction
          |
          v
    Trained Random Forest
          |
          v
    Class Probabilities
          |
          v
    Contextual Risk Assessment
          |
          v
    Results and Explanations
          |
          v
    Web Interface
```

### Main Components

| Component | Responsibility |
|---|---|
| Frontend | Accepts input and displays analysis results. |
| FastAPI backend | Validates requests and exposes API endpoints. |
| Analysis service | Coordinates URL analysis and prediction. |
| Feature extractor | Converts a URL into the features expected by the model. |
| Trained classifier | Estimates the likelihood of each classification. |
| Risk-assessment layer | Produces the application-level risk assessment. |
| Domain-intelligence module | Performs optional external security checks. |
| QR decoder | Extracts content from QR-code images. |
| Browser storage | Supports local history and watchlist features. |

## 🤖 Machine Learning Methodology

PhishingLens uses supervised machine learning to classify URLs into two categories:

- **Legitimate**
- **Phishing**

### 1. Dataset Preparation

A labeled URL dataset is used to provide examples of both classes. Data preparation includes validation, duplicate analysis, and inspection of class distribution.

### 2. Feature Engineering

Raw URL strings are converted into numerical and binary attributes. The trained model works with these extracted characteristics rather than opening the webpage and analyzing its rendered content.

The documented feature design contains 35 engineered URL features covering structural, character-based, and obfuscation-related properties.

The inference pipeline must use the same feature extraction logic and feature ordering expected by the trained model.

### 3. Model Training

A Random Forest classifier is used for supervised classification.

Random Forest combines predictions from multiple decision trees. This can model nonlinear relationships between URL characteristics without requiring every relationship to be explicitly programmed as a rule.

### 4. Prediction

For a submitted URL, the system:

1. Validates the input.
2. Extracts the URL features.
3. Passes the feature vector to the trained classifier.
4. Obtains class predictions and probability estimates.
5. Applies the project's contextual assessment logic.
6. Returns the analysis through the API.

### 5. Model Evaluation

Appropriate evaluation measures for this binary classification task include:

- **Accuracy:** Overall proportion of correct predictions.
- **Precision:** Proportion of predicted phishing URLs that are actually phishing in the evaluation labels.
- **Recall:** Proportion of phishing URLs successfully detected.
- **F1-score:** Harmonic mean of precision and recall.
- **ROC-AUC:** Ability to rank positive and negative examples across classification thresholds.
- **Confusion matrix:** Breakdown of true positives, true negatives, false positives, and false negatives.

Actual evaluation values should be taken from the final training and testing outputs. They should not be inferred from a few demonstration URLs.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Backend and machine-learning implementation. |
| scikit-learn | Machine-learning model and supporting utilities. |
| pandas | Dataset manipulation and analysis. |
| NumPy | Numerical operations. |
| Joblib | Saving and loading the trained model. |
| FastAPI | REST API framework. |
| Uvicorn | ASGI development server. |
| Pydantic | API request and response validation. |
| HTML5 | Webpage structure. |
| CSS3 | Styling and responsive presentation. |
| JavaScript | Frontend interactions and API requests. |
| OpenCV | Optional QR-code decoding. |
| python-multipart | Handling multipart file uploads. |
| RDAP, DNS and TLS utilities | Optional domain-intelligence checks. |
| Git and GitHub | Version control and source-code hosting. |
| Cloudflare Tunnel | Temporary public access to a locally hosted backend, when enabled. |

## 📁 Project Structure

The principal directories and files are organized as follows:

```text
PhishingLens/
│
├── backend/
│   ├── main.py
│   ├── api/
│   │   ├── routes.py
│   │   └── schemas.py
│   ├── services/
│   │   └── analysis_service.py
│   └── ...
│
├── backend_addon/
│   ├── __init__.py
│   ├── domain_intelligence.py
│   ├── qr_backend_fallback.js
│   ├── requirements.txt
│   └── INSTALL.md
│
├── frontend/
│   ├── app.py
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   └── js/
│       ├── app.js
│       └── app_backup.js
│
├── data/
│   ├── external/
│   ├── raw/
│   └── processed/
│
├── models/
│   └── phishinglens_calibrated_v2.joblib
│
├── src/
│   ├── preprocessing/
│   ├── training/
│   ├── prediction/
│   └── analysis/
│
├── tests/
├── docs/
│   ├── index.html
│   ├── css/
│   ├── js/
│   └── .nojekyll
│
├── requirements.txt
├── .gitignore
└── README.md
```

**Note:** This is a guide to the principal project structure. Some directories may contain additional files, and generated files or large model artifacts may be excluded from version control.

## 💻 Installation and Setup

### Prerequisites

Install the following software:

- Python compatible with the project's dependencies.
- Visual Studio Code or another Python development environment.
- Git, if cloning the repository.
- A browser such as Chrome, Edge, or Firefox.

The development environment used for this project is Python 3.14.7. If a dependency is incompatible with that version on your machine, use a Python version supported by the project's pinned dependencies.

### Step 1: Obtain the Project

Download the project ZIP and extract it, or clone the repository:

```bash
git clone https://github.com/puttimonish/ML_Project-PhishingLens.git
cd ML_Project-PhishingLens
```

If you downloaded a ZIP file, open the extracted `PhishingLens` folder instead.

### Step 2: Open the Project

Open the extracted project folder in Visual Studio Code.

Select **Terminal → New Terminal** to open a terminal at the project root.

### Step 3: Create a Virtual Environment

If the project ZIP does not include an existing `.venv` directory, create one:

```powershell
python -m venv .venv
```

Activate it in PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks script execution, use Command Prompt and activate the environment with:

```cmd
.venv\Scripts\activate.bat
```

### Step 4: Install Dependencies

Install the main dependencies:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Install the backend add-on dependencies:

```powershell
python -m pip install -r backend_addon\requirements.txt
```

These commands install the packages declared by the project. Additional setup may be necessary if optional packages, model files, or external-service credentials are not included.

### Step 5: Verify the Trained Model

The backend requires the compatible trained model and its associated feature-extraction implementation.

The expected model path in the current project is:

```text
models/phishinglens_calibrated_v2.joblib
```

The trained model is large and may be excluded from Git because of repository size restrictions. If the file is missing, obtain the correct model artifact from the project owner before running the scanner.

Do not substitute an unrelated model: its expected features and ordering may differ.

## 🚀 Running the Application

From the root of the project, activate the virtual environment and run:

```powershell
.\.venv\Scripts\Activate.ps1
python -m uvicorn backend.main:app --reload
```

Wait until the server reports that startup is complete.

Open the following URL in your browser:

**Website:** http://127.0.0.1:8000

**Interactive API documentation:** http://127.0.0.1:8000/docs

**API root information:** http://127.0.0.1:8000/api

**Health check:** http://127.0.0.1:8000/api/v1/health

Keep the terminal running while you use the application. Press `Ctrl + C` in that terminal to stop the server.

### Important Notes for Team Members

- Each team member runs the backend on their own computer.
- A `.venv` directory created on one computer should not be assumed to work on another computer.
- The model artifact must be present locally.
- The GitHub Pages frontend is a static deployment and does not itself host the Python model.
- Optional integrations may require internet connectivity or additional configuration.

## 🧭 Using PhishingLens

### Analyze a URL

1. Start the backend.
2. Open the website.
3. Enter a URL in the scanner.
4. Select **Analyze URL**.
5. Review the classification, probability estimates, risk assessment, and explanations.

### Scan Multiple URLs

Open the Bulk URL Scanner, provide the supported list of URLs, and run the batch analysis. Review the results and export them when needed.

### Compare URLs

Provide two URLs to compare their classifications, estimated probabilities, and risk scores.

### Extract Links

Use the Email & File Link Extractor to extract URLs from supported text or files. Review the extracted links before scanning them.

### Analyze a QR Code

Upload an image containing a QR code. If decoding succeeds, review the extracted content and use the URL in the scanner when appropriate.

### Inspect Domain Information

Use Domain Intelligence to request supported DNS, registration, TLS, redirect, and optional threat-intelligence information.

### Check Breach Information

Use Known Breach Lookup only when the feature is configured and you have the necessary consent and provider credentials.

### Export Results

Use the Reports & Exports tools to save supported reports or print the current analysis.

## 🔌 API Documentation

PhishingLens exposes its backend through FastAPI.

The interactive API documentation is available at:

`http://127.0.0.1:8000/docs`

### Main Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api` | Returns basic application information. |
| GET | `/api/v1/health` | Reports API health and whether the model is loaded. |
| POST | `/api/v1/analyze` | Analyzes a submitted URL. |
| POST | `/api/v1/intelligence` | Requests domain-intelligence information. |
| POST | `/api/v1/qr-decode` | Decodes a QR-code image upload. |
| POST | `/api/v1/breach-check` | Performs an optional consent-based email breach lookup. |

### Example: URL Analysis

Request:

```http
POST /api/v1/analyze
Content-Type: application/json
```

JSON body:

```json
{
  "url": "https://google.com"
}
```

The response contains fields such as:

```json
{
  "url": "https://google.com",
  "prediction": "LEGITIMATE",
  "model_prediction": "LEGITIMATE",
  "phishing_probability": 6.97,
  "legitimate_probability": 93.03,
  "risk_score": 0,
  "risk_level": "LOW"
}
```

**The values above are an illustrative response from a previous test, not a guaranteed result for every run.** Actual outputs depend on the loaded model, feature extraction, and contextual assessment logic.

The complete response also includes additional assessment fields, explanations, and extracted features.

### Example: Health Check

```http
GET /api/v1/health
```

A successful response resembles:

```json
{
  "status": "healthy",
  "service": "PhishingLens API",
  "model_loaded": true
}
```

## 📊 Dataset and Preprocessing

The project uses a public labeled URL dataset associated with the `URL_Phishing_Detection_Dataset` repository by Hassan-Albattra.

The dataset preparation documented for the project used `balanced_urls.csv`.

| Dataset property | Documented value |
|---|---:|
| Records before duplicate removal | 340,000 |
| Legitimate records before duplicate removal | 170,000 |
| Phishing records before duplicate removal | 170,000 |
| Duplicate rows/URLs identified | 277 |
| Records after duplicate removal | 339,723 |
| Legitimate records after cleaning | 170,000 |
| Phishing records after cleaning | 169,723 |
| Engineered model features | 35 |

The working dataset is approximately balanced between the two classes.

The documented preprocessing workflow includes:

1. Loading the labeled URL data.
2. Checking the required columns and labels.
3. Examining missing values and duplicates.
4. Removing duplicate records.
5. Reviewing the class distribution.
6. Extracting numerical and binary URL features.
7. Preparing the feature matrix and classification labels.
8. Training and evaluating the model using a suitable data-splitting procedure.

These figures describe the documented dataset preparation. The model's final evaluation metrics should be taken from the actual evaluation outputs.

Dataset repository:

https://github.com/Hassan-Albattra/URL_Phishing_Detection_Dataset

## 📈 Risk Assessment

PhishingLens separates the classifier's prediction from the application's risk assessment.

### Model Prediction

The Random Forest classifier estimates the class probabilities and produces a model-level prediction.

### Application-Level Assessment

The contextual layer uses the model output and selected indicators to generate a risk score and assessment.

The application may return categories such as:

- **LOW RISK**
- **REVIEW**
- **SUSPICIOUS**
- **HIGH RISK**

The exact assessment depends on the implemented logic and the URL being analyzed.

A low-risk result does not establish that a website is safe. Similarly, a suspicious-looking URL should be evaluated using additional evidence before drawing a final conclusion.

Probability estimates may also be imperfect, especially when a URL differs substantially from the training data.

## 🔐 Security and Privacy

PhishingLens is intended to analyze URLs without automatically opening the submitted destination in the machine-learning inference process.

Additional precautions include:

- Validate URLs before analysis.
- Avoid entering real passwords, authentication tokens, or other secrets into test URLs.
- Treat predictions as screening results rather than definitive security guarantees.
- Use consent for email breach checks.
- Keep external-service API keys in environment variables rather than committing them to Git.
- Review the backend's network restrictions before exposing it publicly.
- Avoid uploading sensitive files to an untrusted or publicly accessible instance.
- Do not commit virtual environments, private credentials, or unnecessarily large generated artifacts.

The optional domain-intelligence backend includes restrictions intended to prevent checks against localhost, private addresses, and internal hosts. These protections should be reviewed and tested before production deployment.

Browser-local history and watchlist data may remain on the local device until cleared.

## ⚠️ Limitations

1. **Model generalization:** Performance can change when real-world URLs differ from the training dataset.
2. **False positives:** Some legitimate URLs may be classified as phishing or receive elevated contextual risk.
3. **False negatives:** Some phishing URLs may receive low-risk predictions.
4. **Probability interpretation:** Model probabilities are estimates, not guaranteed real-world probabilities.
5. **URL-only inference:** The core classifier does not fully inspect webpage content, JavaScript behavior, visual impersonation, or form submissions.
6. **External intelligence:** Domain checks depend on network access, available data, and service responses.
7. **Optional integrations:** Breach checking and some threat-intelligence functionality require additional configuration.
8. **Model dependency:** The backend cannot perform the expected inference if the compatible trained model is missing.
9. **New threats:** Newly created phishing techniques may not resemble examples in the training dataset.
10. **Educational scope:** The project is not a replacement for enterprise-grade security software or professional incident response.

## 🔮 Future Enhancements

Potential future improvements include:

- Evaluation against newer and independent URL datasets.
- Improved detection of deceptive nested subdomains.
- More comprehensive model calibration and threshold evaluation.
- Explainable AI visualizations for individual predictions.
- Additional threat-intelligence provider integrations.
- Improved monitoring of false positives and false negatives.
- Automated model and dataset version management.
- Authentication, rate limiting, and secure deployment configuration.
- Persistent scan history with an optional database.
- Automated testing and continuous integration.
- Improved support for multilingual phishing and internationalized domains.
- Deployment of the backend to a stable hosted service.

## 🧰 Troubleshooting

### Error: `ModuleNotFoundError`

Activate the project's virtual environment and install the required dependencies:

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m pip install -r backend_addon\requirements.txt
```

### Error: `No module named uvicorn`

Install Uvicorn:

```powershell
python -m pip install uvicorn
```

### Error: Model File Not Found

Check that the required model artifact exists:

```text
models/phishinglens_calibrated_v2.joblib
```

If it is missing, obtain the correct model from the project owner.

### Error: Address Already in Use

Another application may already be using port `8000`. Stop the other server or configure a different port and update the frontend's API configuration accordingly.

### Website Opens but URL Analysis Fails

1. Check that the backend terminal is still running.
2. Open `http://127.0.0.1:8000/api/v1/health`.
3. Confirm that `model_loaded` is `true`.
4. Check the browser console and network requests for errors.
5. Confirm that the frontend is requesting the correct backend URL.

### QR Decoding Does Not Work

Check that the uploaded image contains a readable QR code and that the backend add-on dependencies, including OpenCV and `python-multipart`, are installed.

### Domain Intelligence or Breach Lookup Fails

Check backend connectivity, endpoint availability, and optional provider credentials. Some checks depend on external services and may not always return results.

## 🤝 Contributing

Contributions that improve the reliability, usability, or maintainability of PhishingLens are welcome.

Suggested workflow:

1. Fork or clone the repository.
2. Create a separate branch for your changes.
3. Make focused changes without breaking the existing inference pipeline.
4. Test the relevant API endpoints and frontend workflows.
5. Document any new dependencies or configuration.
6. Submit a pull request with a clear explanation of the changes.

When modifying model features, ensure that training and inference use the same feature definitions and ordering.

## 📄 License

No specific open-source license is declared here. Before redistributing the project or its trained model, add an appropriate license and verify the usage terms of the external datasets and dependencies.

## 👨‍💻 Project Information

**Project:** PhishingLens — AI-Powered Phishing URL Detection

**Category:** Machine Learning / Cybersecurity

**Primary language:** Python

**Frontend:** HTML, CSS, JavaScript

**Backend:** FastAPI

**Machine-learning approach:** Supervised binary classification using Random Forest

**Repository:** https://github.com/puttimonish/ML_Project-PhishingLens

**GitHub Pages frontend:** https://puttimonish.github.io/ML_Project-PhishingLens/

---

*PhishingLens is an academic machine-learning project developed to explore URL-based phishing detection, contextual risk assessment, and practical cybersecurity tooling.*

**Stay alert. Analyze before you trust.** 🛡️
