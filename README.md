# 🛡️ PhishGuard - AI/ML Phishing Threat Intelligence & URL Analysis Platform

[![Author](https://img.shields.io/badge/Author-Priyansh_Gandhi-darkgreen.svg?style=flat-square)](https://github.com/priyanshgandhi2509)
[![GitHub](https://img.shields.io/badge/GitHub-priyanshgandhi2509-181717.svg?style=flat-square&logo=github)](https://github.com/priyanshgandhi2509)
[![Institution](https://img.shields.io/badge/Institution-National_College_of_Ireland-003366.svg?style=flat-square)](https://www.ncirl.ie/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB.svg?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)

**PhishGuard** is an advanced AI/ML-powered URL security and phishing detection platform. It combines lexical structure analysis, Shannon character entropy, brand spoofing detection, homoglyph / Punycode decoding, and hybrid machine learning classification into a unified, explainable threat defense system.

---

## ✨ Features

- **🧠 Hybrid ML & Heuristic Engine**: Integrates character and word token n-grams TF-IDF with 25+ statistical and security heuristics via a calibrated classifier.
- **🔍 Explainable Security Audit**: Every scan reports exactly *why* a URL was flagged (e.g. Raw IP Host, Brand Impersonation, High Entropy, Malicious TLDs, Punycode Homographs).
- **📊 Interactive Cyber Dashboard**: Modern glassmorphism dark-theme web UI with an animated SVG risk score gauge (0-100), preset sample lures, and real-time inspection.
- **⚡ High-Throughput Batch Scanner**: Paste up to 50 URLs simultaneously and export results to CSV or JSON.
- **💻 Full-Featured CLI**: Scan single URLs or batch files from the terminal with colorized risk badges and JSON output modes.
- **🔌 REST API & Python SDK**: Easy programmatic integration for firewalls, mail filtering, or security workflows.
- **🧪 Automated Test Suite**: 17 comprehensive unit & integration tests covering heuristic extractors, model inferences, and API routes.

---

## 🚀 Quick Start

### 1. Installation

```bash
python -m pip install -r requirements.txt
```

### 2. Launch Web Dashboard

```bash
python app.py
```
Open **[http://127.0.0.1:5000](http://127.0.0.1:5000)** in your browser.

*(On Windows, you can also double-click `run.bat`)*

---

## 💻 Command Line Interface (CLI)

Scan URLs directly from your terminal using `cli.py`:

```bash
# Scan a single URL
python cli.py -u "https://www.google.com"

# Scan a suspicious URL with full explainability breakdown
python cli.py -u "http://paypal.com.security-verification.xyz/login.php"

# Batch scan multiple URLs
python cli.py -b "https://github.com" "http://192.168.1.1/auth"

# Scan a file of URLs and export to CSV or JSON
python cli.py -f urls.txt --export results.csv

# Output raw JSON to pipe into other tools
python cli.py -u "http://xn--gogle-pqa.com" --json
```

---

## 🔌 Python SDK (`phishguard_client.py`)

Integrate PhishGuard into your Python scripts:

```python
from phishguard_client import PhishGuardClient

client = PhishGuardClient()  # Uses embedded engine (zero network latency)

# Analyze URL
report = client.scan("http://paypal-security-update.xyz/login")

print(f"Verdict: {report['verdict']}")
print(f"Risk Score: {report['risk_score']}/100")
print(f"Is Phishing: {report['is_phishing']}")
print(f"Risks Detected: {[r['title'] for r in report['audit']['risks']]}")
```

To connect to a remote PhishGuard server:
```python
client = PhishGuardClient(api_url="http://127.0.0.1:5000")
```

---

## 📡 REST API Reference

### `POST /api/scan`
Analyze a single URL.
```bash
curl -X POST http://127.0.0.1:5000/api/scan \
  -H "Content-Type: application/json" \
  -d '{"url": "http://paypal.com.verify-login.xyz/auth"}'
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "url": "http://paypal.com.verify-login.xyz/auth",
    "is_phishing": true,
    "risk_level": "CRITICAL",
    "risk_score": 98.5,
    "confidence": 98.5,
    "verdict": "🛑 High Threat - Malicious / Phishing",
    "audit": {
      "risks": [
        {
          "title": "Target Brand Spoofing Detected",
          "description": "Keywords for popular brand (paypal) found in subdomain/path on an unrelated domain.",
          "severity": "CRITICAL"
        }
      ],
      "trust_signals": []
    }
  }
}
```

### `POST /api/batch-scan`
Scan up to 100 URLs in a single request.
```bash
curl -X POST http://127.0.0.1:5000/api/batch-scan \
  -H "Content-Type: application/json" \
  -d '{"urls": ["https://google.com", "http://192.168.1.1/login"]}'
```

### `GET /api/stats`
Telemetry and model health diagnostics.

---

## 🧪 Model Retraining & Benchmark Evaluation

Train the model and calculate performance metrics:

```bash
python train.py
```

To train on your own custom CSV dataset (`url,label` columns):
```bash
python train.py --data my_dataset.csv
```

---

## 🧪 Running the Test Suite

```bash
python -m pytest tests/ -v
```

---

## 📁 Project Architecture

```
PhishGuard_Antigravity/
├── app.py                  # Flask web dashboard & REST API server
├── model.py                # Hybrid ML pipeline & inference engine
├── features.py             # Heuristics extractor, Shannon entropy, homoglyph check, audit
├── dataset.py              # Benchmark training dataset & synthetic generator
├── train.py                # Model training, validation metrics & artifact serialization
├── cli.py                  # Terminal CLI scanner with JSON/CSV export
├── phishguard_client.py    # Python SDK / client library
├── requirements.txt        # Python package dependencies
├── run.bat                 # One-click Windows runner
├── templates/
│   └── index.html          # Responsive cybersecurity web UI
└── tests/
    └── test_phishguard.py  # Unit & integration test suite
```

---

## 👨‍💻 Author & Contact

* **Developer**: **Priyansh Gandhi**
* **Institution**: National College of Ireland (NCI) — MSc in Cybersecurity
* **GitHub**: [@priyanshgandhi2509](https://github.com/priyanshgandhi2509)
* **Profile**: [https://github.com/priyanshgandhi2509](https://github.com/priyanshgandhi2509)
