# 📈 IPO Edge

> **Your edge in the Indian IPO market.**  
> A full-stack web platform to explore IPO listings, track subscription data, check listing gains, and get instant answers from a Gemini AI assistant — all in one place.

---

## 🌐 Live Preview

```
Home  →  Calendar  →  Companies  →  Dive Deeper with AI  →  Learning Videos
```

*Built with Flask · SQLAlchemy · Google Gemini 2.0 Flash · Deployed via Gunicorn*

---

## ✨ Features

| Page | What It Does |
|---|---|
| 🏠 **Home** | Hero landing page — your gateway to the IPO market |
| 🏢 **Companies** | Full IPO data table with subscription stats, listing gains & current gains |
| 📅 **Calendar** | Embedded Google Calendar showing Indian market holidays (IST) |
| 🤖 **Dive Deeper with AI** | Live chat interface powered by **Google Gemini 2.0 Flash** |
| 🎓 **Learning Videos** | Curated YouTube videos to learn IPO investing from scratch |

---

## 📊 IPO Data — What's Tracked

The Companies page displays a rich table loaded from `ipo_data.csv` into a SQLite/PostgreSQL database. Each IPO record includes:

| Column | Description |
|---|---|
| **Date** | Listing date |
| **IPO Name** | Company name |
| **Issue Size (₹ Cr)** | Total funds raised |
| **QIB** | Qualified Institutional Buyer subscription (×) |
| **HNI** | High Net Worth Individual subscription (×) |
| **RII** | Retail Individual Investor subscription (×) |
| **Total Subscription** | Overall subscription multiple (×) |
| **Offer Price** | IPO issue price (₹) |
| **List Price** | Price at market debut (₹) |
| **Listing Gain %** | Gain/loss on Day 1 — color-coded 🟢/🔴 |
| **CMP (BSE / NSE)** | Current Market Price on both exchanges |
| **Current Gains %** | Returns from offer price till today — color-coded 🟢/🔴 |

---

## 🤖 AI Assistant — Gemini 2.0 Flash

The **Dive Deeper with AI** page provides a real-time chat interface backed by Google's `gemini-2.0-flash` model, configured as a financial assistant. You can ask it:

- *"What does oversubscription mean for an IPO?"*
- *"Explain QIB vs RII categories."*
- *"What is a grey market premium (GMP)?"*
- *"How do I evaluate if an IPO is worth applying for?"*

The backend Flask route `/ask-gemini` proxies your prompt to the Gemini API with a financial context system prompt and returns a clean, plain-text response.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Python 3, Flask |
| **Database** | SQLite (local) / PostgreSQL (production) |
| **ORM** | Flask-SQLAlchemy |
| **AI** | Google Gemini 2.0 Flash (`google-genai`) |
| **Frontend** | HTML5, CSS3 (Jinja2 templates) |
| **Deployment** | Gunicorn + Heroku / Render (via `Procfile`) |
| **Environment** | `python-dotenv` for `.env` config |

---

## 📁 Project Structure

```
IPOEdge/
├── app.py                        # Flask app — routes, DB model, Gemini API
├── ipo_data.csv                  # Source IPO dataset (manually updated)
├── requirements.txt              # Python dependencies
├── Procfile                      # Gunicorn deployment command
├── .env                          # API keys (never commit this!)
├── .gitignore
│
├── templates/
│   ├── website.html              # Home / landing page
│   ├── Companies.html            # IPO data table with load button
│   ├── Calendar.html             # Google Calendar embed (Indian holidays)
│   ├── Dive_Deeper_with_AI.html  # Gemini AI chat interface
│   └── Learning_Videos.html      # Curated YouTube IPO tutorials
│
└── static/
    ├── style.css                 # Global stylesheet
    └── websitehomepagefinal.jpg  # Hero section visual
```

---

## ⚡ Quickstart — Run Locally

### 1. Clone the Repository

