<p align="center">
  <img src="docs/images/wafyurl-banner.webp" alt="WafyURL — Shorten Smarter. Share Faster. Track Everything." width="100%">
</p>

# WafyURL

**Shorten smarter. Share faster. Track everything.**

WafyURL is a Flask-based URL shortener with custom aliases, optional password protection, expiring links, click analytics, QR-code support, bulk shortening, and destination-page previews.

**Live website:** https://url.amwafy.xyz  
**Source code:** https://github.com/afeemuhammodwafy1/wafyurl

## Features

- **Short links:** Create short URLs from publicly accessible HTTP or HTTPS destinations.
- **Custom aliases:** Choose a custom short code when it is available.
- **Password-protected links:** Require a password before redirecting to a destination.
- **Link expiration:** Set links to expire after 1 hour, 24 hours, 7 days, or 30 days.
- **Click analytics:** Record clicks and available referrer, device, browser, operating-system, and location information.
- **QR codes:** Generate QR codes for shortened links.
- **Bulk shortening:** Submit multiple URLs in one batch (the interface supports up to 50 URLs per batch).
- **Link preview:** Retrieve page title, description, and Open Graph image metadata.
- **Rate limiting:** Apply an in-process IP-based request limit to the shortening endpoint.
- **SEO endpoints:** Provide `robots.txt` and a sitemap.

## Technology

- Python and Flask
- Flask-SQLAlchemy
- PostgreSQL in production; SQLite is the local default
- HTML, CSS, and vanilla JavaScript
- Gunicorn
- Render/Vercel deployment configuration

## Run locally

### Requirements

- Python 3.10 or newer (the Render configuration specifies Python 3.11)
- pip
- A PostgreSQL database for production; local development can use SQLite by default

### 1. Clone the repository

```bash
git clone https://github.com/afeemuhammodwafy1/wafyurl.git
cd wafyurl
```

### 2. Create and activate a virtual environment

**Windows (Command Prompt):**

```bat
python -m venv venv
venv\Scripts\activate
```

**Windows (PowerShell):**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Linux/macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Set a strong, unique `SECRET_KEY` before deploying. To use PostgreSQL, set `DATABASE_URL` to your database connection URL. If `DATABASE_URL` is omitted, the app uses a local SQLite database.

Example `.env` file (if you use `python-dotenv` in your local setup):

```env
SECRET_KEY=replace-with-a-long-random-secret
DATABASE_URL=postgresql://USER:PASSWORD@HOST:PORT/DATABASE
```

Never commit real secrets, passwords, or production database credentials. The `.env` file should remain private.

### 5. Start the app

```bash
python app.py
```

Open http://localhost:5000 in your browser.

## Deployment

The repository includes `Procfile`, `render.yaml`, and `vercel.json` deployment configuration. The live deployment is:

**https://url.amwafy.xyz**

Configure `SECRET_KEY` and (for persistent production storage) `DATABASE_URL` in the hosting provider's environment settings. Confirm the selected host supports the app's database and filesystem/runtime requirements before deploying.

## Data and privacy notes

- Click analytics may store IP address, user-agent, referrer, and approximate location data returned by the configured IP geolocation service.
- Scan history and account behavior should be reviewed against the current implementation before making privacy claims; this project does not document a user account system.
- The in-process rate limiter is not shared across multiple worker processes and may reset when the process restarts.
- The link-preview endpoint is intended for public HTTP(S) URLs and blocks local/private-network targets; redirects are not followed.
- Keep `SECRET_KEY` private and use a strong production value.
- Password-protected links should not be treated as a substitute for sharing sensitive information through a dedicated secure channel.

## Project structure

```text
wafyurl/
├── docs/
│   └── images/
│       └── wafyurl-banner.webp
├── static/
│   ├── css/
│   └── js/
├── templates/
├── app.py
├── app.py.txt
├── icon.webp
├── Procfile
├── render.yaml
├── requirements.txt
└── vercel.json
```

## Contributing

Bug reports and improvements are welcome. Open an issue with steps to reproduce the problem, or submit a pull request with a clear description of the change.

## License

This project is licensed under the [MIT License](LICENSE).

## About

**WafyURL** is a product of **Wafyro Software**.

**Founder and Software Developer:** Afee Muhammod Wafy  
