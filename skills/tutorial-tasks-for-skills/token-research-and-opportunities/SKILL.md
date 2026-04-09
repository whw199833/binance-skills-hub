---
name: token-research-and-opportunities
description: |
  Research tokens and projects, surface potential opportunities, and summarize market trends from public information.
  Typical: project fundamentals, new listings, sector narratives (e.g. DeFi, AI tokens).
  Boundaries: heavy use of web_search; not financial advice—always include disclaimer and encourage DYOR.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-token-research-and-opportunities
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/token-research-and-opportunities/SKILL.md
license: MIT
---

# Token Research and Opportunities Task

## Description

**Task Description**: This task helps users research new and existing tokens, discover potential investment opportunities, and stay updated on market trends.

**Typical User Intents**: "Tell me about the Solana project.", "What are some new tokens listed on Binance?", "Find promising projects in the DeFi space.", "What is the narrative around AI tokens?"

**Skill Boundaries**: This task heavily relies on `web_search` to gather information from various sources. It does not provide financial advice, and all information should be presented with a disclaimer.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `web_search` | To research tokens, projects, and market trends from sources like CoinMarketCap, CoinGecko, Messari, and project websites. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Which token or market sector is the user interested in? Are they looking for fundamental analysis, price data, or news?
- **If Unsolvable**: If information is scarce or unreliable, inform the user. Always be cautious about providing information on low-cap or obscure tokens.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Research the Token/Project** | Use `web_search` to find the project's official website, whitepaper, and pages on CoinMarketCap or CoinGecko. |
| **2. Gather Key Metrics** | From the search results, extract key information such as the token's purpose, technology, team, market cap, circulating supply, and recent price action. |
| **3. Analyze Market Narrative** | Use `web_search` to find news articles, analyst opinions, and social media sentiment related to the token or its market sector. |
| **4. Summarize Findings** | Synthesize the gathered information into a concise summary for the user. Present both the potential strengths and weaknesses/risks of the project. |
| **5. Disclaimer** | Always end with a disclaimer that this is not financial advice and the user should do their own research (DYOR). |

---

## Usage Guide

- **DYOR is Paramount**: Always emphasize the importance of "Do Your Own Research." The goal is to provide a starting point for the user's own investigation, not to make a recommendation.
- **Multiple Sources**: Use multiple reputable sources to cross-verify information and get a balanced view.
- **Risk Assessment**: When summarizing, always include potential risks associated with the token or project.
