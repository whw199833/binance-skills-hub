---
name: simple-earn-and-vip-loan
description: |
  Simple Earn products and VIP Loan: available products, subscribe/redeem steps, and loan terms or collateral rules.
  Typical: subscribe to Simple Earn, USDT rates, VIP loan application, collateral requirements.
  Boundaries: simple-earn and vip-loan hub skills; rates and SKUs change—point users to the site for the latest.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-simple-earn-and-vip-loan
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/simple-earn-and-vip-loan/SKILL.md
license: MIT
---

# Simple Earn and VIP Loan Task

## Description

**Task Description**: This task helps users with inquiries related to Binance Simple Earn products and the VIP Loan program. It can provide information on available products, subscription/redemption procedures, and loan conditions.

**Typical User Intents**: "How do I subscribe to Simple Earn?", "What are the current interest rates for USDT in Simple Earn?", "How do I apply for a VIP loan?", "What are the collateral requirements for a VIP loan?"

**Skill Boundaries**: This task primarily uses the `simple-earn` and `vip-loan` skills.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `simple-earn` | For inquiries about Simple Earn products, subscriptions, and redemptions. |
| Primary | `vip-loan` | For inquiries about the VIP Loan program, application, and conditions. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Is the user asking about Simple Earn or VIP Loan? What specific information are they looking for?
- **If Unsolvable**: If the requested information is not available through the skills, guide the user to the relevant pages on the Binance website or suggest they contact customer support for specific account-related issues.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Differentiate Product** | Determine if the user's query is about Simple Earn or VIP Loan. |
| **2. Simple Earn Inquiries** | If about Simple Earn, use the `simple-earn` skill to get information on product availability, interest rates, and how to subscribe or redeem. |
| **3. VIP Loan Inquiries** | If about VIP Loan, use the `vip-loan` skill to provide information on eligibility, collateral assets, interest rates, and the application process. |
| **4. Summarize Information** | Present the information clearly to the user. For processes like subscription or application, provide step-by-step guidance. |

---

## Usage Guide

- **Use the Right Skill**: Ensure you are using the correct skill (`simple-earn` or `vip-loan`) based on the user's query.
- **Check for Updates**: Interest rates and product availability can change. Inform the user that the information is subject to change and they should always check the Binance website for the latest details.
- **No Financial Advice**: As always, clarify that you are not providing financial advice.
