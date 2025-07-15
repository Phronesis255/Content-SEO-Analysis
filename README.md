# Keyword Planner Tutorial

This repository contains a single Jupyter Notebook, **Keyword_Planner_Tutorial.ipynb**, that demonstrates how to gather keyword ideas from Google's Keyword Planner for a list of URLs and identify high-value, less competitive keywords.

## Prerequisites

- **Python 3.7+** with `pip` installed.
- A **Google Cloud service account** with access to the **Google Ads API**.
- A **developer token**, **login customer ID**, and **customer ID** from your Google Ads account.

### Setting up Google Ads API access

1. Sign in to your Google Cloud console and create a new project or select an existing one.
2. Enable the **Google Ads API** for that project.
3. Create a **service account** and download its JSON key file. Save the file somewhere safe— the notebook will reference this path as `SERVICE_ACCOUNT_FILE`.
4. In your [Google Ads manager account](https://ads.google.com/aw/apisetup), generate a **developer token** and link it to the project.
5. Note your **login customer ID** (usually your manager account ID) and the **customer ID** you want to query.
6. Make sure the service account has access to the Google Ads customer by adding it as a user with appropriate permissions.
7. Confirm that billing is enabled in the Google Ads account so the API can return results.

## Running the Notebook

1. Install the required packages:
   ```bash
   pip install google-ads plotly pandas
   ```
2. Launch Jupyter and open **Keyword_Planner_Tutorial.ipynb**.
3. Update the configuration cell with the path to your service account JSON file, your developer token, login customer ID, and customer ID:
   ```python
   SERVICE_ACCOUNT_FILE = '/path/to/service_account.json'
   DEVELOPER_TOKEN = 'YOUR_DEVELOPER_TOKEN'
   LOGIN_CUSTOMER_ID = 'YOUR_LOGIN_CUSTOMER_ID'
   CUSTOMER_ID = 'YOUR_CUSTOMER_ID'
   ```
4. Prepare a CSV file named `urls.csv` with a column called `URL` containing the pages you want to analyze.
5. Run each cell in the notebook. It will:
   - Fetch keyword ideas for each URL via the Google Ads API.
   - Aggregate and deduplicate those keywords.
   - Filter keywords that appear across eight or fewer URLs.
   - Score keywords using the formula:
     
     \[score = \log(\text{avg\_monthly\_searches} + 1) \times \frac{1}{\text{competition\_index} + 1} \times \frac{1}{\text{url\_count} + 1}\]

   - Display an interactive Plotly chart showing keyword opportunities.
   - Save the ranked keywords to `keyword_opportunities.csv`.

## Repository contents

- `Keyword_Planner_Tutorial.ipynb` – Main tutorial notebook.
- `KW_from_URL_(by_Bulk).ipynb` and `Untitled12.ipynb` – Original notebooks the tutorial was derived from.

Feel free to adapt the code for your own keyword research or content planning workflows.
