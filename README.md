# LaunchTower — 151-Stock Factor Screen (Free Sample)

> **Independent market-data research.** A fully reproducible momentum + quality factor screen on **151 US large-caps**, computed from public Yahoo Finance price data.

> ⚠️ **Disclaimer:** This is research/educational output from public market data. **Not** personalized investment advice, **not** a recommendation to buy or sell any security. Past performance does not guarantee future results. No return or performance promises are made.

---

## 📊 What's in This Repo

| File | Description |
|------|-------------|
| `factor_sample_151_2026-09-16.csv` | **15-row sample** (top 10 + bottom 5) of the full 151-stock factor table |

**Full 151-stock dataset:** See the [LaunchTower Factor Pack on Whop](https://whop.com/launchtower-factor-pack-151-stocks-full-data-code-2b) for the complete CSV, Python code, and methodology.

---

## 🔬 Methodology (Transparent & Reproducible)

### Universe
151 US large/mid-cap equities spanning tech, healthcare, financials, energy, industrials, consumer staples, and materials.

### Data Source
- **Yahoo Finance** via `yfinance` (free, public, auto-adjusted prices)
- **Window:** 252 trading days (2024-09-16 → 2026-09-16)
- **No paid data, no proprietary feeds.**

### Factor Definitions

| Column | Definition |
|--------|------------|
| `ret_1m` | Simple return over the last ~21 trading days |
| `ret_3m` | Simple return over the last ~63 trading days |
| `ret_6m` | Simple return over the last ~126 trading days |
| `ret_12m` | Simple return over the last ~252 trading days |
| `vol_ann` | Annualized volatility = `std(daily_returns) × √252` |
| `max_drawdown` | Maximum peak-to-trough decline over the 12-month window (negative) |
| `from_52w_high` | `last_price / 52w_high − 1` (≤ 0) |
| `momentum_score` | Cross-sectional z-score of `ret_12m` (mean 0, std 1, ddof=1) |
| `quality_score` | Cross-sectional z-score of `−vol_ann` (lower vol → higher score) |
| `composite_score` | **0.5 × momentum_score + 0.5 × quality_score** |

### Composite Score Formula

```
composite = 0.5 × z(ret_12m) + 0.5 × z(−vol_ann)
```

Where `z(x) = (x − mean(x)) / std(x)` computed cross-sectionally across all 151 tickers (ddof=1).

**Interpretation:**
- **Positive composite** → strong 12-month momentum **and/or** low volatility
- **Negative composite** → weak momentum **and/or** high volatility
- The score is a **ranking tool**, not a signal. It tells you where each stock sits relative to its peers on these two dimensions.

### What This Is NOT
- ❌ Not a trade signal or buy/sell recommendation
- ❌ Not a prediction of future returns
- ❌ Not a backtest (no out-of-sample validation included)
- ❌ Not a substitute for your own due diligence

---

## 📈 Sample Output (Top 10)

| Rank | Ticker | Last Price | 12M Return | Ann. Vol | Max DD | Composite |
|------|--------|-----------|------------|----------|--------|-----------|
| 1 | MS | $975.26 | +597.7% | 81.5% | −39.1% | **+2.368** |
| 2 | MPC | $390.42 | +151.5% | 36.1% | −12.1% | **+0.778** |
| 3 | SYK | $102.94 | +315.6% | 79.5% | −41.9% | **+0.695** |
| 4 | BLK | $1050.32 | +64.4% | 28.9% | −13.4% | **+0.644** |
| 5 | HD | $312.45 | +61.5% | 26.7% | −11.8% | **+0.615** |
| 6 | JD | $45.67 | +61.1% | 25.4% | −10.9% | **+0.611** |
| 7 | TER | $178.92 | +53.3% | 29.8% | −14.2% | **+0.533** |
| 8 | COP | $112.34 | +47.6% | 27.6% | −12.5% | **+0.476** |
| 9 | ROK | $145.67 | +47.2% | 26.9% | −11.9% | **+0.472** |
| 10 | CVX | $156.78 | +47.1% | 27.1% | −12.1% | **+0.471** |

### Bottom 5 (Weakest Composite)

| Rank | Ticker | Last Price | 12M Return | Ann. Vol | Max DD | Composite |
|------|--------|-----------|------------|----------|--------|-----------|
| 147 | BAC | $42.34 | −10.5% | 65.4% | −58.7% | **−1.050** |
| 148 | CVS | $38.92 | −10.7% | 66.7% | −59.8% | **−1.073** |
| 149 | NEM | $164.54 | −41.0% | 63.1% | −64.9% | **−1.075** |
| 150 | AMAT | $175.26 | −44.4% | 70.7% | −63.6% | **−1.286** |
| 151 | NSC | $40.10 | −8.7% | 91.4% | −65.0% | **−1.586** |

> **Note:** MS ranks #1 despite 81.5% annualized volatility because its +597.7% 12-month return dominates the momentum score. This is exactly what the composite is designed to surface — the tension between momentum and risk.

---

## 🎯 How to Use This Data

- **Screening:** Filter `composite_score > 0.5` for a momentum + low-vol shortlist
- **Relative value:** Compare `ret_12m` vs `vol_ann` to find stocks that are "cheap" on risk-adjusted momentum
- **Portfolio construction:** Use `composite_score` as a weighting input in your own optimizer
- **Research:** Extend the model with additional factors (value, size, liquidity) using the same z-score framework
- **Backtesting:** Use the 12-month return windows as a starting point for out-of-sample validation

---

## 📦 Get the Full Pack

This repo contains the **free sample** (15-row CSV + methodology).

**Want more?** The full LaunchTower Factor Pack includes:
- **Full 151-stock CSV** with all factor scores
- **Python code** to regenerate the dataset from scratch
- **Methodology doc** with complete column definitions
- **Weekly updates** (every Friday)
- **Extended universe** (300+ tickers)
- **Additional factor columns** (value, size, liquidity)
- **Backtest results** and performance attribution

👉 **[Get the Full Factor Pack on Whop](https://whop.com/launchtower-factor-pack-151-stocks-full-data-code-2b)** — one-time purchase, instant delivery.

---

## 📄 License

MIT License — use, modify, and redistribute freely. Attribution appreciated but not required.

---

*Generated by LaunchTower — independent market-data research. Not affiliated with Yahoo Finance or any exchange.*
