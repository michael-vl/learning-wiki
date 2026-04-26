# Stock Trading — 12-Week Practice Schedule

Designed for **5–7 hours per week**. Bias: education and process before any active trading. Most weeks the homework is reading + paper-trading, not real money.

!!! warning "If you skip the reading"
    Active trading without the foundational reading is the single most reliable way to lose money in this hobby. The schedule below is structured so weeks 1–6 build the conceptual foundation; weeks 7–12 build a small live process. **Skipping ahead is more expensive than skipping entirely.**

---

## Week 1 — Setup and core philosophy

- [ ] Day 1: [Quickstart](./quickstart.md) — open brokerage, set up auto-invest
- [ ] Day 2–3: Read **The Bogleheads' Guide to Investing**, chapters 1–6
- [ ] Day 4: Set up a tracking spreadsheet (date, balance, contribution); auto-update monthly
- [ ] Day 5: Sunday review — journal: why active trading interests you (be honest)

## Week 2 — Indexing and efficient markets

- [ ] Day 1–4: Read **A Random Walk Down Wall Street** (Malkiel)
- [ ] Day 5: Journal — convince yourself in writing why your active strategy will beat indexing. If you can't, stop here. That's a win.

## Week 3 — Mechanics

- [ ] Day 1: Read [Usage](./usage.md) — order types, market structure
- [ ] Day 2: Place a limit order on a stock you own (VTI is fine); cancel before fill
- [ ] Day 3: Place a stop-loss order on the same; cancel
- [ ] Day 4: Practice OCO/bracket order syntax in your broker's interface
- [ ] Day 5: Read your account statement carefully — basis, P&L, dividends, fees

## Week 4 — Position sizing math

- [ ] Day 1: Read [Position sizing fundamentals](./usage.md#position-sizing-fundamentals)
- [ ] Day 2: Build a position-sizing spreadsheet (account_eq, risk%, entry, stop → shares)
- [ ] Day 3: Read about R-units and trade expectancy
- [ ] Day 4: Math drill — given 50% win rate, +2R on wins, -1R on losses, what's expectancy? (+0.5R)
- [ ] Day 5: Math drill — work through the asymmetric drawdown table from [Best Practices](./best-practices.md#math-you-must-internalize)

## Week 5 — Charting and TA

- [ ] Day 1: Set up TradingView free account
- [ ] Day 2: Identify trends (HH/HL = up; LL/LH = down) on 5 charts
- [ ] Day 3: Mark support/resistance on 5 charts
- [ ] Day 4: Add 20/50/200 SMAs; observe interactions
- [ ] Day 5: Pick 5 stocks; apply same TA framework; record observations

## Week 6 — Fundamental analysis primer

- [ ] Day 1: Open one company's 10-K on SEC EDGAR; read the *Business* section
- [ ] Day 2: Read its income statement; identify revenue trend, margins
- [ ] Day 3: Read its balance sheet; check debt-to-equity, cash position
- [ ] Day 4: Read its cash flow statement; compare operating cash flow vs net income
- [ ] Day 5: Calculate P/E, P/S, FCF yield from the latest data; compare to industry

## Week 7 — Build a screen

- [ ] Day 1: Open Finviz; build a screen (e.g., "S&P 500 + above 200d SMA + RSI 50–70")
- [ ] Day 2: Save the screen; review the 10 names it surfaces
- [ ] Day 3: Pick 3; apply Week-5 TA framework
- [ ] Day 4: Pick 1; apply Week-6 FA framework
- [ ] Day 5: Write a 1-page trade thesis (entry, stop, target, why)

## Week 8 — Paper trade your first system

- [ ] Day 1: TradingView paper trading account; set initial $50k virtual
- [ ] Day 2–4: Place 3 paper trades from your watchlist using your sizing rules
- [ ] Day 5: Journal — what felt different about real-feeling money?

## Week 9 — Backtesting

- [ ] Day 1: Open Portfolio Visualizer; backtest a basic asset allocation (60/30/10 stocks/bonds/intl)
- [ ] Day 2: Backtest "buy SPY when above 200d SMA, hold cash otherwise"
- [ ] Day 3: Read about backtesting pitfalls — survivorship, look-ahead, overfit
- [ ] Day 4: Build a simple Python backtest with `pandas` + `yfinance` of one strategy
- [ ] Day 5: Calculate CAGR, Sharpe, max drawdown for your tested strategies

## Week 10 — Risk management drill

- [ ] Day 1: Define your daily loss limit (e.g., -2%) and per-trade risk (≤0.5%)
- [ ] Day 2: Set up bracket orders for any open paper positions
- [ ] Day 3: Read [Best Practices](./best-practices.md#process-discipline) end-to-end
- [ ] Day 4: Build your trade journal template — date, ticker, setup, entry, stop, exit, P&L, R, notes
- [ ] Day 5: Backfill your week's paper trades into the journal

## Week 11 — First live mini-trade (optional)

If by this point you have a documented edge thesis, sizing rules, and journaling discipline:

- [ ] Day 1: Allocate ≤5% of your investable assets to an active satellite
- [ ] Day 2: Pick *one* paper-traded setup that's repeatable
- [ ] Day 3: Place ONE trade live with proper sizing and bracket
- [ ] Day 4: Don't look at it. Walk away.
- [ ] Day 5: Journal what happened. *Did you follow the plan?* (yes/no is the metric)

If you don't have those prerequisites: keep paper-trading. There is no penalty for staying paper for 6 more months.

## Week 12 — Quarterly review

- [ ] Day 1: Sum total time spent. Was it worth it? Honestly?
- [ ] Day 2: Read your journal entries from the quarter
- [ ] Day 3: Review your paper-trade ledger — actual win rate, R per trade, expectancy
- [ ] Day 4: Decide: continue active satellite, expand, or shut down and just index
- [ ] Day 5: Update [now.md](../now.md) with Q3 plan

---

## After Week 12

If you continue active trading:
- Pick **one style** (swing trend-following, momentum factor, value-quality screen) and commit to it for at least 6 months.
- Backtest in production-grade tools (QuantConnect or your own pandas backtest with no survivorship bias).
- Walk-forward paper-trade for 3 months before each scaling step.
- Never abandon your boring index core. Active is satellite, always.
