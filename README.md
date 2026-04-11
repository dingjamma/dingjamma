# Hi, I'm James Ding

**Associate Data Analyst @ AirSprint Private Aviation | Calgary, AB**

Forecasting, analytics pipelines, and turning messy aviation data into actionable insights by day. Building autonomous agents with real money on the line by night.

james@dingjames.com  ·  [LinkedIn](https://linkedin.com/in/dingjames)  ·  [dingjames.com](https://dingjames.com)

---

## What I'm Building

### 🤖 [polymarket-detector](https://github.com/dingjamma/polymarket-detector)

**An AWS Lambda bot that reads live Polymarket tech markets, forms an independent probability estimate with Claude, and places bets when it sees edge — with a homegrown insider-trading detector as a defensive filter.**

Every 15 minutes, the bot:

1. Fetches all live Polymarket markets and filters to tech-category markets above $10k liquidity
2. Scores recent whale trades for insider fingerprints (dormant wallets, abnormal size z-scores, proximity to resolution) and blacklists manipulated markets
3. Runs a two-tier Claude cascade — **Haiku 4.5** shortlists 3–5 candidates, **Sonnet 4.6** forms its own probability estimate and decides `BUY` / `SELL` / `SKIP` with confidence and rationale
4. Passes each non-SKIP through hard risk guardrails ($10/trade, $100/day, $400 open exposure) then either paper-logs or signs and submits via `py-clob-client`
5. Records every decision to DynamoDB + S3 for audit
6. Runs a bug-detection circuit breaker — halts on slippage spikes, consecutive API errors, or parse failures, but *not* on losing trades (losing trades are the game)

**Example decision from the first real run:**

> **Market:** "Will GPT-6 be released before GTA VI?"
> **Market YES price:** 0.675  ·  **Sonnet's estimate:** ~0.42
> **Decision:** BUY NO at 0.325 — edge ≈ 0.25 vs 0.08 threshold
> **Rationale:** *"GTA VI has a confirmed 2025 release window. GPT-6 has no announced date and would follow GPT-5. Even accounting for delay risk, the NO price offers significant edge."*

Running at ~$1/day all-in on AWS. Paper-mode first, seven-day review, then real money.

---

## Stack

**Python** · **AWS** (Lambda, Bedrock, DynamoDB, S3, Secrets Manager, EventBridge, CloudWatch, CDK) · **Claude Haiku 4.5 + Sonnet 4.6** · **py-clob-client** · **pytest + moto + respx** for end-to-end mocked testing

Day job: pandas, NumPy, scikit-learn, XGBoost, Prophet, Tableau, Power BI.

---

## Let's Talk About

- Autonomous LLM agents with real money on the line and how to keep them from blowing up
- Bedrock, cross-region inference profiles, and the IAM rabbit hole
- Prediction markets, insider trading on-chain, and where the actual edge lives
- Time-series forecasting in real business settings
- How oil prices drive Alberta real estate
