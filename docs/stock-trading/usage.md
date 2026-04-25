# Usage — Brokers, Orders, Market Mechanics

## Brokerage accounts

A **brokerage account** is what holds your cash and securities and routes your orders to exchanges. US-resident options:

| Broker            | Strengths                                                  | Weaknesses                                |
|-------------------|------------------------------------------------------------|-------------------------------------------|
| Interactive Brokers (IBKR) | Lowest fees, best routing, global markets, professional API | Steeper learning curve                    |
| Fidelity          | Strong defaults, no commissions, good research, real fractional shares | UI is dated                              |
| Charles Schwab    | Same level as Fidelity; ThinkOrSwim platform              | Brokerage merger churn                    |
| Robinhood         | Friction-free UI                                           | Order routing economics work against you (PFOF), questionable in stress events |
| E*TRADE           | Solid mainstream                                           | Owned by Morgan Stanley, average overall  |

**For serious work: Fidelity, Schwab, or IBKR.** Robinhood is fine for tiny accounts learning UI but you give up execution quality via Payment for Order Flow (PFOF), and they have a documented history of UI-led behavior (gamification, restricted trading during volatility events).

### Account types

- **Cash account** — you trade with settled cash. No leverage. Settlement is T+1 (one business day) on US equities since May 2024.
- **Margin account** — broker lends you money against your equity (collateral). Up to 2× day-trade buying power; 4× for *Pattern Day Traders*.
- **Pattern Day Trader (PDT)** — if you make 4+ day-trades in 5 business days in a margin account *and* day trades exceed 6% of total trades, you're flagged as a PDT. PDTs need ≥ $25,000 minimum equity. Below that, your account is restricted.
- **Retirement accounts** (IRA, Roth IRA, 401k) — long-term tax-advantaged. Limited or no margin. Day trading inside an IRA is technically allowed but cash-only and the tax shelter actively discourages frequent trading.

## Order types

The most common:

| Order type        | Behavior                                                              | When to use                                                              |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Market**        | Execute immediately at best available price                           | Liquid stocks, small size, you don't care about the spread              |
| **Limit**         | Execute only at your price or better                                  | Default for most retail. Always know your fill price                     |
| **Stop (stop-loss)** | Becomes a market order when price hits your stop                  | Defining max loss                                                        |
| **Stop-limit**    | Becomes a *limit* order when stop is hit                             | Avoids slippage but can fail to fill in fast moves                       |
| **Trailing stop** | Stop that moves with price (locks in gains)                          | Riding winners                                                           |
| **GTC** (good til canceled) | Stays open until filled or canceled (broker-dependent expiry, often 60–90 days) | Most non-day-trade orders                                  |
| **Day**           | Cancels at end of session                                            | Default for day-trading                                                  |
| **OCO** (one-cancels-other) | Two orders linked; filling one cancels the other          | Bracket: take-profit + stop-loss simultaneously                          |
| **MOC / MOO**     | Market-on-close / Market-on-open — executes at the closing/opening auction | Index rebalances, end-of-day positioning                          |

**Default to limit orders.** Market orders on illiquid stocks or off-hours can fill at terrible prices. The few cents you "save" by using a limit are real money over hundreds of trades.

## Market structure

- **Regular hours**: 9:30 AM – 4:00 PM ET, Mon–Fri.
- **Pre-market**: typically 4:00 AM – 9:30 AM ET. Lower liquidity, wider spreads, news-driven moves.
- **After-hours**: 4:00 PM – 8:00 PM ET. Same caveats. Earnings reports often hit immediately after the close.
- **Closing auction**: enormous volume; most institutional flow passes through here. The MOC mechanic.

### Bid, ask, spread

Every quote is two numbers:
- **Bid** — highest price someone will buy at right now.
- **Ask** (offer) — lowest price someone will sell at right now.
- **Spread** = ask − bid. Tight spreads (1 cent on AAPL) = liquid. Wide spreads (10+ cents) = illiquid; cost of round-tripping is the spread + commissions + slippage.

If you market-buy and market-sell the same instant, you lose the spread. This is your minimum cost per round-trip.

### Order books and Level 2

- **Level 1** — best bid and ask (one price each side).
- **Level 2** — depth: how much size sits at each price level.
- For day-trading, Level 2 is informative but easily manipulated by spoofing. Don't over-rely on it.
- For long-term investing, you don't need Level 2 at all.

## Position sizing fundamentals

A position has three numbers worth knowing:
- **Entry price** — where you got in.
- **Stop price** — where the trade is "wrong" and you exit.
- **Target price** — where you take profit.

The **risk** of a trade is `(entry - stop) × shares`. If you risk $200 on every trade, the share count is determined: `shares = $200 / (entry - stop)`. This is how professionals size positions — by *risk*, not by share count or dollar amount.

**The 1% rule:** never risk more than 1% of total account equity on a single trade. With a $50k account that's $500 risk per trade. After ~100 trades a 50%-win-rate, 2:1 reward-risk strategy yields a small positive expectation; one or two big losses don't blow up the account.

## Market data and tools

- **Free real-time quotes**: most brokers include them. Some (IBKR) charge for non-US exchanges and Level 2.
- **Charts**: TradingView is the de-facto standard charting platform. Free tier covers most use cases.
- **Screeners**: Finviz (free, fundamentals + technicals), TradingView (technical), Stock Rover (paid, deep fundamentals).
- **News**: Bloomberg, Reuters, WSJ — but for trading you need it *fast*. Benzinga Pro is the retail standard.

## Common gotchas

- **Settlement and "free riding"**: you can't sell a position bought with unsettled funds in a cash account before those funds settle. Margin accounts avoid this; cash accounts limit how often you can rotate.
- **Wash sale rule**: selling at a loss and buying "substantially identical" within 30 days disallows the loss for tax purposes. Devastating for active traders in taxable accounts.
- **PDT designation** is sticky once flagged. Brokers can require an explicit account type change to lift it.
- **Halts**: trading halts on news (*Limit Up–Limit Down* halts on rapid moves; *T1/T12* halts for news). Stops do not protect you across a halt.
- **Slippage on stops**: stops are not insurance. In a gap-down open, your stop fires at the open price, possibly far below your stop level.
- **Dividends and ex-div dates**: if you're short on the ex-div date you owe the dividend; if you're long after the close on the day before ex-div you receive it.
- **Earnings announcements**: scheduled. You can look up the date. Holding through earnings is a binary event; treat it as gambling unless you have an edge in interpreting earnings.
