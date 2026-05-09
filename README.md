# Fire Safety Equipment Validation Pipeline

## Overview

This project is an AI-powered fire extinguisher inspection pipeline that validates fire safety equipment from uploaded images using:

- Google Gemini Vision API
- OpenCV image preprocessing
- OCR reasoning
- Structured JSON reporting

The system performs automated fire safety checks and generates a final inspection verdict.

---

# Features

The pipeline performs the following validations:

1. Subject Verification
2. Refill Status Validation
3. Pressure Gauge Inspection
4. Tamper Seal Verification
5. Serial Number Extraction and Deduplication

Each check returns:

- PASS / FAIL / UNCERTAIN
- confidence score
- reasoning output

Final verdict:

- ACCEPT
- REJECT
- REVIEW

---

# Tech Stack

- Python
- OpenCV
- Google Gemini API
- Pillow
- JSON database

---

# Project Structure

```txt
fire_safety_pipeline/
│
├── app/
│   ├── main.py
│   ├── pipeline.py
│   ├── checks/
│   └── utils/
│
├── sample_images/
├── outputs/
├── serial_store.json
├── requirements.txt
├── .env
└── README.md
```

---

# Model Selection

Model used:

```txt
gemini-2.5-flash
```

## Why Gemini 2.5 Flash

`gemini-2.5-flash` was selected because it provides the best balance between:

- multimodal reasoning
- OCR capability
- structured JSON generation
- inference speed
- reliability
- free-tier availability

The model demonstrated strong performance for:

- fire extinguisher recognition
- handwritten refill date extraction
- pressure gauge reasoning
- tamper seal validation
- structured safety analysis

while remaining within free-tier API limits.

---

# OpenCV Usage

OpenCV is used for:

- image resizing
- grayscale conversion
- OCR enhancement
- thresholding
- blur analysis
- preprocessing optimization

before Gemini inference.

---

# Pipeline Architecture

```txt
Input Images
      ↓
OpenCV Preprocessing
      ↓
Gemini Vision Analysis
      ↓
Structured JSON Validation
      ↓
Duplicate Serial Check
      ↓
Final Verdict Engine
      ↓
JSON Report Output
```

---

# Installation

## Clone Repository

```bash
git clone <repo-url>
cd fire_safety_pipeline
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Environment Setup

Create a `.env` file:

```env
GEMINI_API_KEY=your_api_key_here
```

---

# Run Project

Place extinguisher images inside:

```txt
sample_images/
```

Run:

```bash
python -m app.main
```

---

# Output

Generated report:

```txt
outputs/report.json
```

Example output:

```json
{
  "subject_verification": {
    "status": "PASS",
    "confidence": 0.95,
    "reason": "Images clearly depict a real fire extinguisher."
  },
  "final_verdict": "ACCEPT"
}
```

---

# Verdict Logic

| Condition | Verdict |
|---|---|
| Any FAIL | REJECT |
| UNCERTAIN exists | REVIEW |
| All PASS | ACCEPT |

---

# Engineering Highlights

- Modular AI inspection pipeline
- OpenCV preprocessing
- Structured multimodal reasoning
- OCR-based date extraction
- Duplicate serial detection
- Confidence-aware outputs
- Conservative uncertainty handling

---

# Safety Design

The system intentionally prioritizes conservative safety validation.

In ambiguous cases, the system returns:

```txt
UNCERTAIN
```

instead of overconfident PASS results to reduce false approvals.

---

# Notes

- No hardcoded extinguisher layouts are used.
- No hardcoded serial formats are used.
- API keys are securely handled through environment variables.
- Duplicate serial detection uses persistent local storage.
