# 🎓 Automated Bubble Sheet & Essay Evaluation System

Final Software is a desktop-style examination and assessment platform built with [Eel](https://github.com/python-eel/Eel) for the UI and Flask for the backend API. It combines student/admin workflows with OMR processing, barcode detection, essay evaluation, report generation, and password-reset support in a single application.

## What the project does

- Runs a local desktop-like app from Python using an embedded web UI.
- Provides authentication, sessions, admin tools, and password reset flows.
- Processes answer sheets and related exam data through the backend.
- Supports barcode detection, fold detection, and OMR-oriented workflows.
- Includes essay text extraction and AI-assisted essay/rubric generation helpers.
- Produces reports and exportable results for exam review and analysis.

## Main features

- Login, dashboard, admin pages, report views, and settings screens.
- Forgot-password flow with OTP-based reset support.
- Bubble sheet upload and processing workflows.
- Essay review workflow with AI-assisted scoring utilities.
- Barcode detection utilities for scanned exam material.
- Database-backed storage for users, reports, and application state.

## Project structure

- [main.py](main.py): application entry point that starts the backend and launches the Eel UI.
- [app/](app): Flask backend, authentication, database, mail, security, and API logic.
- [web/](web): HTML pages and frontend assets used by the desktop UI.
- [config.py](config.py): legacy Gemini API key reference used by some helper scripts.
- [gemini_utils.py](gemini_utils.py): direct Gemini API helper functions.
- [barcode_detector.py](barcode_detector.py) and [barcode_detector_v2.py](barcode_detector_v2.py): barcode and OCR utilities.
- [essayText.py](essayText.py), [evaluate_essay.py](evaluate_essay.py), [rubric_generator.py](rubric_generator.py): essay extraction and evaluation helpers.
- [omr_backend_service.py](omr_backend_service.py): OMR backend integration.
- [requirements.txt](requirements.txt): Python dependencies.

## Important files and data

This repository is intended to keep code in Git while excluding confidential runtime data such as uploaded sheets, generated results, databases, and local environment files.

Tracked code should normally include the Python source files, the `app/` package, and the `web/` UI files.

Kept local and ignored:

- model binaries and training artifacts other than the `.h5` file you choose to track
- uploaded bubble sheets and essay images
- generated reports and export folders
- local databases and environment secrets
- virtual environments and build output

## Requirements

The app uses a local `.env` file for configuration. Typical values include email/OTP settings and optional service keys.

Example environment values:

```env
GEMINI_API_KEY=your_gemini_api_key
SENDGRID_API_KEY=your_sendgrid_api_key
SENDGRID_FROM_EMAIL=your_verified_sender@example.com
APP_RESET_BASE_URL=http://127.0.0.1:8000
SESSION_TTL_MINUTES=480
RESET_TOKEN_TTL_MINUTES=30
DEFAULT_ADMIN_USERNAME=admin
DEFAULT_ADMIN_PASSWORD=admin123
DEFAULT_ADMIN_EMAIL=admin@example.com
FOLD_MODEL_PATH=model4_cnn.h5
OMR_MODEL_PATH=best.pt
```

Notes:

- `config.py` and `app/config.py` provide defaults for many values.
- If you use email-based password reset, set the SendGrid variables.
- Model paths can be overridden through environment variables if needed.

## Installation

Create and activate a virtual environment, then install the dependencies:

```powershell
git clone https://github.com/akabirabbasnaqvi/Automated-Bubblesheet-and-Essay-Evaluation-System.git
   cd Automated-Bubblesheet-and-Essay-Evaluation-System
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

If you are using the existing environment in this workspace, activate that environment instead of creating a new one.

## Running the app

```powershell
python main.py
```

The app starts a local backend API first, then opens the desktop-style web UI on a free local port.

## Password reset flow

1. Open the login page.
2. Select `Forgot password?`.
3. Enter the email address and request an OTP.
4. Open the reset page.
5. Enter the email, OTP, and new password.
6. Submit the form to complete the reset.

## Development notes

- The repository includes scripts for checking databases, verifying results, and debugging exam batches.
- Some helpers depend on native software such as Tesseract OCR or ZBar, depending on how you run barcode and OCR workflows.
- The app is designed to run locally and should not be treated as a public multi-user deployment without additional hardening.

