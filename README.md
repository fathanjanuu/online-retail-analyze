# Online Retail Analysis

An analysis of transaction data from a UK-based online store (Dec 2010 to Dec 2011), done in Python with pandas.

Status: work in progress. The data understanding step is done, cleaning is next.

## Background

The Online Retail dataset has over 540k transaction lines from a store that sells gift items, mostly to wholesalers. The raw data contains a lot of rows that are not regular sales (cancellations, stock adjustments, postage fees, bad debt entries), so it needs to be understood and cleaned before any real analysis.

## Business question

TODO: pick one main goal, for example

- customer segmentation (RFM + K-Means)
- sales forecasting
- market basket analysis (products bought together)

## What I found so far

- 541,909 rows, 25,900 invoices, 4,372 customers and 38 countries. About 91% of the rows are from the United Kingdom.
- 24.9% of the rows have no `CustomerID`, and it isn't random (Hong Kong is missing it entirely).
- 10,624 rows have a negative `Quantity`. 9,288 are normal cancellations (`C` invoices) and 1,336 are internal stock adjustments (price 0, no customer).
- About 2,995 rows are not products (`POST`, `DOT`, `M`, `BANK CHARGES`, etc.), plus 3 "Adjust bad debt" rows of ±11,062.06.
- Two order-then-cancel pairs with huge quantities (±80,995 and ±74,215 units), and one 12,540-unit invoice at price 0 that moves the mean `Quantity` of StockCode 84826 from 29.9 to 359.1.
- The data ends on 9 Dec 2011, so December 2011 is incomplete.

The details and code are in [`notebooks/01_data_understanding.ipynb`](notebooks/01_data_understanding.ipynb).

## Repo structure

```
online-retail-analysis/
├── data/
│   ├── raw/             # put Online Retail.xlsx here (not tracked)
│   └── processed/       # cleaned data (not tracked)
├── notebooks/
│   └── 01_data_understanding.ipynb
├── reports/             # final charts and summaries
├── requirements.txt
└── README.md
```

## How to run

1. Download the dataset from [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail) and save it as `data/raw/Online_Retail.xlsx`.
2. Create an environment and install the dependencies:
   ```bash
   python -m venv .venv
   # Windows: .venv\Scripts\activate    |  macOS/Linux: source .venv/bin/activate
   pip install -r requirements.txt
   ```
3. Run `jupyter lab` and open the notebooks in `notebooks/` in order.

## Data source

Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. See the UCI page for license terms.
