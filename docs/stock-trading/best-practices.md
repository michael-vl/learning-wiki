# Best Practices

## Risk management (the only thing that matters long-term)

**You can't predict markets. You can control how much you lose when wrong.** That's the entire skill.

### The hierarchy of risk control

1. **Position sizing** — risk a fixed percentage of equity per trade (commonly 0.25%–1%). This is the single most important number.
2. **Stop losses** — predetermined exit if the trade goes wrong. *Set before you enter.*
3. **Diversification** — don't have multiple trades depending on the same factor (sector, theme, macro).
4. **Portfolio heat** — sum of all open trade risks. Cap at ~5% (you survive a market-wide bad day).
5. **Drawdown limits** — pre-commit to a level (e.g., -20% account drawdown) where you stop trading and reassess.

### Math you must internalize

If you lose 50%, you need +100% to break even. Drawdowns are asymmetric:

| Drawdown | Required gain to recover |
|----------|--------------------------|
| -10%     | +11%                     |
| -25%     | +33%                     |
| -50%     | +100%                    |
| -75%     | +300%                    |
| -90%     | +900%                    |

This is why "small losses, let winners run" beats "I'll make it back." You can't make it back from large drawdowns.

### Risk:Reward and win rate together

A profitable system needs:
```
expectancy = (win_rate × avg_win) - (loss_rate × avg_loss)
```

A 40% win rate is fine if avg_win = 2× avg_loss.
A 60% win rate is a disaster if avg_win = 0.3× avg_loss.

Never evaluate your strategy on win rate alone.

## Process discipline

### Always-on rules

- **No trade without a written plan**: entry, stop, target, position size, thesis.
- **Place the stop with the entry**, not after. Brackets / OCO orders make this physical.
- **Don't move stops further away.** Ever. A widened stop is a confession.
- **Never average down** on a losing trade. You're adding to a losing thesis.
- **One trade per setup**, not three "in case it works." That's emotional sizing.
- **End of day: log every trade.** Date, ticker, setup, entry, stop, target, exit, P&L, what happened, what you felt.

### The trading journal

Without a journal, you're not trading; you're guessing and forgetting. Minimum columns:

| Date | Ticker | Setup | Direction | Entry | Stop | Target | Size | Exit | P&L | R | Notes |
|------|--------|-------|-----------|-------|------|--------|------|------|-----|---|-------|

`R` = the trade's outcome in units of risk (-1R, +2R, +0.5R, etc.). Aggregate over many trades and you have your real expectancy. Most systems people *think* are profitable are not, when measured this way.

### Weekly review

Every Saturday morning (or whatever your "off-market" window is):

1. Sum the past week's R outcomes. What's the running average?
2. Did every trade follow the plan? Mark "yes/no". Track the *yes-rate*; that's your discipline metric.
3. Did any "rule" need to change because of new information, or because you wanted it to be easier to win? The first is OK; the second is dangerous.
4. Were there setups you saw and didn't take? Why?
5. Are you over-trading? Most retail accounts have *too many* trades, not too few.

## Psychology

The classic lessons keep being true because human nature is constant:

- **Fear and greed are equally dangerous.** Fear makes you cut winners early; greed makes you hold losers and over-leverage.
- **The market doesn't owe you a comeback.** Losses are sunk cost. Each trade is independent of the last.
- **You will have streaks of luck (good and bad) far longer than your intuition expects.** A 5-loss streak in a 50%-win-rate system happens 3% of the time. Don't conclude your system is broken from one bad month.
- **Process > outcome.** A good trade can lose money; a bad trade can make money. Judge yourself by adherence to plan, not by P&L.
- **Take a break after a big win OR loss.** Both alter your judgment.
- **Don't trade on tilt.** If you're angry at the market, you've already lost the next trade.

## Taxes (US-focused, generic, NOT advice)

### Account hierarchy
- **Tax-advantaged first** — 401(k), IRA, Roth IRA, HSA. Trading inside these has no annual tax drag.
- **Taxable brokerage** — every realized gain is taxed. Short-term gains (held <1 year) at ordinary income rates. Long-term gains (≥1 year) at preferential rates (0/15/20%).
- **Wash sales** — selling at a loss and rebuying within 30 days disallows the loss in the taxable account; the basis is shifted into the new lot. Adds complexity but isn't fatal.

### For active traders specifically
- Track P&L in real time, not at year-end. Brokers provide 1099-B forms but they have errors; reconcile.
- Consider **mark-to-market election** (IRS Section 475(f)) if you qualify as a "trader in securities." Lets you treat trading as a business, deduct expenses, but converts gains/losses to ordinary income (no LTCG rate). Talk to a CPA.
- **Estimated taxes**: if you're profitable, you owe quarterly. Penalties for under-payment.

## Brokers and executions

- **Default to limit orders.** A few cents per trade compounds.
- **Use a real broker** for active trading (IBKR, Schwab, Fidelity). Commission-free brokers route to PFOF venues; for most retail, the price impact is small but real.
- **Read your fills.** If you're consistently getting filled at the worst price in the spread, your broker's routing is bad.
- **Watch fees**: data subscriptions (Level 2, real-time futures), inactivity fees, regulatory fees. They add up.

## What pros do that retail rarely does

- **Pre-commit to rules.** Then make those rules harder to break (auto orders, brackets, removed UI temptations).
- **Pre-mortem every trade**: "If this stops out, why?" If you can't articulate a clean reason, the thesis is fuzzy.
- **Backtest before trading live.** "I think this works" is not data.
- **Walk away from the market regularly.** Hourly breaks during the session, full days off weekly, months off yearly. Burnout is a real failure mode.
- **Maintain a watchlist, not a wish-list.** Names to monitor for setups, not "stocks I think will go up."
- **Pay attention to base rates.** Most strategies you can think of have been tested by quants for decades. Read the academic literature; don't reinvent.

## Pitfalls that bite everyone

1. **Confusing one good year with skill.** Bull markets cover a lot of bad strategy.
2. **Sizing up after wins** ("I'm in the zone"). The math doesn't change because of recent emotion.
3. **Sizing up after losses** ("I'll make it back"). Worse.
4. **Switching strategies after a drawdown.** A drawdown of expected magnitude is not evidence of failure.
5. **Chasing newsletter / Twitter picks.** Anyone confidently sharing trades publicly has a different P&L motive than yours.
6. **Trading in retirement accounts as if they're playgrounds.** The tax shelter is precious; preserve it.
7. **Neglecting the boring core.** A great satellite portfolio + mediocre core portfolio still loses to mediocre satellite + great core.
