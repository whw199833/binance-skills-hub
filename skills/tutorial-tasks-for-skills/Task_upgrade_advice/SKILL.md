---
name: Task_upgrade_advice
description: |
  Aggregates default structured pipelines (Plan section A) referenced across tutorial tasks; exact HTTP paths and parameters follow each task section B and matching SKILL.md in binance-skills-hub.
  Cross-task pre-planning: before any plan or trade/product advice, confirm balances and available funds, open and in-flight orders (algo, grids, conditional), and earn/loan locks or transfer prerequisites; if tools cannot, disclose gaps and avoid executable trade paths from assumptions.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-Task_upgrade_advice
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/Task_upgrade_advice/SKILL.md
license: MIT
---

# Task upgrade advice — default execution DAG (overview)

This document aggregates the **default structured pipelines** referenced in each Task **Plan §A**. Concrete HTTP paths and parameters follow each Task **§B** and the matching `SKILL.md` in `binance-skills-hub`.

---

## Pre-planning: confirm account state (cross-task)

Before **planning** a user task (execution plan or trading/product advice), the agent **should first** confirm current account state, then decide whether the request is supportable or actionable:

- **Balances and available funds**: Available balance and margin usage for the relevant market/account type (futures, leverage, unified account, etc.); avoid pushing order plans when funds are insufficient or assets are mismatched.
- **Open and in-flight orders**: Open orders, algo orders, grids, conditional orders, etc.; avoid conflicts with existing positions or duplicate orders.
- **Other relevant state**: Earn/loan locks, freezes, sub-account and transfer prerequisites; link to [account-and-asset-management.cn.md](./account-and-asset-management.cn.md) and each Task §A when needed.

If tools cannot fetch the above, **tell the user what is missing** or ask them to self-check before giving a plan; **do not** propose executable trade paths from price alone or assumed balances.

### When state is unknown or insufficient: suggested user dialog

1. **Explain**: Briefly state known facts and gaps (e.g. insufficient balance, market type unclear, API permission missing, campaign metrics may differ).
2. **Ask**: Offer options or confirmations (deposited/transferred?, cancel an order?, provide order id/symbol/time range?, verify campaign progress or API rights in the app?).
3. **Hold line**: Until the user supplements or self-checks, **do not advance** irreversible actions (orders, transfers, subscriptions, borrows, on-chain pay). You may give **conditional** guidance (“if balance is X and there is no conflicting open order, then …”).

Each Task **Plan** adds intent-specific detail; the table below is the default pipeline summary.

---

| § | Task / theme | Default pipeline (summary) |
|---|----------------|---------------------------|
| **1** | [account-and-asset-management.cn.md](./account-and-asset-management.cn.md) | Scope → balance snapshot → deposit/withdraw/transfer alignment → sub-account/fiat branches → consolidated output. |
| **2** | [api-authorization-and-debugging.cn.md](./api-authorization-and-debugging.cn.md) | Classify error → permission truth → per-market read path → sub-account/IP → signing environment → supply-chain tools (`skill-vetter` / `healthcheck`). |
| **3** | [trading-execution.cn.md](./trading-execution.cn.md) | **Single** market lock → read-only orders/positions → precision/rules before writes → algo sub-order tracking; market data from [market-data-and-analysis.cn.md](./market-data-and-analysis.cn.md). Spot/convert/USDS-M may cross-check **`binance`** (`binance-cli`, see that Task §C). |
| **4** | [market-data-and-analysis.cn.md](./market-data-and-analysis.cn.md) | Broad to narrow: rankings → Top N → `meta` + `dynamic` → 1–3 symbols’ klines → optional inflow/smart money; RWA separate. Scheduled pulls: that file **§B.C** (Python / Shell). |
| **5** | [onchain-signals-and-security.cn.md](./onchain-signals-and-security.cn.md) | **If contract address: audit first** → signals → liquidity check → address paging; meme narrative may align. Scheduled monitoring: **§B.C** (Python / Shell). |
| **6** | [token-research-and-opportunities.cn.md](./token-research-and-opportunities.cn.md) | Locate → risk (audit) → market position → behavior/narrative → RWA separate; orders → [trading-execution.cn.md](./trading-execution.cn.md). |
| **7** | [product-help-and-order-lookup.cn.md](./product-help-and-order-lookup.cn.md) | FAQ first, APIs second; read-only order lookup only for “my order/grid”; confirm spot/futures/algo first. |
| **8** | [token-deployment-and-onchain-pay.cn.md](./token-deployment-and-onchain-pay.cn.md) | No one-click deploy REST; pay flow: pairs → payment → quote → address/network → pre-order → poll; after deploy: search + audit + address holdings. |
| **9** | [campaigns-and-rewards.cn.md](./campaigns-and-rewards.cn.md) | Rules per website → optional token market data → optional user self-check volume; discussion-only has no API. |
| **10** | [binance-square-posting.cn.md](./binance-square-posting.cn.md) | Draft finalize → optional market facts → single `content/add`; scheduled posts default **§B.C** (Python / Shell + cron). |
| **11** | [education-and-learning.cn.md](./education-and-learning.cn.md) | Concepts first → if user wants examples: search → dynamic → klines; reusable tutorials via `skill-creator`. |
| **12** | [simple-earn-and-vip-loan.cn.md](./simple-earn-and-vip-loan.cn.md) | Pick product line (Simple Earn / VIP Loan / margin) → list → positions → preview → subscribe/borrow → `getUserAsset` check. |

Cross-links: deeper assets → [account-and-asset-management.cn.md](./account-and-asset-management.cn.md); trading → [trading-execution.cn.md](./trading-execution.cn.md); market data → [market-data-and-analysis.cn.md](./market-data-and-analysis.cn.md).
