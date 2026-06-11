# GitHub Dashboard

Interactive Flask web dashboard for GitHub repositories. Shows open issues, pull requests, recent commits and team productivity metrics — all in one page with live charts and CSV export.

---

## What it does

| Feature | Description |
|---|---|
| **Repository filter** | Load any GitHub user or organization, then pick a specific repo |
| **KPI cards** | Total commits, open issues, open PRs, closed PRs, contributors |
| **Commits chart** | Bar chart of commit activity over the last 30 days (Chart.js) |
| **Contributors chart** | Doughnut chart of commits broken down by author |
| **Issues table** | All open issues with labels, assignee and relative timestamp |
| **Pull requests** | Tabbed view — open and closed PRs with merge status |
| **Commits table** | Recent commits with author, message and date |
| **CSV export** | Download issues or commits as a CSV file |

---

## File overview

```
github_dashboard_app8/
├── app.py               # Flask backend — all API routes
├── templates/
│   └── index.html       # Single-page dashboard (Chart.js + dark theme)
├── requirements.txt     # Python dependencies
├── .env.example         # Token template — copy to .env
└── README.md
```

---

## 1. Prerequisites

- Python 3.10 or newer
- A GitHub account
- A GitHub personal access token

---

## 2. Install dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install flask python-dotenv requests
```

---

## 3. Create your GitHub token

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Give it a name (e.g. `dashboard`)
4. Select scopes: `repo` (full) and `read:org`
5. Click **Generate token** and copy it

---

## 4. Configure the .env file

```bash
cp .env.example .env
```

Open `.env` and paste your token:

```
GITHUB_TOKEN=ghp_your_token_here
```

---

## 5. Run the app

```bash
python app.py
```

Then open your browser at:

```
http://localhost:5000
```

---

## 6. Using the dashboard

1. Enter a GitHub **username or organization** in the search box (e.g. `microsoft`, `torvalds`)
2. Click **Load Repos** — a dropdown with all their repositories appears
3. Select a repository and click **Load Data**
4. The dashboard populates with metrics, charts and tables
5. Use **Export Issues CSV** or **Export Commits CSV** to download data

---

## 7. API routes

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | Dashboard HTML |
| GET | `/api/repos?owner=X` | List repos for a user or org |
| GET | `/api/issues?owner=X&repo=Y` | Open issues for a repo |
| GET | `/api/pulls?owner=X&repo=Y` | Open and closed PRs |
| GET | `/api/commits?owner=X&repo=Y` | Recent commits (paginated) |
| GET | `/api/metrics?owner=X&repo=Y` | Commits by day + by author |
| GET | `/api/export/issues?owner=X&repo=Y` | Download issues as CSV |
| GET | `/api/export/commits?owner=X&repo=Y` | Download commits as CSV |

---

## 8. Environment variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GITHUB_TOKEN` | Yes | Personal access token with `repo` and `read:org` scopes |

---

## Troubleshooting

| Error | Fix |
|-------|-----|
| `401 Unauthorized` | Token is missing or invalid — check your `.env` |
| `403 Forbidden` | Token lacks required scopes — regenerate with `repo` + `read:org` |
| `404 Not Found` | Username or repo does not exist |
| `422 Unprocessable` | Empty repository (no commits yet) |
| Rate limit hit | Authenticated requests allow 5,000/hour — wait or use a different token |