```bash
git clone https://github.com/kushalradia2007/IPOEdge.com.git
cd IPOEdge.com
```

### 2. Create a Virtual Environment

```bash
# macOS / Linux
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up Your `.env` File

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_google_gemini_api_key_here
```

> **Get your free Gemini API key** at [Google AI Studio](https://aistudio.google.com/app/apikey)

For production with PostgreSQL, also add:

```env
DATABASE_URL=postgresql://user:password@host:port/dbname
```

If `DATABASE_URL` is not set, the app automatically falls back to a local **SQLite** database (`ipos.db`), which is perfect for local development.

### 5. Run the App

```bash
python app.py
```

Open your browser and visit: **`http://127.0.0.1:5000`**

---

## 📥 Loading IPO Data

The Companies page starts empty on first run. To populate it:

1. Navigate to **`http://127.0.0.1:5000/companies`**
2. Click the **"Load IPO Data"** button
3. The app reads `ipo_data.csv`, clears any existing records, and imports all IPO entries into the database
4. Refresh the page to see the full table

To update with new IPOs, edit `ipo_data.csv` and click the button again.

> The CSV uses these columns:  
> `Date, IPO_Name, Issue_Size(crores), QIB, HNI, RII, Total, Offer Price, List Price, Listing Gain, CMP(BSE), CMP(NSE), Current Gains`

---

## 🚀 Deployment (Heroku / Render)

The project includes a `Procfile` for seamless deployment:

```
web: gunicorn app:app
```

**Heroku:**

```bash
heroku create your-app-name
heroku config:set GEMINI_API_KEY=your_key_here
git push heroku main
```

Add the Heroku Postgres add-on for a production database — the `DATABASE_URL` env variable will be set automatically. The app handles the legacy `postgres://` → `postgresql://` URL fix required by SQLAlchemy.

**Render:**

Set `GEMINI_API_KEY` in the environment variables dashboard and use `gunicorn app:app` as the start command.

---

## 🔒 Environment Variables

| Variable | Required | Description |
|---|---|---|
| `GEMINI_API_KEY` | ✅ Yes | Your Google Gemini API key |
| `DATABASE_URL` | Optional | PostgreSQL URI (falls back to SQLite if absent) |

> ⚠️ **Never commit your `.env` file or expose your API keys.** The `.gitignore` is already configured to exclude `.env`.

---

## 📸 Pages at a Glance

### 🏠 Home
A clean hero section with the headline *"YOUR EDGE IN THE IPO MARKET"* and two call-to-action buttons — **View Current IPOs** and **Ask AI**.

### 🏢 Companies
A scrollable data table of all IPO records. Listing Gain and Current Gains columns are color-coded — green for positive returns, red for losses. Click **Load IPO Data** to (re)import from the CSV.

### 📅 Calendar
An embedded Google Calendar pre-loaded with Indian stock market holidays in the IST timezone — so you always know when markets are open or closed.

### 🤖 Dive Deeper with AI
A polished purple-themed chat UI with a scrollable message window. Ask any IPO or finance question and get a concise, professional answer from Gemini 2.0 Flash in seconds. Supports Enter key to send.

### 🎓 Learning Videos
Curated YouTube tutorials on IPO investing fundamentals — perfect for first-time investors and those looking to understand the process before applying.

---

## 🤝 Contributing

Pull requests are welcome! Ideas for future features:

- Live IPO data fetching via a public API (no manual CSV updates)
- GMP (Grey Market Premium) tracker
- Filtering, sorting, and searching on the Companies table
- User authentication and personal IPO watchlists
- Charts and visualizations for subscription trends

Feel free to fork the repo and open a PR.

---

## 📄 License

This project is licensed under the terms in the [LICENSE](LICENSE) file.

---

## 👨‍💻 Author

**Kushal Radia** — B25DS018  
Built as a Data Science project combining web development, relational databases, and AI integration.

---

*Made with 💜 for investors who want an edge.*
