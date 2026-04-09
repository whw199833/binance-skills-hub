---
name: token-deployment-and-onchain-pay
description: |
  Token deployment on various chains and using Binance Pay (or on-chain pay flows) for crypto sends to addresses.
  Typical: create a BEP-20-style token, token standards, pay to an on-chain address.
  Boundaries: web_search for deployment guides; onchain-pay skill for Binance on-chain payment flows.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-token-deployment-and-onchain-pay
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/token-deployment-and-onchain-pay/SKILL.md
license: MIT
---

# Token Deployment and Onchain Pay Task

## Description

**Task Description**: This task assists users with inquiries related to deploying tokens on various blockchains and using Binance Pay for on-chain transactions.

**Typical User Intents**: "How do I create a token on BNB Smart Chain?", "What are the standards for creating a token?", "How do I use Binance Pay to send crypto to an on-chain address?"

**Skill Boundaries**: This task uses `web_search` to find guides on token deployment and the `onchain-pay` skill for Binance Pay inquiries.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `web_search` | To find tutorials and documentation on token creation and standards (e.g., ERC-20, BEP-20). |
| Primary | `onchain-pay` | For inquiries related to using Binance Pay for on-chain transactions. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Is the user asking about creating a token or using Binance Pay? Which blockchain are they interested in?
- **If Unsolvable**: For complex token development questions, guide the user to developer communities and official blockchain documentation. For Binance Pay issues, if the skill cannot resolve them, suggest contacting Binance support.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Token Deployment Guidance** | If the user wants to create a token, use `web_search` to find guides and tutorials for the specified blockchain (e.g., "how to create BEP-20 token"). Provide links to these resources. |
| **2. Onchain Pay Guidance** | If the user is asking about Binance Pay, use the `onchain-pay` skill to explain how to use it for on-chain transfers, including how to select the network and enter the address. |
| **3. Summarize and Clarify** | Summarize the steps for either process. For token deployment, emphasize the need for technical knowledge and careful testing. For onchain pay, remind the user to double-check the address and network. |

---

## Usage Guide

- **Token Deployment is Complex**: Make it clear to the user that creating a token is a technical process that requires coding knowledge. The resources provided are for guidance only.
- **Security for Onchain Pay**: When guiding users on onchain pay, stress the importance of verifying the recipient's address and selecting the correct blockchain network to avoid loss of funds.
- **Use Official Documentation**: For both token standards and Binance Pay, refer to the official documentation from the respective blockchains and Binance.
