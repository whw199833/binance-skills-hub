---
name: tutorial-tasks-for-skills
description: |
  Bundles the Tutorial-Tasks-for-2C corpus as one installable skill: task playbooks, Task upgrade advice, and intent taxonomy (README, intent_category.json, linked .cn.md sources).
  For classifying user messages, following each task Plan (section A DAG, section B endpoints) against skills under skills/binance and skills/binance-web3; begin with Task_upgrade_advice for global pre-planning and default DAG overview.
metadata:
  version: 1.0.0
  author: Tutorial-Tasks-for-2C
  source_repo: Tutorial-Tasks-for-2C
license: MIT
---

# Tutorial Tasks for 2C (skill bundle)

This folder packages the **Tutorial-Tasks-for-2C** corpus as a **single installable skill**: Task docs, upgrade advice, and intent taxonomy live alongside this file.

## When to use

- Classify a user message and pick **which Task file** applies.
- Follow **Plan → section A (DAG)** in that Task, then **section B** for endpoints; cross-check with the matching skill under `skills/binance/` or `skills/binance-web3/`.
- Start from **[`Task_upgrade_advice.cn.md`](./Task_upgrade_advice.cn.md)** (or [`Task_upgrade_advice/SKILL.md`](./Task_upgrade_advice/SKILL.md)) for the global default DAG and **pre-planning** account checks.

## Entry points

| File | Role |
|------|------|
| [`README.md`](./README.md) | Full index: intent → Task file → core skills; how to read the docs. |
| [`intent_category.json`](./intent_category.json) | Intent categories and example queries. |
| [`Task_upgrade_advice.cn.md`](./Task_upgrade_advice.cn.md) | Cross-task default execution DAG (Chinese source). |
| [`Task_upgrade_advice.md`](./Task_upgrade_advice.md) | Cross-task advice (alternate variant if present). |
| `*.cn.md` | Per-intent Task sources: description, skills, section A DAG, section B API notes (Chinese). |

## Per-task source documents (Chinese `.cn.md`)

- [`account-and-asset-management.cn.md`](./account-and-asset-management.cn.md)
- [`api-authorization-and-debugging.cn.md`](./api-authorization-and-debugging.cn.md)
- [`trading-execution.cn.md`](./trading-execution.cn.md)
- [`market-data-and-analysis.cn.md`](./market-data-and-analysis.cn.md)
- [`onchain-signals-and-security.cn.md`](./onchain-signals-and-security.cn.md)
- [`token-research-and-opportunities.cn.md`](./token-research-and-opportunities.cn.md)
- [`product-help-and-order-lookup.cn.md`](./product-help-and-order-lookup.cn.md)
- [`token-deployment-and-onchain-pay.cn.md`](./token-deployment-and-onchain-pay.cn.md)
- [`campaigns-and-rewards.cn.md`](./campaigns-and-rewards.cn.md)
- [`binance-square-posting.cn.md`](./binance-square-posting.cn.md)
- [`education-and-learning.cn.md`](./education-and-learning.cn.md)
- [`simple-earn-and-vip-loan.cn.md`](./simple-earn-and-vip-loan.cn.md)
- [`fuzzy-intent-and-account-onboarding.cn.md`](./fuzzy-intent-and-account-onboarding.cn.md)

## Hub alignment

Skill **names** and REST details are defined in each **`SKILL.md`** under `skills/binance/*` and `skills/binance-web3/*`. The aggregate CLI entry is **`skills/binance/binance/SKILL.md`** (`binance-cli`: `spot`, `convert`, `futures-usds`).

## Compliance

Task text is **routing and capability** guidance only—not investment advice. Product rules and disclaimers on Binance official channels prevail.
