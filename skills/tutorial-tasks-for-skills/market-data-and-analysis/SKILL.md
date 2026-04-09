---
name: market-data-and-analysis
description: |
  Real-time and historical crypto market data: price, volume, order book depth, candlesticks, and basic technical analysis where requested.
  Typical: spot price quotes, depth, klines, simple indicators (e.g. moving averages).
  Boundaries: primarily spot and derivatives-trading-usds-futures; combine with other analysis tools for heavier quant work.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-market-data-and-analysis
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/market-data-and-analysis/SKILL.md
license: MIT
---

# Market Data and Analysis Task

## Description

**Task Description**: Provides users with real-time and historical market data for cryptocurrencies, including price, volume, order book depth, and candlestick data. It can also perform basic technical analysis.

**Typical User Intents**: "What's the price of BTC?", "Show me the order book for ETH/USDT.", "Get the 1-hour candlestick data for BNB.", "Calculate the 20-day moving average for ADA."

**Skill Boundaries**: This task primarily uses the `spot` and `derivatives-trading-usds-futures` skills to fetch market data. For complex analysis, it may need to be combined with other data analysis tools.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `spot` | To get real-time and historical market data for the spot market. |
| Primary | `derivatives-trading-usds-futures` | To get real-time and historical market data for the futures market. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Which trading pair is the user interested in? What time frame? What type of data (price, volume, etc.)?
- **If Unsolvable**: If the requested data is not available through the API, inform the user and suggest checking the Binance website.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Identify Trading Pair and Market** | Ask the user for the trading pair (e.g., BTC/USDT) and whether they are interested in the spot or futures market. |
| **2. Get Real-time Data** | Use the `spot` or `derivatives-trading-usds-futures` skills to get real-time data like the current price, 24-hour volume, and order book. |
| **3. Get Historical Data** | If the user wants historical data, use the klines (candlestick) endpoint. Specify the trading pair, interval (e.g., 1h, 1d), and time range. |
| **4. Perform Basic Analysis** | If the user requests it, perform basic technical analysis, such as calculating moving averages or RSI, based on the historical data. |
| **5. Present Data** | Present the data to the user in a clear and easy-to-understand format. For charts, you can describe the general trend or key levels. |

---

## Usage Guide

- **Specify the Market**: Always clarify whether the user is asking about the spot or futures market, as the data can differ.
- **Use Correct Symbols**: Ensure you are using the correct trading pair symbols (e.g., BTCUSDT, not BTC/USDT in the API call).
- **Data, Not Advice**: Present the data and analysis neutrally. Do not interpret the data as a buy or sell signal.
