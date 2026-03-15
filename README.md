## Professional Single‑Page SAP Startup Site (HTML/CSS/JS + Flask)

This project is a **single-page** website (HTML/CSS/JS) served by **Python Flask**, with a **Contact Us** form that sends email via **SMTP** (built-in `smtplib`).

### Project structure

```text
News/
  app.py
  requirements.txt
  .env.example
  templates/
    index.html
  static/
    css/styles.css
    js/main.js
    img/hero.webp
```

### Local setup (Windows PowerShell)

```powershell
cd d:\News
py -m venv .venv
.\.venv\Scripts\python -m pip install -r requirements.txt
.\.venv\Scripts\python app.py
```

Open `http://127.0.0.1:5000`.

### SMTP configuration

Set these environment variables (same names as `.env.example`):

- **MAIL_SERVER**: SMTP host (e.g. `smtp.gmail.com`, `smtp.office365.com`)
- **MAIL_PORT**: typically `587` (TLS) or `465` (SSL)
- **MAIL_USE_TLS**: `true`/`false`
- **MAIL_USE_SSL**: `true`/`false`
- **MAIL_USERNAME**: SMTP username
- **MAIL_PASSWORD**: SMTP password (often an **App Password**)
- **MAIL_DEFAULT_SENDER**: e.g. `"Your Company <no-reply@yourcompany.com>"`
- **MAIL_TO**: where inquiries should be delivered

Example (PowerShell for current terminal session):

```powershell
$env:MAIL_SERVER = "smtp.gmail.com"
$env:MAIL_PORT = "587"
$env:MAIL_USE_TLS = "true"
$env:MAIL_USE_SSL = "false"
$env:MAIL_USERNAME = "your_email@gmail.com"
$env:MAIL_PASSWORD = "your_app_password"
$env:MAIL_DEFAULT_SENDER = "Your Company <your_email@gmail.com>"
$env:MAIL_TO = "contact@yourcompany.com"
.\.venv\Scripts\python app.py
```

#### Development mode (don’t send real emails)

Set:

```ini
MAIL_SUPPRESS_SEND=true
```

The API will still return `{"ok": true}` so you can test the full flow.

### Contact endpoint

- **POST** `/api/contact`
- Accepts `application/x-www-form-urlencoded` (browser form post) or JSON

Quick test:

```powershell
$body = @{
  name    = "Test User"
  email   = "test@example.com"
  company = "DemoCo"
  phone   = "123"
  service = "SAP S/4HANA Migration & Transformation"
  message = "Hello from local test"
  website = "" # honeypot must be empty
}
Invoke-RestMethod -Method Post -Uri http://127.0.0.1:5000/api/contact -Body $body
```

### Editing service modules / sections

Service cards + the “Service” dropdown are plain HTML in:

- `templates/index.html`

Update titles/descriptions/tags there to match your final service catalog.

