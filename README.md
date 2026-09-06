# Smarterz AI

A sleek AI chat interface powered by Google Gemini Reverse Engineered (No need of API key or Authorization Cookies), deployable on Render for free.

## Features

- ⚡ Fast AI responses using Gemini 3.5 Flash
- 🎨 Beautiful dark UI, mobile + desktop responsive
- 💾 Local chat history (IndexedDB — stored only in your browser)
- 🔄 Auto-summarizes long conversations for context
- 🏷️ AI-generated chat titles
- 🔁 Auto proxy rotation on rate limits
- 🔒 No server-side storage of any conversations

## Deploy to Render (Free)

1. Push this folder to a GitHub repo
2. Go to [render.com](https://render.com) and create a new **Web Service**
3. Connect your GitHub repo
4. Settings:
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app --bind 0.0.0.0:$PORT --workers 2 --timeout 300`
   - **Python version:** 3.11
5. Click **Deploy**


## Optional Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `REQUEST_TIMEOUT` | `180` | Seconds before request times out |
| `RETRY_ATTEMPTS` | `3` | How many times to retry on error |
| `RETRY_DELAY` | `2` | Seconds between retries |
| `PROXY_LIST` | *(empty)* | Comma-separated proxy URLs for rate limit fallback. Example: `http://proxy1:8080,http://proxy2:8080` |

## Proxy Rotation

If you hit rate limits, add proxies in the `PROXY_LIST` env var:
```
PROXY_LIST=http://user:pass@proxy1.example.com:8080,http://proxy2.example.com:3128
```

The app will automatically rotate to the next proxy when it detects a rate limit (429/503) or error.

## Local Development

```bash
pip install -r requirements.txt
python app.py
# Open http://localhost:5000
```

## Architecture

- **Backend:** Python Flask + Gunicorn
- **AI Layer:** Direct calls to Gemini's StreamGenerate endpoint (no API key needed)
- **Frontend:** Vanilla JS + marked.js + highlight.js (no build step)
- **Storage:** Browser IndexedDB only — zero server-side persistence

## Privacy

All chat history lives in your browser's IndexedDB. The server processes your message and immediately forgets it. No logs, no databases, no tracking.

## Developer

Built by **Smarterz**
