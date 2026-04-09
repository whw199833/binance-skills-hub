---
name: trading-execution
description: |
  Spot, convert, algo, margin, futures, and options: place, amend/cancel, and query orders; take-profit/stop-loss, grids, and automated trading; data-side support from market data and order state when advising on strategy.
  Typical: quant/short-term strategies, auto-trading and clearing orders, futures entries, TP/SL, grids, order status, directional execution.
  Boundaries: compliant “investment” wording; orders must use the skill for the real product (spot ≠ futures ≠ options); execution via REST quick refs or binance-cli (binance skill) when installed.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-trading-execution
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/trading-execution/SKILL.md
license: MIT
---

# Trading execution task

## Description

**Task summary**: Covers spot / convert / algo / margin / futures / options intents: place, amend/cancel, query orders, take-profit/stop-loss, grids, and automated trading; includes **data-side** support for strategy advice (market data, order state) and skill selection along the execution path.

**Typical intents**: Quant/short-term strategies; auto-trading and clearing orders; BNB futures entries and strategy; TP/SL; grid trading and order monitoring; DOGE/FDUSD grids; order status queries; long BTC execution, etc.

**Skill boundaries**: “Investment advice” must stay compliant; real orders must use the skill for the **actual product** (spot ≠ futures ≠ options). **Execution path**: same market can use **REST** (per-product `SKILL.md` quick reference) or, when `binance-cli` is installed, the **`binance`** skill (`spot` / `convert` / `futures-usds` subcommands, cross-checked with spot, convert, USDS-M REST).

---

## Recommended skill mix

| Scenario | Primary skill | Secondary |
|----------|---------------|-----------|
| Spot / convert / USDS-M (**CLI**) | `binance` (`binance-cli`) | Cross-check with `spot` / `convert` / `derivatives-trading-usds-futures`—pick one or verify |
| Spot trade, cancel, query | `spot` | `convert` (quick swap) |
| Convert | `convert` | `query-token-info` (pair sanity check) |
| TWAP and other algo orders | `algo` | `spot` or the relevant derivative market |
| USDS-M perp/delivery | `derivatives-trading-usds-futures` | `algo` (if supported on that market) |
| COIN-M perp/delivery | `derivatives-trading-coin-futures` | same as above |
| Options | `derivatives-trading-options` | `query-token-info` |
| Unified portfolio margin | `derivatives-trading-portfolio-margin` / `derivatives-trading-portfolio-margin-pro` | `assets` |
| Cross/isolated margin spot | `margin-trading` | `spot` |
| P2P quotes and order history | `p2p` | — |

---

## Plan

**Step 0: Prerequisite state check — *MANDATORY***

> **Goal**: Before concrete actions, understand the user’s full state for safer, personalized guidance.  
> **Core skills**: `assets`, `spot` (for `getOrders`), `derivatives-trading-usds-futures` (for `getPositions`)

1. **Account assets**: `assets.getUserAssets` across wallets (especially spot `SPOT` and funding `FUNDING`).
2. **Open positions**: `derivatives-trading-usds-futures.getPositions` for USDS-M direction, size, unrealized PnL.
3. **Recent activity and open orders**: `spot.getOrders` for habits (preferred pairs) and open orders.

> **After diagnosis**: Adjust next steps; if related exposure exists, center the plan on it; if underfunded, see **`fuzzy-intent-and-account-onboarding.cn.md`** for funding.

---

> Aligns with `Task_upgrade_advice.cn.md` §3: **single market lock** → read-only orders/positions → precision/rules before writes → algo sub-order tracking; market data from `market-data-and-analysis.cn.md`—do not substitute order APIs for prices.

### Status checks and when you cannot proceed

- **Before writes** (required): **single market** locked; **available balance** and **margin** (derivatives/margin); **open orders and positions** (incl. algo, grids); avoid clashes with in-flight orders.
- **If under-margined, missing params**: (1) State gap and quantified ceiling (e.g. max buy size); (2) Ask about deposit/transfer, cancel/reduce, smaller size or leverage change; (3) **Do not** place orders or confirm convert on the user’s behalf until confirmed.
- **Cross-task rules**: [Task_upgrade_advice.cn.md](./Task_upgrade_advice.cn.md) opening section.

### A. Structured pipeline (DAG)

| Step | Action |
|------|--------|
| **Market lock** | Map to one skill: `spot` / `convert` / `algo` / `fapi` / `dapi` / `eapi` / `papi` / `margin` / `p2p` (quotes only); **never** mix `fapi` and `dapi` in one flow. With CLI: `binance-cli spot` \| `convert` \| `futures-usds` maps 1:1 (see §C). |
| **Read-only** | `openOrders` → `order` (by id) → futures `positionRisk`; CLI e.g. `get-open-orders`, `query-order`, `position-information-v-3`; cancel/amend only after confirmation. |
| **Writes** | Spot: `exchangeInfo`/`myFilters` then `order`; futures: `leverage`/`marginType` if needed; convert: `exchangeInfo` → `getQuote` → confirm → `acceptQuote`. CLI: §C; **production trades require user `CONFIRM`** (`binance` SKILL). |
| **Algo orders** | After place: `algo/*/openOrders` + `subOrders` for child progress. |
| **Market data** | Prices/rankings from `market-data-and-analysis.cn.md`. |

### B. REST endpoint quick reference

**Bases**: Spot/Convert/Algo/Margin/SAPI → `https://api.binance.com`; USDS-M → `https://fapi.binance.com`; COIN-M → `https://dapi.binance.com`; Options → `https://eapi.binance.com` (per SKILL).

