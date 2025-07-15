# 📈 Get High-Value Keywords from a List of URLs

Harvest high‑value keyword ideas from any set of landing‑page URLs using the **Google Ads Keyword Plan Ideas** endpoint — all inside a single, reproducible Jupyter Notebook.

> **Notebook:** `Keyword_Planner_Tutorial.ipynb`

---

## 🚀 What this repo does

1. **Takes one or more URLs** (e.g. your competitors’ product pages).
2. Calls the **Keyword Plan Ideas** API to fetch fresh keyword suggestions, volumes & competition metrics.
3. **Cleans & aggregates** the raw ideas into a tidy DataFrame.
4. Surfaces the biggest opportunities with interactive Plotly charts.

No copy‑and‑paste out of Google Ads UI, no CSV wrangling — just run the notebook and explore.

---

## 🎒 Prerequisites

| Requirement | Why you need it |
|-------------|-----------------|
| **Python 3.9+** | Any recent 3.x works, but all examples assume ≥3.9 |
| **Google Cloud project** with **Google Ads API** enabled | The API is not on by default |
| **Service Account** _JSON key_ **file** | Used for OAuth2 service‑account flow (no user consent screen required) |
| Google Ads **developer token** | Issued from [Google Ads → Tools → API Center] |
| Your Ads **customer ID** *(login & target)* | Needed to scope requests |

### Creating the service‑account key

1. In the Google Cloud console: **IAM & Admin → Service Accounts → +Create**.
2. Grant the account **→ Basic → Viewer** (later you can restrict to Ads scopes only).
3. On the _Keys_ tab click **Add Key → JSON**. Save the file someplace safe (not in the repo!).
4. In your **Google Ads Manager** account add the service‑account email as a user (**Access & Security**) with _Standard_ access.

> ⚠️ **The service account will show up as a regular user** in Google Ads once invited & accepted.

---

## 🛠️ Quick‑start

```bash
# 1. Clone & enter the project
$ git clone https://github.com/your-org/keyword-planner-notebook.git
$ cd keyword-planner-notebook

# 2. Create an isolated env (optional but recommended)
$ python -m venv .venv
$ source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 3. Install deps
$ pip install -r requirements.txt

# 4. Export Google Ads creds (Bash / Z‑shell)
export GOOGLE_ADS_JSON_PATH="/absolute/path/to/service-account.json"
export GOOGLE_ADS_DEVELOPER_TOKEN="INSERT-YOUR-TOKEN"
export GOOGLE_ADS_LOGIN_CUSTOMER_ID="1234567890"    # manager (MCC) ID; omit dashes
export GOOGLE_ADS_CUSTOMER_ID="0987654321"          # client ID you want data for

# 5. Fire up Jupyter Lab / Notebook
$ jupyter lab
```

Open **`Keyword_Planner_Tutorial.ipynb`** and run the cells in order (or **Kernel → Restart & Run All**).

> The notebook will pick up your credentials from the four environment variables above. Alternatively, you can hard‑code the paths/IDs in the first code cell — but **don’t commit secrets**.

---

## 🏃‍♂️ How to use the notebook

1. **Edit the `seed_urls` list** in cell 2 to include the landing pages you’re analysing.
2. Tweak the **language**, **geo‑targets**, and **date range** parameters if needed.
3. Click **Run** ▶️ on each cell (or run all).
4. Inspect the final DataFrame and interactive plots to spot:
   * High‑volume / low‑competition keywords
   * The pages that trigger ad impressions for those terms
5. Export the results via the provided *Download CSV* cell, or copy–paste straight into your campaign build sheet.

---

## ❓ Troubleshooting

| Symptom | Likely cause | Fix |
|---------|--------------|------|
| `UNAUTHENTICATED` / `REQUEST_DENIED` | Wrong or missing dev‑token / customer IDs | Verify all env vars; check Ads → API Center token status |
| `USER_PERMISSION_DENIED` | Service account not added to Ads account | Invite the service‑account email as a user and accept |
| `PERMISSION_DENIED` referencing `listAccessibleCustomers` | Dev‑token in *basic* mode can’t access non‑test accounts | Request *Standard* access or use a test account |
| `QuotaError` | Too many requests, or daily quota hit | Add exponential back‑off; request higher quota |

---

## 🧩 Dependencies

Everything needed is captured in **`requirements.txt`**, but the headline libs are:

- `google-ads` → official Google Ads API client
- `pandas` + `numpy` → data wrangling
- `plotly` → charts
- `ipykernel` / `jupyterlab` → notebook runtime

---

## 📜 License

This project is licensed under the MIT License — see `LICENSE` for details.

---

## 🙌 Contributing

PRs for bug fixes or enhancements are welcome! Please open an issue first to discuss major changes.

