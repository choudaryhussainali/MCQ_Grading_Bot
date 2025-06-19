# 📝 MCQ Grading Bot

> **Automatically grade solved MCQ answer sheets from images using Google Gemini 1.5 Vision, displayed through an elegant Gradio web app.**

---
![Gradio](https://img.shields.io/badge/Built%20with-Gradio-f06) ![Python](https://img.shields.io/badge/Built%20with-Pyhton-yellow) ![License](https://img.shields.io/badge/License-MIT-green) ![Made with ❤](https://img.shields.io/badge/Made%20with-%E2%9D%A4-red) 
---

![MCQ Grading Bot Screenshot](https://github.com/user-attachments/assets/99a8fda5-adb7-490d-b473-b6a09f45d45a)



---

## Table of Contents
1. [Overview](#overview)  
2. [Key Features](#key-features)  
3. [Live Demo (Colab)](#live-demo-colab)  
4. [Architecture](#architecture)  
5. [Installation](#installation)  
6. [Configuration & API Keys](#configuration--api-keys)  
7. [Running the App](#running-the-app)  
8. [Output Format](#output-format)  
9. [Project Structure](#project-structure)  
10. [Roadmap](#roadmap)  
11. [Contributing](#contributing)  
12. [License](#license)  
13. [Acknowledgements](#acknowledgements)

---

## Overview
**MCQ Grading Bot** is a lightweight Python application that turns handwritten or printed multiple‑choice answer sheets into structured feedback in seconds. By combining Google Gemini 1.5 Vision’s image‑understanding power with an intuitive Gradio interface, teachers and automated testing systems can:

* Scan a photo of a completed MCQ paper.  
* Instantly obtain the student’s name, total questions, correct/wrong counts, score %, and a detailed per‑question breakdown.  
* Export or copy results for record‑keeping or analytics workflows.

Average response time is <5 seconds on a Colab GPU (Gemini Flash model, temperature 0.1).

---

## Key Features
| Capability | Details |
|------------|---------|
| 📸 **Image Upload** | Accepts PNG/JPG; auto‑converts to bytes for the API. |
| 🧠 **Gemini Vision Grading** | Generates a strict JSON report, then prettifies it for display. |
| 💡 **Name Detection** | Parses student name from the sheet if present. |
| 📊 **Detailed Analytics** | Correct ✓ / wrong ✗ tag on every answer plus overall percentage. |
| ⚡ **Fast & Lightweight** | No server‑side storage; everything happens in‑memory. |
| 🌐 **Colab‑Friendly** | One‑click run in Google Colab; sharing enabled. |

---

## Live Demo (Colab)
| Launch | Link |
|--------|------|
| ▶️ **Open in Colab** | [![Open In Colab](https://raw.githubusercontent.com/googlecolab/open_in_colab/master/data/icons/colab-badge.svg)](https://colab.research.google.com/github/choudaryhussainali/MCQ_Grading_Bot/blob/main/MCQ_Grading_Bot.ipynb) |

> The Colab notebook comes pre‑installed with requirements and uses **Colab Secrets** so your API keys stay private.

---

## Architecture
```text
┌───────────────┐     Image (PNG/JPG)     ┌──────────────────┐
│   Frontend    │ ───────────────────────►│  Gemini Vision    │
│  (Gradio UI)  │◄──────── Report JSON ── │  (1.5‑Flash)      │
└─────▲─┬───────┘                          └────────▲─────────┘
      │ |  Prettify + Stats                         |
      │ └───────────────────────────────────────────┘
      │            Backend (Fast in‑memory)
      └────────── Results to User (Markdown Textbox)
````

---

## Installation

1. **Clone the repo**

   ```bash
   git clone https://github.com/choudaryhussainali/MCQ_Grading_Bot.git
   cd MCQ_Grading_Bot
   ```

2. **Create a virtual environment (optional)**

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

---

## Configuration & API Keys

The app needs **Google Gemini** (and optionally **Groq**) API keys.

| Variable         | Description                    | Required |
| ---------------- | ------------------------------ | -------- |
| `GEMINI_API_KEY` | Key for Gemini 1.5 Vision      | ✅        |
| `GROQ_API_KEY`   | Key for Groq LLMs (future use) | ⬜        |

\### Option A — Colab Secrets

```python
from google.colab import userdata
# then access with userdata.get("GEMINI_API_KEY")
```

\### Option B — Environment File
Create a `.env` in project root:

```env
GEMINI_API_KEY=your_gemini_key_here
GROQ_API_KEY=your_groq_key_here
```

```bash
pip install python-dotenv
```

The script will fall back to `os.getenv()` if `google.colab` isn’t present.

---

## Running the App

```bash
python mcq_grading_bot.py      # or the filename you saved
```

The terminal prints a local URL (e.g. [http://127.0.0.1:7860](http://127.0.0.1:7860)).
Open it in your browser, upload an MCQ sheet image, and click **“Grade Answers”**.

---

## Output Format

Internally the bot expects Gemini to return **pure JSON**:

```jsonc
{
  "student_name": "John Doe",
  "total_questions": 20,
  "correct_answers": 18,
  "wrong_answers": 2,
  "score_percentage": 90,
  "mcqs": [
    {
      "question_number": "Q1",
      "question": "What is 2 + 2?",
      "correct_answer": "B",
      "student_answer": "B",
      "is_correct": true
    }
  ]
}
```

This is parsed and rendered as a neat, human‑readable Markdown report in the Gradio textbox.

---

## Project Structure

```text
MCQ_Grading_Bot/
├─ mcq_grading_bot.py          # Main Gradio app
├─ requirements.txt
├─ screenshots/
│  └─ demo.png                 # UI screenshot
├─ .env.example                # Sample env file
└─ README.md
```

---

## Roadmap

* [ ] **CSV / PDF** export of grading results
* [ ] Bulk image upload & batch grading
* [ ] Integration with LMS APIs (Moodle, Canvas)
* [ ] UI theme switcher (light/dark)
* [ ] Automated unit tests & CI workflow

---
## 🖼️ Screenshots

![Capture](https://github.com/user-attachments/assets/214b68cf-29de-4cd6-b327-ca29cc10cb45)
---
![Capture2](https://github.com/user-attachments/assets/cd9d8871-3ec5-40ba-adc5-ca9bb1da3197)
---
![Capture3](https://github.com/user-attachments/assets/d40282e3-fb86-4b92-b03e-2c6d85b9154c)
---
![Capture4](https://github.com/user-attachments/assets/9e597dee-73c5-4704-bcba-d0043f74e31f)
---
![Capture5](https://github.com/user-attachments/assets/012011d5-fae5-42a6-9810-c6c6f095e480)
---

---

## Contributing

Pull requests are welcome!

1. Fork the repo
2. Create a feature branch: `git checkout -b feat/your‑feature`
3. Commit & push: `git commit -m "Add feature"`
4. Open a PR describing your changes.

Please run `black` and `flake8` before submitting.

---

## 📄 License

This project is proprietary and confidential. All rights reserved.

```
© 2025 HUSSAIN ALI. This code may not be copied, modified, distributed, or used without explicit permission.
```

---

## 📬 Contact

For questions or collaboration requests:

* 📧 Email: [choudaryhussainali@outlook.com](mailto:choudaryhussainali@outlook.com)
* 🌐 GitHub: [choudaryhussainali](https://github.com/choudaryhussainali)


---

## Acknowledgements

* [Google Generative AI Python SDK](https://github.com/google-gemini/generative-ai-python)
* [Gradio](https://gradio.app/)
* [Pillow](https://python-pillow.org/)
* Inspired by educators streamlining assessment workflows.

---

> **Happy grading!** If this project helps you, please ⭐️ the repo and share feedback.

```
