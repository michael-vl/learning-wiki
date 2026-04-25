# Examples — Worked Trade Setups

Each example is a *concrete* setup with rules, not a "tip." Rebuild the logic; never trade live based on a single example you read.

---

## 1. Three-fund passive portfolio

**Concept:** the boring path that beats most retail traders.

```
Account: Roth IRA, $7,000 annual contribution
Allocation:
  VTI  (US total market)        70%
  VXUS (international ex-US)    20%
  BND  (US aggregate bond)      10%

Rules:
  - Auto-invest contribution monthly via broker's recurring buy.
  - Rebalance once per year: any leg drifted >5% from target → trim and add.
  - Never sell on news. Never sell on a drawdown. Never sell because of a feeling.

Expected outcome:
  - Long-term ~7% real CAGR (historical US equity premium).
  - Will see -50% drawdowns once or twice in a 30-year horizon. That's the price.
```

This is a "trade." Reading too many YouTube videos may make it feel inadequate. It's not.

---

## 2. Dollar-cost averaging into a target allocation

**Concept:** a systematic way to avoid timing risk on a lump sum.

```
You have $24,000 to invest.
Target allocation: 80% VTI, 20% VXUS.
DCA over 12 months → $2,000/month split 80/20 ($1,600 VTI + $400 VXUS).
Auto-set as recurring buys.
```

DCA is *not* a return-maximizer (lump-sum has higher expected return). It's a regret-minimizer — protects against the scenario where you invest all $24k the day before a 30% drop.

---

## 3. Swing trade: 20-day breakout (Donchian-style)

**Concept:** buy strength, sell weakness. Mechanical trend following.

```
Universe: S&P 500 stocks above $20.

Entry rule:
  Today's close > highest close of the prior 20 trading days
  AND today's close > 200-day SMA (long-term filter)
  → buy at next day's open (limit ≤ today's close × 1.005)

Position sizing:
  Risk 0.5% of account per trade.
  Stop = lowest close of last 10 days.
  Shares = (0.005 × account_equity) / (entry - stop)

Exit rules:
  Stop = trailing 10-day low (move up only)
  Time exit: if held 100 days without hitting stop → close

Portfolio rules:
  Max 10 concurrent positions.
  Max 25% sector exposure.

Backtest first: ~2010–2024 on a survivorship-bias-free dataset.
Expect: many small losses, occasional big winners. Win rate <50% but R:R >1.
```

This is a real strategy class, well-studied. Adapt to taste — your job is to make sure you can *follow* it, not perfect it.

---

## 4. Earnings post-drift (PEAD) momentum

**Concept:** stocks that beat earnings tend to drift higher for weeks. Documented anomaly (post-earnings-announcement drift, Bernard & Thomas 1989).

```
Trigger: company reports earnings.
Filter:
  EPS surprise > +5% (actual vs. consensus)
  AND price gaps up >2% next day
  AND volume of gap day > 2× 30-day average

Entry: limit buy on day-after-earnings open + 0.5%.
Stop: 7% below entry (hard stop).
Target: hold 30 trading days OR -7% stop, whichever first.
Sizing: 1% account risk per trade.
```

The drift isn't huge per trade but adds up over 50–100 setups per year. Caveat: the size of the anomaly has shrunk as it's become well-known. Always re-test on recent data.

---

## 5. The "boring quality" filter

**Concept:** quality factor — owning high-ROIC, low-debt, profitable businesses tends to outperform the market with less drawdown over the long run (Asness, Frazzini, Pedersen 2013).

```
Universe: S&P 500.

Score each stock:
  + ROIC (5-year average) percentile
  + Gross margin stability percentile
  + Debt/EBITDA percentile (inverted — low is good)
  + Free cash flow yield percentile

Pick top 25 by composite score.
Equal-weight.
Rebalance quarterly: drop names below top 50 in score; add new top names.

Hold in a tax-advantaged account if possible (turnover creates short-term gains).
```

This is a watered-down version of what AQR / Robeco / Research Affiliates do at institutional scale. Won't beat them, but will beat random stock picking.

---

## 6. Bracket order — disciplined entry with predefined exits

When you place a swing trade, place a **bracket** — entry + stop-loss + take-profit — as one OCO order at the broker. You're not relying on yourself to babysit:

```
Entry:        BUY 100 AAPL @ $185 (limit)
Stop-loss:    SELL 100 AAPL @ $178 (stop, GTC)   [-3.8% risk]
Take-profit:  SELL 100 AAPL @ $200 (limit, GTC)  [+8.1% reward]
              R:R = 8.1 / 3.8 ≈ 2.1
```

Once filled, the stop and target are linked OCO — whichever fills cancels the other. You can go to work.

---

## 7. Tax-loss harvesting

**Concept:** realize losses to offset gains, reducing tax bill, while staying close to your target exposure.

```
Hold: 1,000 shares VOO at avg cost $410. Current price $390. Unrealized loss $20,000.

Action:
  1. Sell 1,000 VOO. Realize $20,000 loss.
  2. Immediately buy 1,000 IVV (different ticker, same S&P 500 exposure, NOT a "substantially identical" security per IRS — debatable but generally accepted for different fund families).
  3. Wait 31 days, then optionally swap back to VOO if you prefer.

Tax effect: $20,000 loss offsets up to $20,000 of gains, or up to $3,000 of ordinary income with the rest carried forward.
```

**Watch out for the wash-sale rule.** Buying the same or "substantially identical" security within 30 days disallows the loss. Auto-reinvested dividends, IRA purchases of the same security, and a spouse's account purchases all trigger the rule.

---

## 8. A position-sizing worksheet

```
Account equity:           $50,000
Per-trade risk %:         0.5%
Per-trade $ risk:         $250

Trade idea: long XYZ
  Entry:        $42.50
  Stop:         $40.00
  Risk per share: $2.50
  Shares:       $250 / $2.50 = 100

Capital used:   100 × $42.50 = $4,250  (8.5% of equity)
Max loss:       $250 (0.5%)
Reward target:  $47.50  (R:R = 2:1)  → +$500 profit
```

Do this on every trade. If you find yourself thinking "I want to put $X in" before you know the stop, you're sizing emotionally, not rationally.
