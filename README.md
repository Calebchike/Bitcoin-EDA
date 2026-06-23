# Bitcoin Historical Data Analysis (2014–2026)

An exploratory data analysis of Bitcoin's daily price and volume history, from its first recorded trading days in September 2014 through mid-2026. The project asks a set of plain, practical questions about price behavior, risk, and seasonality, then answers each one in code, with a full set of visualizations to match.

Two notebooks. One asks the questions. One draws the pictures. Together they cover eleven years of a market that does not sit still.

---

## Why this project

Most Bitcoin "analysis" online is a price chart and an opinion. This project treats the dataset the way a working analyst would: state a question that someone actually wants answered, write the code to answer it, report the number, and move to the next one. No narrative is forced onto the data that the data does not support.

---

## Dataset

| | |
|---|---|
| **Source** | [Kaggle](https://www.kaggle.com) Bitcoin historical price dataset |
| **Range** | September 17, 2014 – June 5, 2026 |
| **Frequency** | Daily |
| **Records** | 4,280 rows |
| **Columns** | `Date`, `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume` |
| **Missing values** | None |

The data is read directly from a CSV hosted in this repository, so the notebooks run end-to-end with no manual download step.

---

## Repository structure

```
Bitcoin-EDA/
├── Bitcoin_EDA_Q_A_2014-2026.ipynb     # Questions and answers, in code
├── Bitcoin_EDA_Visualization.ipynb     # All charts generated in python code
├── bitcoin_dataset.csv                 # Source data
├── images/                             # Chart exports used in this README
└── README.md
```

Both notebooks are self-contained and open directly in Google Colab via the badge at the top of each file.

---

## Notebook 1: `Bitcoin_EDA_Q_A_2014-2026.ipynb`

Eleven questions, grouped into three categories, each answered with pandas and printed as a clear result.

### Price Behaviour

**Q1. What was the total return from 2014 to 2026, and what does $1,000 invested at the start become?**
Bitcoin moved from $457.33 to $60,922.67 — a total return of **13,221.26%**. A $1,000 investment on day one becomes **$133,212.63**.

**Q2. Which year had the best return? Which had the worst?**
Best year: **2017** at **+1,318.02%**. Worst year: **2018** at **−72.60%**. The spread between them is 1,390.61 percentage points in a single twelve-month swing.

**Q3. How many days did it take to 10x, 100x, and 200x from the starting price?**

| Milestone | Price | Date Reached | Time Elapsed |
|---|---|---|---|
| 10x | $4,573.34 | 2017-08-29 | 1,077 days (~2.9 years) |
| 100x | $45,733.40 | 2021-02-08 | 2,336 days (~6.4 years) |
| 200x | $91,466.80 | 2024-11-19 | 3,716 days (~10.2 years) |

**Q4. What is the largest single-day gain and the largest single-day loss?**
Largest gain: **+25.25%** on 2017-12-07. Largest loss: **−37.17%** on 2020-03-12 — the COVID liquidity crash.

**Q5. What percent of days closed green versus red? Is it close to a coin flip?**
Green days: 2,242 (**52.40%**). Red days: 2,036 (47.58%). Flat days: 1. Close to a coin flip, tilted slightly upward — consistent with an asset that has trended up over its lifetime, but not by enough to call daily direction reliably predictable from the day count alone.

### Volatility and Risk

**Q1. What is the rolling 30-day volatility, and which periods spike hardest?**
Every one of the top five volatility spikes falls in a nine-day window in **March–April 2020**, peaking at an annualized volatility of **174.49%** on 2020-04-06. The COVID crash was, by this measure, the single most violent stretch in the dataset.

**Q2. What is the largest drawdown from peak to trough, and how long did it take to recover?**
Maximum drawdown: **−83.40%**, from a peak of $19,497.40 (2017-12-16) to a trough of $3,236.76 (2018-12-15). Recovery to a new all-time high did not happen until **2020-11-30**. Full cycle — peak to bottom to new peak — took **1,080 days**, of which 364 was the crash and 716 was the climb back.

**Q3. Does volume predict direction, or is the correlation near zero?**
Correlation between volume change and signed daily return: **0.034** — essentially zero. Correlation between volume change and the *magnitude* of daily return: **0.351** — moderate. Volume tells you a big move is likely happening. It does not tell you which way.

**Q4. Is volatility clustered — do high-volatility days follow other high-volatility days?**
Day-to-day correlation of absolute returns: **0.211**. Positive and non-trivial — calm days tend to follow calm days, and violent days tend to cluster, but the effect is moderate rather than strong.

### Seasonality and Cycles

**Q1. Is there a "best month" or "worst month" pattern?**
Computed median return, mean return, and win rate for each calendar month across all years. February shows the strongest historical performance (median +11.86%, 75% win rate); January is the weakest median performer. Worth treating as a descriptive pattern from a limited number of yearly observations per month, not a dependable trading edge.

**Q2. Does the four-year halving cycle show up in the return data?**
Price is normalized to 100 on each halving date (2016-07-09, 2020-05-11, 2024-04-19) and tracked forward, to compare how each post-halving cycle progressed relative to the others.

**Q3. Are weekday returns different from weekend returns?**
Weekday average return: **0.2010%**, volatility (std dev) **3.76**. Weekend average return: **0.1127%**, volatility **2.71**. Weekdays return more on average and swing harder. Bitcoin trades seven days a week, but the human capital and institutional flow behind it still mostly does not.

---

## Notebook 2: `Bitcoin_EDA_Visualization.ipynb`

Seven charts, each built to carry one idea clearly rather than crowd several into one figure.

### Close price over time — linear and log scale

The same eleven years told two ways. Linear scale makes recent moves look enormous and early history look flat. Log scale restores proportion — the 2014–2017 run and the 2024–2026 run look comparably significant, because they were.

<img width="1600" height="533" alt="bitcoin_price_over_time " src="https://github.com/user-attachments/assets/a2a114e3-557e-4e8f-afa6-bd9a1301c261" />


### Daily trading volume over time

Volume by date, with the single highest-volume day (2021-02-26, $350.97B) marked directly on the chart.

<img width="1600" height="686" alt="bitcoin_volume_chart" src="https://github.com/user-attachments/assets/3b3fed15-a409-44f0-bea2-41557279a419" />

### Close price annotated with major market events

Price on a log scale with the 2018 crash, 2021 cycle peak, 2022 FTX crash, and 2024 pre-halving peak labeled at their exact price points.

<img width="1600" height="853" alt="bitcoin_annotated_chart" src="https://github.com/user-attachments/assets/52b443c5-0cfe-423c-a6ea-8a5e51a0c3d8" />

### Daily log returns histogram vs. normal distribution

The empirical return distribution plotted on a log y-axis against a theoretical normal curve. The tails sit visibly above the normal curve — large moves happen far more often than a normal distribution would predict. This is the chart that explains why volatility modeling and risk management for Bitcoin cannot borrow assumptions from a textbook built on equities.

<img width="1600" height="873" alt="bitcoin_returns_histogram" src="https://github.com/user-attachments/assets/3606c1e9-5c1b-42e5-b820-0024961c3290" />

### Annual returns bar chart

One bar per year, 2015–2026, green for positive and red for negative. The 2017 bar (+1,368.9%) dwarfs every other year on the same axis — included deliberately, because that's the honest shape of this asset's history.

<img width="1600" height="800" alt="bitcoin_annual_returns" src="https://github.com/user-attachments/assets/675684f2-1242-4526-a092-4b903f1dd2a6" />


### Quarterly returns bar chart

The same idea at finer resolution. Smooths out some of the extremity of the annual view while still showing how concentrated the gains and losses are within specific quarters rather than spread evenly through a year.

<img width="1600" height="700" alt="bitcoin_quarterly_returns" src="https://github.com/user-attachments/assets/019d81e1-35c3-4930-bea3-ea206e9b6c11" />

### Calendar heatmap — month × year grid

Every month's return from 2014 through 2026, in one grid. The fastest way to see both seasonal patterns and crisis months at a glance — March 2020, June 2022, and May 2021 stand out immediately in red.

<img width="1600" height="914" alt="bitcoin_calendar_heatmap" src="https://github.com/user-attachments/assets/55354a0d-3959-4272-a12b-47c9a6110b14" />

---

## Tools used

- **Python 3** — pandas, NumPy for data handling and computation
- **Matplotlib, Seaborn** — all visualizations
- **SciPy** — statistical distribution comparison
- Built and run in **Google Colab**

---

## Key takeaways

- Bitcoin's lifetime return is dominated by a handful of extreme years, not steady compounding. 2017 alone returned more than the next four best years combined.
- Drawdowns are deep and slow. An 83% drawdown took nearly three years to fully recover from.
- Volume signals *that* something is happening, not *what*. Use it for risk sizing, not direction.
- The return distribution has fat tails. Treating daily Bitcoin returns as normally distributed will understate the odds of a large move in either direction.
- Day-of-week and month-of-year patterns exist in the data, but the sample size per bucket (roughly a dozen years of observations) is thin enough that none of them should be mistaken for a reliable edge.

---
## 🚀 Machine Learning & Predictive Modeling (RapidMiner Phase)

Following the initial Exploratory Data Analysis (EDA) and feature engineering stage in Python, the engineered dataset (`bitcoin_engineered.csv`) was imported into **RapidMiner Studio** to build an end-to-end predictive pipeline for forecasting tomorrow's Bitcoin closing price (`Tomorrow_Close`).

The primary objective was to evaluate whether machine learning models could outperform a robust **Naïve Baseline Strategy** (predicting that tomorrow's price equals today's close price).

### 📐 Workflow Architecture & Methodology

The RapidMiner pipeline, shown in the optimized process view below, was designed using a dual-track parallel evaluation paradigm.

<img width="1486" height="720" alt="rapidminer_optimized_flow" src="https://github.com/user-attachments/assets/f5f8ae32-bd9f-4cd4-87d2-97e9c8599f20" />

1. **The Baseline Stream (Top Track):** Isolated the raw `Close` price, calculated the benchmark metrics using a manual `prediction` role assignment via the *Generate Attributes* operator.
2. **The Machine Learning Stream (Bottom Track):** Processed advanced engineered features through a *Select Attributes* block, normalized scales, partitioned historical data via sequential *Split Data* linear sampling (80% training / 20% testing), trained regression estimators, and applied the model for out-of-sample testing.

---

### 📥 Project Reproducibility: RapidMiner XML

For users who wish to reproduce these results or inspect the operator configurations directly in RapidMiner Studio, the full `.XML` process file used for this phase is available in the repository.

You can download the raw file here: https://raw.githubusercontent.com/Calebchike/Bitcoin-EDA/refs/heads/main/Bitcoin_Naive_%26_Linear_Regression_Model.xml

*To use this file: Download it, open RapidMiner Studio, and import the file as a new process. Note: You will need to re-link the 'Retrieve' operator to your local copy of the engineered dataset.*

---

### 📊 Iterative Model Performance & Benchmark Results

The performance of each model was strictly evaluated using **Root Mean Squared Error (RMSE)** to penalize large, volatile price miscalculations.

| Model Tier / Workflow Variant | Test RMSE ($) | Technical Engineering Verdict |
| :--- | :--- | :--- |
| **Naïve Baseline Benchmark** | *~1,148.49* | 🎯 The target random-walk benchmark to beat. |
| **Initial SVM (Linear)** | ~71,110.94 | ❌ Completely decoupled; flat lines failed on non-linear exponential cycles. |
| **Neural Network** | ~21,964.30 | ⚠️ Overfitted to training regimes; struggled on standard tabular timeline horizons. |
| **Baseline Linear Regression** | ~6,340.13 | 📈 Significant structural improvement after adjusting capability constraints to regression. |
| **Optimized Linear Regression** | **~2,789.97** | 📈 Massive breakthrough; cut ML error by over 56%. |

---

### Key Technical Breakthroughs & Optimization

The transition from a raw **$6,340 RMSE** down to a highly competitive **$2,789 RMSE** represents the core analytical victory of this phase:

1. **Handling Multicollinearity (Feature Pruning):** Linear Regression models natively degrade when fed features tracking identical structural patterns. By systematically pruning highly correlated, slow-moving indicators (**`SMA_30`** and **`Rolling_Vol_30d`**), and removing raw day-of **`Volume`** noise (while retaining `Volume_Lag_1`), the feature space was targeted specifically toward short-term momentum flags (`Close_Lag_1`, `Close_Lag_2`, `SMA_7`, and `Rolling_Vol_7d`).
2. **Magnitude Scale Equalization:** By incorporating a data-wide **`Normalize`** step (Z-score transformation) ahead of data splitting, the absolute scale disparities between massive raw transactional volumes and fractional percentage daily returns were eliminated. This ensured balanced feature weight allocations across the linear solver.

---

## Coming next

A predictive modeling layer — time-series forecasting models, plus a backtested moving-average crossover strategy — is planned as a third notebook to extend this EDA into an actual trading-signal evaluation.

---

## Author

**Caleb Chisom Chike**
Repo: [github.com/Calebchike/Bitcoin-EDA](https://github.com/Calebchike/Bitcoin-EDA)