1. **Spot (`spot`)**
   - Place: `POST /api/v3/order` (`symbol`, `side`, `type`, `quantity`/`quoteOrderQty`, `price`, `timeInForce`, etc.).
   - Cancel: `DELETE /api/v3/order`; cancel all: `DELETE /api/v3/openOrders`.
   - Query: `GET /api/v3/order`, `GET /api/v3/openOrders`, `GET /api/v3/allOrders`.
   - Conditional/OCO: see SKILL `/api/v3/orderList/*`, `/api/v3/order/oco`, etc.

2. **Convert (`convert`)**
   - Pairs: `GET /sapi/v1/convert/exchangeInfo`.
   - Quote: `POST /sapi/v1/convert/getQuote` (`fromAsset`, `toAsset`, `fromAmount`/`toAmount`).
   - Accept: `POST /sapi/v1/convert/acceptQuote` (`quoteId`).
   - Limit: `POST /sapi/v1/convert/limit/placeOrder`; status: `GET /sapi/v1/convert/orderStatus`, `GET /sapi/v1/convert/limit/queryOpenOrders`.

3. **Algo TWAP/VP (`algo`)**
   - Futures: `POST /sapi/v1/algo/futures/newOrderTwap`, `POST /sapi/v1/algo/futures/newOrderVp`; open: `GET /sapi/v1/algo/futures/openOrders`; children: `GET /sapi/v1/algo/futures/subOrders?algoId=`.
   - Spot TWAP: `POST /sapi/v1/algo/spot/newOrderTwap`; open: `GET /sapi/v1/algo/spot/openOrders`.

4. **USDS-M (`derivatives-trading-usds-futures`)**
   - Order: `POST /fapi/v1/order`; cancel: `DELETE /fapi/v1/order`; batch: `POST /fapi/v1/batchOrders`.
   - Positions: `GET /fapi/v2/positionRisk`; balance: `GET /fapi/v2/balance`.
   - Conditional/algo: `POST /fapi/v1/algoOrder`, `GET /fapi/v1/openAlgoOrders`.

5. **COIN-M (`derivatives-trading-coin-futures`)**
   - `POST /dapi/v1/order`, `GET /dapi/v1/openOrders`, `GET /dapi/v1/positionRisk`, etc. (often `pair`/`symbol`).

6. **Options (`derivatives-trading-options`)**
   - `POST /eapi/v1/order`, `GET /eapi/v1/openOrders`, `GET /eapi/v1/position`, `DELETE /eapi/v1/allOpenOrders`.

7. **PM (`derivatives-trading-portfolio-margin`)**
   - Account and orders: `GET /papi/v1/account`, `GET /papi/v2/um/account`, `POST /papi/v1/um/order`, `POST /papi/v1/cm/order`, etc. (see SKILL quick reference).

8. **Margin spot (`margin-trading`)**
   - `POST /sapi/v1/margin/order` (`isIsolated`, `sideEffectType`, etc.); open: `GET /sapi/v1/margin/openOrders`.

9. **P2P quotes and history (`p2p`)**
   - Public: `GET https://www.binance.com/bapi/c2c/v1/public/c2c/agent/quote-price` (`fiat`, `asset`, `tradeType`); `.../ad-list`; `.../trade-methods`.
   - Private: `GET /sapi/v1/c2c/orderMatch/listUserOrderHistory`, `GET /sapi/v1/c2c/orderMatch/getUserOrderSummary` (signed; **do not sort** SAPI params).

### C. `binance-cli` (`binance` skill, vs §B)

`binance-skills-hub/skills/binance/binance/SKILL.md`: **`binance-cli`** needs `BINANCE_API_KEY`, `BINANCE_API_SECRET`; optional `BINANCE_API_ENV`. Common spot, convert, USDS-M flows are **REST-equivalent** to §B §§1, 2, 4—agent picks **REST skill** or **CLI**, or read-only cross-check.

| Subcommand | REST skill | Hub reference |
|------------|------------|---------------|
| `binance-cli spot <endpoint>` | `spot` | `references/spot.md` (e.g. `get-account`, `get-open-orders`, `new-order`, `get-order`, `delete-order`) |
| `binance-cli convert <endpoint>` | `convert` | `references/convert.md` (e.g. `list-all-convert-pairs`, `send-quote-request`, `accept-quote`, `order-status`) |
| `binance-cli futures-usds <endpoint>` | `derivatives-trading-usds-futures` | `references/futures-usds.md` (e.g. `position-information-v-3`, `current-all-open-orders`, `new-order`, `query-order`) |

- **Install**: `metadata.openclaw.install` → `@binance/binance-cli` (see `binance` SKILL); **profiles**: `binance-cli profile create` / `change`; add `--profile <name>` to any command.
- **Safety**: Production execution requires user **`CONFIRM`**; `--recvWindow`, Unix ms timestamps match REST; details in `references/auth.md`.
- **CLI gaps**: `algo`, `p2p`, `margin-trading`, COIN-M, options, PM—use **REST** `SKILL.md` only (§B).

---

## Usage guide

### Structure

- **One intent, one market chain**; changing market means re-picking the skill.
- **Read before write** except convert instant fill—confirm orders/positions before amending.

### Conventions

- **`newClientOrderId` (spot)**: SKILL requires `agent-` prefix (auto-prefixed if omitted).
- **USDS vs COIN**: do not mix `fapi` and `dapi`; options use `eapi`.
- **convert vs spot**: one-tap quote+fill → `convert/getQuote` + `acceptQuote`; limit book depth → `spot`.
- **With `market-data-and-analysis.cn.md`**: on-chain/aggregated feeds use Web3 BAPI (see that doc); this task is exchange order APIs.
- **`binance` vs REST**: Follow what the deployment enables; **do not** double-submit the same trade on CLI and REST (read-only cross-check is OK).
