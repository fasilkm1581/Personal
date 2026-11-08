---
name: day-trader
description: >-
  Day-trading toolkit (11 tools in one skill). Scan the market for setups
  (opening-range breakouts, flags, oversold bounces), track breaking news and
  8-Ks, time the entry, set stop and target, replay the trade 10,000 times
  (Time Machine), size the position to a budget, risk-check it, build a broker
  ticket (paper by default, never without the user's yes), set price alerts,
  analyze earnings from SEC EDGAR, and track Congress/Pelosi stock-trade
  disclosures. Use for: "scan for setups", "any news on TSLA", "has it broken
  out", "where's my stop", "what are the odds", "how many shares", "risk
  check", "place the order", "alert me when", "how did earnings look", "what
  is Pelosi buying", or any day-trading request.
---

# day-trader

One skill, eleven tools. Each tool lives in its own subfolder with a `GUIDE.md`
(how to run it) and a plain-Python script (standard library, Python 3.8+, free
public data, no API keys). Read the matching `GUIDE.md` before running a tool.
In those guides, `${CLAUDE_SKILL_DIR}` means that tool's own subfolder
(e.g. `${CLAUDE_SKILL_DIR}/../day-trader/trader-risk`), not the top-level folder.

| user wants | read | script |
| --- | --- | --- |
| scan for setups, build a watchlist | trader-scanner/GUIDE.md | scan.py |
| news / 8-Ks on watched stocks | trader-news/GUIDE.md | news.py |
| when to get in | trader-entry/GUIDE.md | entry.py |
| stop and target | trader-exit/GUIDE.md | exit.py |
| odds / replay / backtest a trade | trader-timemachine/GUIDE.md | timemachine.py |
| how many shares | trader-budget/GUIDE.md | size.py |
| check against risk limits | trader-risk/GUIDE.md | check.py |
| place / close an order | trader-broker/GUIDE.md | ticket.py |
| price alerts, market hours | trader-alerts/GUIDE.md | alerts.py |
| earnings analysis (SEC) | trader-analyst/GUIDE.md | facts.py |
| Congress / Pelosi trades | trader-pelosi/GUIDE.md | ptr.py |

## One trade, in order

scanner -> news -> entry -> exit -> timemachine -> budget -> risk -> broker,
then alerts while it is open. Each step writes into a `trader/` folder in the
user's project and the next step reads it. news / analyst / pelosi run on their
own, on a schedule.

## Hard rules

- No order is ever placed without the user typing yes for that exact order.
  Only trader-broker can lead to an order, and only after trader-risk PASSES it.
  A BLOCK from trader-risk is final.
- Paper trading is the default. Keys live in environment variables, never in chat.
- SEC tools need `sec_user_agent` ("Name email") in `trader/config.json` or the
  `SEC_USER_AGENT` env var.
- The Time Machine is a simulation, not a prediction. Most day traders lose
  money. This is education and tooling, not financial advice.

Source: github.com/Jakeschincariol/day-trader-skill (MIT).
