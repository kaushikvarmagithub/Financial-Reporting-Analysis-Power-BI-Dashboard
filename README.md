# 📊 Financial Reporting & Analysis — Power BI Dashboard

> A multi-page Power BI report for end-to-end financial performance tracking — from Sales Revenue and Gross Profit to EBITDA, Net Profit, and Cross-Country comparisons.

---

## 📈 Project Stats

| Metric | Value |
|---|---|
| GL Transactions | 27,910 rows |
| Date Range | 2018 – 2020 |
| Countries | 7 |
| Report Pages | 4 |
| Data Source | Microsoft Excel (.xlsx) |

---

## 🗂️ Project Structure

```
Financial-Reporting-PowerBI/
│
├── 📗 Finacial_Data.xlsx                              ← Source data (6 sheets, 27,910 rows)
├── 🟠 Finanicial_Reporting_And_Analysis_PowerBI_.pbix ← Power BI Report (4 pages)
└── 📄 README.md                                       ← This file
```

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI** | Interactive report pages with slicers, KPIs, pivot tables, and trend charts |
| **Microsoft Excel** | Source data workbook with 6 structured sheets |
| **Star Schema** | Fact table (GL) linked to dimension tables via surrogate keys |
| **Date Intelligence** | Calendar dimension enabling YTD, TTD, and period-over-period analysis |

---

## 🗃️ Data Model — Excel Workbook

The Excel workbook (`Finacial_Data.xlsx`) contains **6 sheets**:

### 📋 GL — General Ledger *(Fact Table · 27,910 rows)*

| Column | Type | Description |
|---|---|---|
| Index | PK | Unique row identifier |
| Date | DATE | Transaction date (2018–2020) |
| Territory_key | FK | Links to Territory dimension |
| Account_key | FK | Links to Chart of Accounts |
| Details | TEXT | Transaction description |
| Amount | NUMBER | Transaction value |

---

### 🗂️ Chart of Accounts *(Dimension)*

| Column | Type | Description |
|---|---|---|
| Account_key | PK | Surrogate key |
| Report | TEXT | Balance Sheet / Profit and Loss / Adjusting |
| Class | TEXT | Assets, Liabilities, Trading, Operating, etc. |
| SubClass | TEXT | Sub-classification |
| Account | TEXT | Account name |
| SubAccount | TEXT | Sub-account name |

---

### 🌍 Territory *(Dimension · 7 rows)*

| Column | Type | Description |
|---|---|---|
| Territory_key | PK | Surrogate key |
| Country | TEXT | USA, Canada, UK, Germany, France, Australia, New Zealand |
| Region | TEXT | North America, Europe, Oceania |

---

### 📅 Calendar *(Dimension)*

| Column | Type | Description |
|---|---|---|
| Date | DATE | Full date |
| Year | NUMBER | 2018, 2019, 2020 |
| Quarter | TEXT | Qtr 1 – Qtr 4 |
| Month | TEXT | Jan – Dec |
| Day | TEXT | Mon – Sun |

---

### 💵 CashFlow_St *(Mapping Table)*

| Column | Type | Description |
|---|---|---|
| Type | TEXT | Cash flow category |
| Subtype | TEXT | Sub-category |
| Account | TEXT | Account name |
| SubAccount | TEXT | Sub-account name |
| ValueType | TEXT | Opening balance / FTP |
| Account_Key | FK | Links to Chart of Accounts |

---

### 📈 SoCE_St — Statement of Changes in Equity *(Mapping Table)*

| Column | Type | Description |
|---|---|---|
| Type | TEXT | Equity category |
| Account | TEXT | Share Capital, Share Premium, Retained Earnings, etc. |
| Balancetype | TEXT | Opening balance type |
| AccountKey | FK | Links to Chart of Accounts |

---

## 📄 Report Pages

### Page 1 — Sales

```
┌─────────────────────────────────────────────────────────┐
│  FILTER: Year | Quarter | Month                [Slicer] │
├────────────────────────────────┬────────────────────────┤
│  Sales Revenue — Pivot Table   │  Total Sales Revenue   │
│                                │                        │
│  Country  2018   2019   2020   │     $21.0M             │
│  USA      $2.1M  $2.4M  $2.6M │   ▲ 12.8% vs prior yr │
│  UK       $1.3M  $1.5M  $1.7M │                        │
│  Germany  $0.9M  $1.0M  $1.1M │                        │
│  Total    $6.2M  $7.0M  $7.8M │                        │
├────────────────────────────────┴────────────────────────┤
│  Monthly Sales Revenue Trend          YoY Growth Line   │
│  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~     ~~~~~~~~~~~~~~~~  │
└─────────────────────────────────────────────────────────┘
```

**Visuals:** Pivot Table · 2× Line Charts · Period Slicer · KPI Card

---

### Page 2 — Profit & Loss

