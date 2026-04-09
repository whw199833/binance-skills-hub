---
name: product-help-and-order-lookup
description: |
  Explain Binance products and help users look up order or cash-movement status (e.g. withdrawals) with the right APIs.
  Typical: how Earn works, futures fees, where a spot order is, withdrawal status.
  Boundaries: web_search for help articles; spot, derivatives-trading-usds-futures, and assets for order/transfer lookups as applicable.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-product-help-and-order-lookup
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/product-help-and-order-lookup/SKILL.md
license: MIT
---

# Product Help and Order Lookup Task

## Description

**Task Description**: This task assists users by providing information about various Binance products and helping them look up the status of their orders.

**Typical User Intents**: "How does Binance Earn work?", "What are the fees for futures trading?", "Where is my spot order?", "Can you check the status of my withdrawal?"

**Skill Boundaries**: This task uses `web_search` to find help articles and `spot`, `derivatives-trading-usds-futures`, and `assets` to look up order and transaction statuses.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `web_search` | To find help articles and documentation about Binance products. |
| Primary | `spot` | To look up spot orders. |
| Primary | `derivatives-trading-usds-futures` | To look up futures orders. |
| Primary | `assets` | To check the status of deposits and withdrawals. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Which Binance product is the user asking about? Do they have an order ID or transaction ID for lookup?
- **If Unsolvable**: If an order cannot be found, ask the user to double-check the order ID and the trading pair. If the information is not available via the API, guide them to check their order history on the Binance website or app.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Product Information** | If the user is asking about a Binance product, use `web_search` to find the relevant help articles on the Binance support website. Summarize the information and provide the link. |
| **2. Spot Order Lookup** | If the user wants to check a spot order, ask for the trading pair and order ID. Use the `spot` skill to get the order status. |
| **3. Futures Order Lookup** | For futures orders, use the `derivatives-trading-usds-futures` skill, again asking for the trading pair and order ID. |
| **4. Deposit/Withdrawal Lookup** | For deposits and withdrawals, use the `assets` skill. You might need the coin, transaction ID (TxID), and the network. |
| **5. Present Status** | Clearly present the status of the order or transaction to the user. |

---

## Usage Guide

- **Order ID is Key**: For order lookups, the order ID is the most important piece of information. Prompt the user for it if they don't provide it.
- **Distinguish Between Order Types**: Be aware of the different types of orders (spot, futures, etc.) and use the correct skill to look them up.
- **Refer to Official Docs**: For product help, always prioritize and refer to the official Binance documentation and support articles.
