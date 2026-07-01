# EECE 6544 — MiniProject #01: Cobblestone Gifts Sales Analysis

## What this project does
Cleans and analyses a raw 541,909-row e-commerce export from Cobblestone Gifts,
a UK online gift retailer (Dec 2010 – Dec 2011). The notebook applies all 21
required pandas data-wrangling techniques across 5 phases and answers 7 business
questions for the Head of Commercial.

## Dataset
**E-Commerce Data (UK Online Retail)** — real anonymised transaction data compiled
at London South Bank University, hosted on Kaggle.

Kaggle page: https://www.kaggle.com/datasets/carrie1/ecommerce-data

### How to download
The notebook handles this automatically via `kagglehub`. You just need a Kaggle
account and your API token set up:

1. Go to kaggle.com → Account → API → Create New Token
2. Download `kaggle.json` and place it in `~/.kaggle/` (Linux/Mac) or
   `C:\Users\<username>\.kaggle\` (Windows)
3. Run the notebook — it will download and extract the dataset automatically

Or manually: open the Kaggle page above, click Download, unzip, and place
`data.csv` in the same folder as the notebook. Then update `csv_path` in
the second code cell.

> **Note:** the file uses ISO-8859-1 encoding (not UTF-8) because it contains
> the £ symbol. The notebook handles this automatically.

## How to run

### Google Colab (recommended)
1. Upload `MiniProject_01.ipynb` to Colab
2. Set up your Kaggle token — in Colab, run:
   ```python
   from google.colab import files
   files.upload()  # upload your kaggle.json
   !mkdir -p ~/.kaggle && mv kaggle.json ~/.kaggle/ && chmod 600 ~/.kaggle/kaggle.json
   ```
3. Run all cells top to bottom (Runtime → Run all)
4. Download `clean_online_retail.csv`, `chart_monthly_revenue.png`, and
   `chart_top_markets.png` from the Colab file browser when done

### Locally
```bash
git clone <your-repo-url>
cd <repo-folder>
pip install -r requirements.txt
jupyter notebook MiniProject_01.ipynb
```

## Repository structure

```
├── MiniProject_01.ipynb          # main cleaning + analysis notebook
├── findings_summary.md           # one-page summary of all 7 business questions
├── clean_online_retail.csv       # exported clean dataset (run notebook to generate)
├── chart_monthly_revenue.png     # monthly revenue trend (run notebook to generate)
├── chart_top_markets.png         # top non-UK markets bar chart (run notebook to generate)
├── requirements.txt              # python dependencies
└── README.md                     # this file
```

## Key findings

| Question | Finding |
|----------|---------|
| Seasonality | Total revenue ~£9M; peaks in November 2011 at ~2× the average non-peak month |
| Best sellers | Top revenue and top unit lists barely overlap — two distinct demand patterns |
| Markets | Netherlands, Germany, France are top non-UK markets; Western Europe dominates |
| Customer concentration | Top 1% of customers account for a large share of revenue — wholesale-driven |
| Order value | Non-UK average order value is materially higher than UK |
| Returns | ~2% of transactions are cancellations; concentrated in a small customer group |
| Data quality | 3.6% of raw rows removed; ~25% lack CustomerID — revenue figures reliable, customer KPIs need a caveat |

## Data quality summary
- **Raw rows:** 541,909
- **Clean rows:** 522,501
- **Removed:** 19,408 (3.6%)
- **Main reasons:** non-positive quantities, cancellations, duplicates, blank descriptions
- **Repaired:** ~135,080 rows with missing CustomerID filled with 'UNKNOWN'