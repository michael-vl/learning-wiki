# Tutorial — Beginner to Advanced

Five levels. Critically, includes the **full-time worker plan** at Level 2 — that's the realistic path for most readers.

---

## Level 1 — Foundations: open an account, learn the mechanics

**Goal:** be able to navigate a brokerage, place a limit order, read a chart.

### Steps
1. Open a brokerage account at Fidelity, Schwab, or Interactive Brokers. Cash account first; you don't need margin yet.
2. Fund with $1,000–$5,000. **This is tuition money. Assume you might lose it.** If losing it would change your life, the amount is too high.
3. Buy one share each of three companies you actually understand (your employer if public, a company whose products you use, an index ETF). The point is mechanics, not selection.
4. Place a limit order, a market order, and a stop-loss order. Watch them fill.
5. Read your account statement. Understand: cost basis, unrealized P&L, realized P&L, dividends, fees.

### Read these (Level 1 reading)
- **The Intelligent Investor** (Graham) — read chapters 8 (Mr. Market) and 20 (Margin of Safety) at minimum. The rest is context.
- **A Random Walk Down Wall Street** (Malkiel) — the case for indexing. Read it to understand what you're betting *against* if you actively trade.
- **The Bogleheads' Guide to Investing** — the boring path that beats almost everyone. Required context even if you'll deviate.

After Level 1, **most readers should stop here**. Buy total-market index funds (VTI, VXUS for international, BND for bonds), set a contribution schedule, and ignore the market for 30 years. Compound returns and tax efficiency win.

---

## Level 2 — The full-time worker plan

**Goal:** participate in markets in a way compatible with a 40+ hour/week job, without your portfolio becoming your second job.

### Honest framing
- **Day trading is a poor fit for full-time workers.** You can't watch the market 9:30–4:00 ET, and the strategies that pay are time-intensive and demanding. Don't try to bend a square peg into a round hole.
- **Swing trading and position trading are reasonable.** Holding periods of days to months. You analyze evenings/weekends; you place orders that don't require live management.
- **Systematic / mechanical investing is best.** Rules-based strategies you execute on a schedule, automated where possible.

### The recommended core (boring but works)

This is what 80% of your investable money should look like, regardless of trading interest:

1. **Max your tax-advantaged accounts first.** 401(k) up to the employer match (free money), then Roth IRA contribution limit (income limits apply), then back to 401(k) up to the annual limit. HSA if eligible.
2. **Auto-invest in low-cost index funds.** A 3-fund portfolio is sufficient for most:
   - 60–80% US total market (VTI / FZROX / SCHB)
   - 10–30% international (VXUS / FZILX / SCHF)
   - 0–30% bonds (BND / SCHZ; weight increases with age and proximity to need)
3. **Rebalance quarterly or annually.** A 5%-band rule (rebalance when any asset drifts >5% from target) is fine.
4. **Don't touch this.** The S&P 500 has had 50%+ drawdowns. The plan is to ride them out. People who panic-sell at the bottom are why long-term passive investing has good returns for the disciplined.

This consumes ~1 hour per quarter. **It is not exciting. Excitement is the enemy of long-term return.**

### The "active" satellite (optional, ≤20% of investable money)

If you genuinely want to learn active trading, allocate a deliberately small "satellite" account. Treat it as an education expense.

#### Weekly rhythm for a full-time worker

- **Sunday evening (1–2 hours):** review the past week's trades. Update your trading journal. Run your screen. Build a watchlist of 5–15 candidates for the coming week.
- **Mon–Fri morning (15 min before work):** check pre-market on watchlist names. Adjust GTC limit orders if your levels changed.
- **Lunch break (5 min):** glance at positions. Don't trade impulsively.
- **After-hours (15–30 min):** read end-of-day commentary. Note what worked or didn't.
- **Saturday morning (1–2 hours):** weekly review. Are your trades following the system, or is emotion creeping in?

