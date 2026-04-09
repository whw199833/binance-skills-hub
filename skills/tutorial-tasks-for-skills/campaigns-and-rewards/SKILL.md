---
name: campaigns-and-rewards
description: |
  Discover campaigns, explain rules and requirements, reason about eligibility/participation at a high level, and answer reward-distribution questions using public info and balances.
  Typical: new campaigns, rule checks, participation status questions, when rewards arrive.
  Boundaries: web_search plus assets for possible reward tokens; does not drive a campaign participation API—official announcements are source of truth.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-campaigns-and-rewards
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/campaigns-and-rewards/SKILL.md
license: MIT
---

# Campaigns and Rewards Task

## Description

**Task Description**: Helps users discover ongoing Binance campaigns, understand the rules and requirements, check their eligibility and participation status, and inquire about reward distribution.

**Typical User Intents**: Finding new campaigns; checking campaign rules; verifying participation in a campaign; asking about when rewards will be distributed.

**Skill Boundaries**: This task will primarily use `web_search` to find information on the Binance website and `assets` to check for reward distribution. It does not directly interact with a campaign participation system.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `web_search` | To find information about current campaigns, rules, and announcements on the Binance website. |
| Auxiliary | `assets` | To check the user's asset balance for new tokens, which might be rewards from a campaign. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: What specific campaign is the user interested in? Are they looking for new campaigns or checking the status of one they participated in?
- **If Unsolvable**: If campaign details cannot be found, inform the user that information is not available and suggest they check the official Binance announcements page. For reward issues, if no new assets are found, advise them to contact Binance support with their participation details.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Discover Campaigns** | If the user is looking for new campaigns, use `web_search` with queries like "Binance new campaigns" or "Binance Launchpool". |
| **2. Get Campaign Details** | For a specific campaign, use `web_search` to find the announcement page, which contains the rules, participation period, and reward structure. |
| **3. Check Participation** | This task cannot directly check participation. Inform the user that they need to verify their participation on the campaign page on the Binance website. |
| **4. Check Rewards** | Ask the user for the reward token and the approximate distribution date. Use the `assets` skill to check their wallet balance for the reward token around the specified time. |
| **5. Summarize** | Provide the user with the information found, including links to the campaign announcements and the results of the asset check. |

---

## Usage Guide

- **Official Sources**: Always rely on the official Binance website and announcements for campaign information. Do not trust third-party sources.
- **No Guarantees**: Do not guarantee that a user will receive rewards. Participation does not always equal rewards.
- **Reward Timing**: Reward distribution can take time. Advise the user to be patient and check their asset balance periodically after the campaign ends.
