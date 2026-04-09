---
name: onchain-signals-and-security
description: |
  On-chain data analysis and security Q&A: track addresses, explore large movements (whale-style context), and summarize wallet security best practices using public sources.
  Typical: “track this address”, large USDT movements, how to secure a wallet.
  Boundaries: web_search to explorers and guides; not real-time push alerts.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-onchain-signals-and-security
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/onchain-signals-and-security/SKILL.md
license: MIT
---

# Onchain Signals and Security Task

## Description

**Task Description**: This task helps users with on-chain data analysis and security-related inquiries. It can be used to track wallet addresses, monitor for large transactions (whale alerts), and provide information on security best practices.

**Typical User Intents**: "Track this Bitcoin address.", "Alert me when there are large movements of USDT.", "How can I secure my crypto wallet?"

**Skill Boundaries**: This task primarily uses `web_search` to query blockchain explorers and security resources. It does not provide real-time, push-based alerts.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `web_search` | To query blockchain explorers (like Etherscan, BscScan) and find security guides. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: What blockchain is the user interested in? What is the specific address or transaction hash? What security topic are they asking about?
- **If Unsolvable**: If the information cannot be found on a public blockchain explorer, inform the user. For security advice, always refer to official sources and recommend professional security audits for complex situations.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Identify Blockchain and Target** | Ask the user for the blockchain (e.g., Ethereum, BNB Smart Chain) and the specific address, transaction hash, or type of on-chain event they are interested in. |
| **2. Formulate Search Query** | Construct a search query for a public blockchain explorer. For example, "Etherscan address [address]" or "BscScan transaction [tx_hash]". |
| **3. Execute Web Search** | Use the `web_search` skill to get the data from the blockchain explorer. |
| **4. Extract and Present Data** | Extract the relevant information from the search results, such as the balance of an address, the details of a transaction, or a list of recent large transactions. |
| **5. Provide Security Information** | For security questions, use `web_search` to find articles on topics like wallet security, phishing prevention, and common scams. Summarize the key points and provide links. |

---

## Usage Guide

- **Use Reputable Explorers**: Always use well-known and reputable blockchain explorers to ensure the data is accurate.
- **Privacy and Security**: Remind users not to share their private keys or seed phrases. When discussing addresses, clarify that all information is public on the blockchain.
- **Not Real-time Alerts**: Inform users that this task provides on-demand information and does not support real-time, push-based alerts for on-chain events.
