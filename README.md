# AI-Fraud-Message-Detector-hackindia
ScamShield is an AI tool that detects scam and fraud messages and explains why they look suspicious. A user pastes any SMS or WhatsApp message. A machine learning model labels it as scam or not, and an LLM explains the reason in simple language, such as urgency, a fake link or a demand for money.
# ScamShield: AI Fraud Message Detector

**Team Shadow Fleet** | 13th Protocol: An AI Hackathon 2026 (HackIndia, KCCITM)
Team: Ravindra Shukla (team leader), Raunak Kumar Arora

ScamShield checks SMS and WhatsApp messages for fraud. The user pastes a suspicious
message. A machine learning model says whether it is a scam, and an LLM explains in
simple language why it looks fraudulent (urgency, fake links, requests for money or
personal details).

## Problem
Fake bank alerts, lottery prizes, KYC updates and job offers are spreading fast over
SMS and WhatsApp in India, and most people cannot tell them apart from genuine messages.

## How it works
1. **Data:** public Kaggle *SMS Spam Collection* dataset.
2. **Model:** TF-IDF features (unigrams and bigrams) with Logistic Regression (`train.py`).
3. **Explanation:** an OpenAI model explains the verdict in plain language (`explain.py`).
   If no API key is set, the app falls back to simple rule-based signals.
4. **App:** Streamlit web app where the user pastes a message (`app.py`).

## Project structure
```
app.py                    Streamlit app
train.py                  trains and saves the classifier, prints metrics
explain.py                LLM explanation + rule-based fallback
data/sample_messages.csv  tiny demo dataset (40 messages) for a quick test only
requirements.txt
.env.example
```

## Setup
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Train the model
1. Download the SMS Spam Collection from Kaggle and save it as `data/spam.csv`.
2. Run:
```bash
python train.py
```
This saves `models/scamshield.joblib` and `models/metrics.json` (accuracy, precision,
recall, F1 on a held-out 20% test set).

Quick smoke test without Kaggle: `python train.py --data data/sample_messages.csv`.
That file is too small to give meaningful accuracy.

## Enable the LLM explanation (optional)
Copy `.env.example` to `.env` and set your key:
```
OPENAI_API_KEY=your-key-here
OPENAI_MODEL=gpt-4o-mini
```

## Run the app
```bash
streamlit run app.py
```
Open the local URL shown in the terminal, paste a message and click **Check message**.

## Results
Run `python train.py` on the Kaggle dataset and write your numbers here:

| Metric | Value |
|---|---|
| Accuracy | _fill in_ |
| Precision | _fill in_ |
| Recall | _fill in_ |

Add a screenshot of the app here: `![ScamShield screenshot](screenshot.png)`

## Limitations and future scope
- The Kaggle dataset is mostly English, so Hindi/Hinglish messages are not yet well covered.
- Planned: Hindi/Hinglish support, a browser extension and a WhatsApp bot.
- ScamShield is an aid, not a guarantee. Never share OTPs, PINs or passwords, and
  do not click unknown links.
