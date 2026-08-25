# AI-Powered Algorithmic Trading Signal Agent

An n8n-based agentic workflow that accepts a stock symbol through Telegram, retrieves multi-timeframe market data and recent financial news, aggregates and normalizes the data, and uses LLM-powered agents to generate a structured trading analysis.

> **Educational project:** This system generates analysis/signals and does not place live trades. It is not financial advice.

## Features

- Telegram stock-symbol input
- 1-minute, 15-minute and 30-minute candle data
- Recent news retrieval
- Market-data aggregation
- JavaScript OHLC normalization
- LLM-based news/sentiment analysis
- LLM-based final trading recommendation
- Telegram response delivery

## Architecture

```text
Telegram Trigger
   ├── 1m Market Data ──┐
   ├── 15m Market Data ──┼──> Merge -> Aggregate -> JS Normalize ──┐
   ├── 30m Market Data ──┘                                        │
   └── News API -> AI Agent (sentiment) ──────────────────────────┤
                                                                  ↓
                                                     Merge -> Aggregate
                                                                  ↓
                                                            AI Agent
                                                                  ↓
                                                          Telegram
```

## Tech Stack

- n8n
- Telegram Bot API
- Twelve Data
- NewsAPI
- OpenAI-compatible LLM
- JavaScript
- GitHub

## Workflow

1. User sends a stock symbol through Telegram.
2. Three parallel API requests retrieve 1m/15m/30m candles.
3. A separate request retrieves recent news.
4. Market responses are merged and aggregated.
5. JavaScript normalizes candle timestamps and OHLC values.
6. An AI agent analyzes the news.
7. Market data and sentiment are combined.
8. A second AI agent generates the final recommendation.
9. The result is sent to Telegram.

## Output

The agent is designed to return:

- BUY / SELL / HOLD
- Entry Price
- Stop-Loss
- Target/Exit Price
- Hold or Exit Decision

## Setup

### 1. Import

Import `workflow/ai-trading-signal-agent.json` into n8n.

### 2. Credentials

Configure your own:

- Telegram credential
- OpenAI or OpenAI-compatible model credential

### 3. API keys

Replace the placeholders for:

- Twelve Data
- NewsAPI

**Never publish real API keys, Telegram bot tokens, or credentials on GitHub.**

## Current Limitations

The current JavaScript node normalizes OHLC data; although the agent prompt mentions RSI/MACD, those indicators are not explicitly calculated by the current workflow.

The workflow also does not place live orders.

## Planned Improvements

- Explicit RSI/MACD/EMA calculations
- NSE/BSE instrument mapping
- Upstox integration for Indian market data
- Backtesting
- PostgreSQL signal/outcome storage
- Paper trading
- Risk-management rules
- Retry/error handling
- Performance metrics

## Project Structure

```text
ai-trading-signal-agent/
├── README.md
├── LICENSE
├── .gitignore
├── workflow/
│   └── ai-trading-signal-agent.json
├── docs/
│   └── architecture.md
└── screenshots/
```

## Disclaimer

For educational/software-engineering demonstration purposes only. Trading involves risk. This project is not financial advice and does not guarantee profits.
