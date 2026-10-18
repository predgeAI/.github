# Predge — the trust layer for AI-agent payments

**Your agent paid. Did the work arrive? Predge signs the answer and refunds
the payer if not.** Delivery checks, disputes, refunds and signed receipts on
top of the payment rail, rail-agnostic by design. Live today: x402 on Base,
Solana, Arc, Monad and Algorand; the arbiter contract that rules is live on
16 mainnets including Circle's Arc, and every ruling has a
bond behind it ([how verdicts work](https://predge.io/docs#verdicts)).

**First vertical: prediction markets.** Signed settlement risk for Polymarket
markets (3,005 UMA disputes analyzed, 1 Jan to 2 Oct 2026) and whale data.
We track every Polymarket whale trade (≥ $10,000) and score wallets by
**realized win rate, computed only from resolved markets**.

Data is sold **per call over the [x402 protocol](https://x402.org)**:
USDC, no API keys, no accounts. Errors are never charged.

## The stack

| Surface | What it is |
|---|---|
| [Whale Data API](https://x402-api-production-266e.up.railway.app/) | 7 pay-per-call endpoints, $0.005–$0.03: whale feed, per-market activity, daily digest, wallet win-rate leaderboard, wallet profiles, price movers, smart-money consensus |
| [data.predge.io](https://data.predge.io) | Docs, quickstart, copy-paste agent prompt, [llms.txt](https://data.predge.io/llms.txt), [OpenAPI](https://data.predge.io/openapi.json), [x402 discovery](https://data.predge.io/.well-known/x402) |
| [`@predge/whale-data-mcp`](https://github.com/predgeAI/whale-data-mcp) | MCP server exposing the 7 endpoints as agent tools — bring a funded wallet key, your agent shops on its own |
| [@predge_alerts_bot](https://t.me/predge_alerts_bot) | The real-time Telegram product our pipeline powers (paid API data is delayed 15 min by design — Pro keeps the real-time edge) |

## Try it in 30 seconds

```bash
# window-shopping is free: the 402 carries price, schema and an example
curl -i "https://x402-api-production-266e.up.railway.app/v1/whales/latest?limit=5"

# pay for real (funded wallet key; the facilitator pays gas — no ETH needed)
npx x402-proxy "https://x402-api-production-266e.up.railway.app/v1/signals/daily"
```

## Honest-data principles

- Paid data is **delayed 15 minutes** — stated upfront, never sold as real-time.
- Young aggregates answer `{"insufficient_data": true, "reason": …}` instead of pretending.
- Win rates count **resolved markets only**; movers are trade-print-derived, not orderbook quotes.
- 4xx/5xx are never charged — settlement happens only after a successful response.

**Find us:** [predge.io](https://predge.io) · [docs](https://predge.io/docs) · [X @PredgeAI](https://x.com/PredgeAI) · [news](https://t.me/predge_news) · [data docs](https://data.predge.io)
