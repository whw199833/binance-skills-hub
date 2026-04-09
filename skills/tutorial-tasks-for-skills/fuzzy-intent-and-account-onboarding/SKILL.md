---
name: fuzzy-intent-and-account-onboarding
description: |
  Vague “get started on Binance” intents: guide funding the account and a first trade end-to-end.
  Typical: “how do I start?”, “I want to buy crypto”, “what first?”.
  Boundaries: orchestrates fiat, assets, and spot; not financial advice; KYC or fiat problems → customer support.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-fuzzy-intent-and-account-onboarding
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/fuzzy-intent-and-account-onboarding/SKILL.md
license: MIT
---

# Fuzzy Intent and Account Onboarding Task

## Description

**Task Description**: This task is designed to handle vague user intents related to starting their crypto journey on Binance. It guides new users through the initial steps of funding their account and making their first trade.

**Typical User Intents**: "How do I start?", "I want to buy crypto.", "What should I do first?"

**Skill Boundaries**: This task orchestrates `assets`, `fiat`, and `spot` skills to facilitate the onboarding process. It does not provide financial advice.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `fiat` | For guiding users on how to deposit fiat currency. |
| Primary | `assets` | For checking balances and guiding transfers between wallets. |
| Primary | `spot` | For helping users make their first spot trade. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Is the user a new user? Have they completed KYC? Do they have any assets in their account?
- **If Unsolvable**: If the user is facing issues with KYC or fiat deposits, guide them to Binance customer support.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Welcome and Assess** | Welcome the user and ask a few questions to understand their level of experience and what they want to achieve. |
| **2. Guide Fiat Deposit** | Use the `fiat` skill to guide the user on how to deposit their local currency into their Binance account. |
| **3. Check Balance** | Use the `assets` skill to confirm that the fiat deposit has been credited to their account. |
| **4. Guide Transfer to Spot Wallet** | Use the `assets` skill to guide the user on how to transfer their funds from the Funding Wallet to the Spot Wallet. |
| **5. Guide First Spot Trade** | Use the `spot` skill to help the user make their first trade. Suggest a popular and relatively stable trading pair like BTC/USDT. |
| **6. Confirmation and Next Steps** | Confirm that the trade was successful and suggest next steps, such as exploring other Binance products or learning more about crypto. |

---

## Usage Guide

- **Be Patient and Encouraging**: New users can be overwhelmed. Be patient and provide clear, step-by-step instructions.
- **Focus on the Basics**: Don't overload the user with too much information. Focus on the essential steps of funding and trading.
- **No Financial Advice**: Explicitly state that you are not providing financial advice and that all investments carry risk.