That's ~5 hours/week. If you can't allocate that consistently, your active satellite should be smaller or non-existent.

#### Style choices that fit this rhythm

- **Swing trading on the daily timeframe.** Hold for 3–15 trading days. Identify setups on the daily chart; place limit entries with stop-loss and take-profit; let the market work for you.
- **Trend following.** Mechanical entry/exit rules based on moving averages or breakout systems. Studied by Andreas Clenow ("Following the Trend"); fits a working schedule perfectly.
- **Long-term momentum.** Buy what's been outperforming over the past 3–12 months; rebalance monthly. Studied extensively (Jegadeesh & Titman 1993; Asness, Moskowitz, Pedersen 2013).
- **Dividend / quality investing.** Slower, simpler, well-researched.

#### Style choices that DON'T fit

- Scalping (seconds to minutes).
- News-driven day trading (you're at work when news breaks).
- Options strategies that require active management (gamma scalping, complex spreads).
- Anything you have to babysit. If you can't be away from your desk, the strategy is unsuitable.

---

## Level 3 — Technical and fundamental analysis (real version)

**Goal:** evaluate a trade idea on its merits, not on hype.

### Technical analysis (TA)

The honest version: TA is a language for describing price behavior, and *some* patterns have weak statistical edges. The cult-of-TA version (where every chart has hidden meaning) is mostly nonsense.

What's worth knowing:
- **Trend identification**: higher highs + higher lows = uptrend; opposite = downtrend; neither = chop. The simplest test that beats most retail traders.
- **Support/resistance**: price levels where buyers/sellers have repeatedly stepped in. Useful for *placement* (entries, stops, targets), not as standalone signals.
- **Moving averages**: 20/50/200-day SMA. Used in countless mechanical systems (Golden Cross, Donchian breakouts, etc.).
- **Volume**: a breakout on heavy volume is more credible than on light volume.
- **Relative strength**: a stock outperforming its sector outperforming the index is in confirmed strength. Cross-comparing matters more than absolute levels.

Skip these (no documented edge): MACD divergences, Elliott Waves, Fibonacci retracement *predictions* (lines as markers are fine), most candlestick "patterns" beyond context.

### Fundamental analysis (FA)

For longer holds, you're buying a piece of a business. Worth understanding:

- **Income statement** — revenue, gross margin, operating margin, net income.
- **Balance sheet** — assets vs. liabilities; cash; debt; book value.
- **Cash flow statement** — operating cash flow vs. net income (red flag if they diverge persistently).
- **Key ratios** — P/E, P/B, P/S, EV/EBITDA, ROE, ROIC, debt-to-equity, free cash flow yield.
- **Growth rates and trends** — 3-year and 5-year revenue/EPS growth.
- **Quality** — earnings stability, return on invested capital trend.

Sources: company 10-Ks (the annual report) on SEC EDGAR (free, authoritative). Earnings call transcripts. Investor day presentations. Don't outsource your reading to one analyst's summary; read the source.

---

## Level 4 — Systematic strategies and backtesting

**Goal:** build, test, and run rules-based strategies.

### Why systematic
- Removes emotional decisions in the moment.
- Lets you measure expectation in advance instead of guessing.
- Makes losses *expected* events you've already planned for, not surprises.

### Anatomy of a strategy

1. **Universe** — what stocks/ETFs are eligible (e.g. S&P 500, Russell 2000, ETFs only).
2. **Filter / signal** — what makes a name a candidate (e.g. "20-day breakout AND above 200-day MA").
3. **Entry rule** — when and how to buy (e.g. open of next session, limit at signal price).
4. **Position sizing** — how much per trade (e.g. risk 0.5% per trade, max 20 positions).
5. **Exit rules** — stop, target, time-based exit (e.g. trailing 10-day low; or 6-month max hold).
6. **Portfolio constraints** — max sector concentration, max total exposure, leverage cap.

A strategy without all six of these is not a strategy; it's an idea.

### Backtesting

Tools, ranked by accessibility:
- **Portfolio Visualizer** (portfoliovisualizer.com) — free; great for testing asset allocations and simple factor strategies.
- **TradingView Pine Script** — easy charting backtests; limited universe scanning.
- **QuantConnect** — Python-based, free tier, equities/futures/crypto. Steeper but real.
- **Zipline** (open source) — local Python, less maintained but works.
- **Custom Python with pandas + yfinance** — quick & dirty; do this once to truly understand.

### Backtest pitfalls (will bite you)

- **Look-ahead bias** — using data not available at the trade time (e.g., today's close to make today's open trade).
- **Survivorship bias** — backtesting on the current S&P 500 ignores companies that went to zero. Use a point-in-time index.
- **Overfitting** — tuning parameters to historical noise. Test on out-of-sample data; if you tested 100 parameter combinations, the best one is probably overfit.
- **Transaction costs** — include realistic spread + commission + slippage. A strategy that turns over weekly looks great gross and terrible net.
- **Tax drag** — short-term gains are taxed as ordinary income (US). A strategy that's only profitable pre-tax may be a loss after taxes.

### Walk-forward and live deployment

- After a backtest, **paper-trade** for 1–3 months to confirm the live behavior matches simulation. Many strategies that backtest well break in live data due to fills, slippage, or market regime change.
- Then **live-trade with minimum size** for another 3–6 months.
- Only scale to real allocation if both above pass.

---

## Level 5 — Day trading (the actual hard mode)

**Goal:** if and only if you've reached this level *and* you can quit your day job, this is what serious day trading looks like.

### Realistic prerequisites

- $50k–$100k+ trading capital you can afford to lose.
- 6–12 months living expenses in a separate account.
- Acceptance that the first 1–2 years are tuition.
- A spouse/support system that understands month-to-month income variability.
- A real edge — not vibes. A documented, backtested system or a verifiable mentor's playbook.

### Common day-trading styles

- **Opening range breakout (ORB)** — trade breakouts of the first 5/15/30 minutes' high/low. Mechanical-ish; well-studied.
- **VWAP fade / hold** — Volume-Weighted Average Price as a magnet; trade reversion to or rejection from it.
- **News momentum** — pre-market gappers on news; trade the continuation or fade.
- **Liquidity provision / scalping** — extract spread from illiquid names. Hard, capital-intensive, mostly dominated by HFTs.

### Infrastructure

- **Direct-market-access broker** (DAS Trader, IBKR TWS, Lightspeed) — not Robinhood.
- **Hotkeys** for entry/exit. You will not survive on click-through.
- **Multi-monitor setup**, news terminal, charts, scanner, level 2.
- **A mentor or paid education program** that has demonstrated profitability — not by their marketing, but by verified track records. Many "trading educators" make their money from courses, not trading.

### Risk discipline

- Daily loss limit (e.g., -2% of account). Hit it, you're done for the day. No exceptions.
- Per-trade risk ≤ 0.5% of account.
- Max 3 losing trades in a row → step away for an hour minimum.
- **Journal every trade.** Date, ticker, setup, entry, stop, exit, P&L, what you saw, how you felt. Review weekly.

### Why most fail

- Undercapitalized (PDT rules force overconcentration).
- Treat trading as gambling — chase, revenge trade, double down on losers.
- No system; trade vibes and screenshots from Twitter.
- Underestimate the toll of staring at PnL all day.
- Don't account for taxes (short-term gains hit hard).
- Quit too early or scale too late — both kill long-run probability.

### What "advanced" means

You have a documented edge. You can describe in one sentence what statistical pattern you're exploiting. You execute it for a year and your real returns track your expected returns within reasonable noise. You know your risk-adjusted returns (Sharpe, Sortino, Calmar) and they're positive after fees and taxes. **And** you didn't blow up.

That's a tiny minority of people who try.