```
┌──────────────────────────────────────────────────────────────────┐
│  KPIs:  Sales TTD: $7.8M  │  Gross Profit: $3.2M  │  EBITDA: $2.1M  │
│         Net Profit: $1.4M │  PBIT: $1.8M          │  Op. Profit: $2.0M │
├──────────────────────────────────┬───────────────────────────────┤
│  P&L Monthly Breakdown           │  Net Profit Monthly Trend     │
│                                  │                               │
│  Metric       Actual   Budget    │   ~~~~~~~~~~~~~~~~~~~~        │
│  Sales        $7.8M    $7.5M     │                               │
│  COGS        $(4.6M)  $(4.5M)    │                               │
│  Gross Profit $3.2M    $3.0M     │                               │
│  EBITDA       $2.1M    $1.9M     │                               │
└──────────────────────────────────┴───────────────────────────────┘
```

**Visuals:** 6× Pivot Tables · KPI Card · KPI Visual · 3× Line Charts · 2× Slicers

---

### Page 3 — Cross Country

```
┌──────────────────────────────────────────────────────────────────┐
│  Sales Revenue by Country        │  Gross Profit Trend           │
│                                  │                               │
│  USA         ████████████ $7.1M  │  USA    ~~~~~~~~~~~~~~~~~~~   │
│  UK          ███████      $4.5M  │  UK     - - - - - - - - - -   │
│  Germany     █████        $3.0M  │  Germany ................     │
│  Australia   ████         $2.4M  │                               │
│  France      ███          $1.8M  ├───────────────────────────────┤
│  Canada      ██           $1.5M  │  Net Profit Multi-Country     │
│  NZ          █            $0.8M  │  USA / Australia / France     │
└──────────────────────────────────┴───────────────────────────────┘
```

**Visuals:** 3× Line Charts (Sales Revenue, Gross Profit, Net Profit) segmented by country

---

### Page 4 — Extended P&L *(Duplicate of P&L + Extended)*

```
┌──────────────────────────────────────────────────────────────────┐
│  Sales Revenue                   │  Sales to Marketing Cost      │
│  Line + Column Combo Chart       │  Stacked Column + Line Combo  │
│                                  │                               │
│  ▓▓ ▓▓ ▓▓ ▓▓ ▓▓ ▓▓ ▓▓           │  ██ ██ ██ ██ ██ ██           │
│  ~~~~~~~~~~~~~~~~~~              │  -- -- -- -- -- -- (ratio)    │
├──────────────────────────────────┼───────────────────────────────┤
│  Gross Profit Margin %           │  Net Profit Margin %          │
│                                  │                               │
│  Country  2018   2019   2020     │  Country  2018   2019   2020  │
│  USA      41.2%  42.5%  43.8%    │  USA      18.4%  19.2%  20.1%│
│  UK       38.5%  39.1%  40.2%    │  UK       16.0%  17.1%  18.3%│
│  Germany  36.0%  37.4%  38.6%    │  Germany  14.5%  15.6%  16.8%│
└──────────────────────────────────┴───────────────────────────────┘
```

**Visuals:** Line+Column Combo Chart · Stacked+Line Combo Chart · 2× Margin Pivot Tables · All P&L KPIs

---

## 🌍 Countries Covered

| Country | Region |
|---|---|
| 🇺🇸 USA | North America |
| 🇨🇦 Canada | North America |
| 🇬🇧 UK | Europe |
| 🇩🇪 Germany | Europe |
| 🇫🇷 France | Europe |
| 🇦🇺 Australia | Oceania |
| 🇳🇿 New Zealand | Oceania |

---

## 📑 Financial Reports Supported

- ✅ Profit & Loss Statement
- ✅ Balance Sheet
- ✅ Cash Flow Statement
- ✅ Statement of Changes in Equity (SoCE)

---

## 🚀 Getting Started

**Step 1 — Check the Data Source**

Open `Finacial_Data.xlsx` and verify all six sheets are present:
`GL`, `Chart of Accounts`, `Territory`, `Calendar`, `CashFlow_St`, `SoCE_St`

**Step 2 — Open in Power BI Desktop**

Open the `.pbix` file in **Power BI Desktop (February 2024 or later)**.

**Step 3 — Update the Data Source Path**

Go to: `Home → Transform Data → Data Source Settings`  
Update the file path to point to your local copy of the Excel file.

**Step 4 — Refresh Data**

Click `Home → Refresh` to load all 27,910 GL transactions into the model.

**Step 5 — Explore the Pages**

Navigate the four report pages using the tabs at the bottom:
`Sales` → `P&L` → `Cross Country` → `Extended P&L`

Use the **Year / Quarter / Month slicers** on each page to filter the view.

---

## 📌 Notes

- The `.pbix` file was last saved on **11 February 2024**
- All financial figures in the pivot tables are derived from the GL via DAX measures
- The Calendar table enables time-intelligence functions (TTD, YTD, prior-period comparisons)
- Territory dimension covers **3 regions** across **7 countries**

---

*Financial Reporting & Analysis · Power BI · Data: 2018–2020 · 7 Countries · 27,910 Transactions*
