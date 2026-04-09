---
name: api-authorization-and-debugging
description: |
  API Key creation, permission scopes, HMAC/RSA/Ed25519 signing, IP whitelist setup, and debugging for clients (e.g. Postman) and code (Python/Node), including binance-connector issues.
  Typical: permission requests, key security, signature errors, IP whitelist, sample clients, connector usage.
  Boundaries: signing debug via binance (sign.sh); out-of-scope code issues → binance-connector-python or binance-connector-node on GitHub.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-api-authorization-and-debugging
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/api-authorization-and-debugging/SKILL.md
license: MIT
---

# API Authorization and Debugging Task

## Description

**Task Description**: Handles user inquiries regarding API Key creation, permission configuration, signing algorithms (HMAC/RSA/Ed25519), IP whitelist settings, debugging for clients (like Postman) and code (like Python/Node.js), and issues related to `binance-connector`.

**Typical User Intents**: API permission requests; API Key security and management; signing algorithm and error debugging; IP whitelist configuration; client and code examples; `binance-connector` usage consultation.

**Skill Boundaries**: Signing debugging primarily uses the `binance` Skill (providing `sign.sh` examples). If code-level debugging is out of scope, guide the user to the official GitHub repositories: `binance/binance-connector-python` or `binance/binance-connector-node`.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `binance` | Provides `sign.sh` script for HMAC/RSA/Ed25519 signature verification and debugging. |
| Auxiliary | `web_search` | To find Postman configurations or code examples for Binance API clients in specific languages (Python/Node.js). |
| Connecting | `sub-account` | If the API Key is for a sub-account, check the sub-account's API permissions. |

---

## Plan

> Aligns with `Task_upgrade_advice` §5: Determine Key type → Check permissions → Verify signature → Check IP & client → Summarize.

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Is the API Key for a main or sub-account? Is the signing algorithm HMAC, RSA, or Ed25519? Is the issue about permissions, signature, or client configuration?
- **If Unsolvable**: For persistent signature errors, guide the user to self-diagnose using the `binance` Skill's `sign.sh`. For code-level issues, direct them to the official GitHub repos. For security issues (Key leak), immediately advise the user to delete and recreate the Key.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **Key Type** | Confirm the API Key's ownership (main/sub-account) and signing algorithm (HMAC/RSA/Ed25519). If it's for a sub-account, use `sub-account` skill to check its API permissions. |
| **Permission Check** | Based on the endpoint the user wants to access (e.g., `/sapi/v1/capital/config/getall`), verify if the Key has the corresponding permission enabled (e.g., "Enable Universal Transfer"). |
| **Signature Verification** | **Core Step**: Use the `binance` Skill's `sign.sh` script. Pass the query string to be signed and compare the output with the user's generated `signature` to identify the problem. |
| **IP & Client** | Check the IP whitelist configuration. For Postman, advise checking environment/variable settings. For code, recommend using the official `binance-connector`. |
| **Code Examples** | Use `web_search` to find `binance-connector-python example` or `binance api postman collection` and provide the reference links. |
| **Summarize** | Summarize the debugging steps and conclusion. If the Key is compromised, **advise the user to delete and recreate it with the highest priority**. |

### B. API-Level Quick Reference

This task does not directly call Binance API endpoints but assists in debugging using scripts and external knowledge. The core is the signing script provided by the `binance` skill.

1. **Signing Script (`binance` Skill)**
   - **Path**: `binance-skills-hub/skills/binance/binance/scripts/sign.sh`
   - **Usage**:
     ```bash
     # HMAC-SHA256
     bash sign.sh "symbol=BNBUSDT&side=SELL&type=LIMIT&quantity=1&price=500&timeInForce=GTC" "$SECRET_KEY"
     ```
   - **Purpose**: To provide a standard, reproducible way of generating a signature to compare against the user's result, quickly identifying if the issue is with the query string construction, the `secretKey`, or the signing logic itself.

2. **Sub-account API Permissions (`sub-account` Skill)**
   - `GET /sapi/v1/sub-account/list`: Check if the sub-account exists.
   - `GET /sapi/v2/sub-account/info`: Check detailed information for a specific sub-account.
   - `GET /sapi/v1/sub-account/apiRestrictions`: Get API permission details for a sub-account.

---

## Usage Guide

- **Security First**: Never ask the user to send their `secretKey` or private key in plain text. Debugging should be done by comparing signature results or guiding the user to run `sign.sh` locally.
- **Isolate Variables**: Remind users to store `apiKey` and `secretKey` as variables in Postman or their code, rather than hardcoding them, to prevent accidental leaks.
- **Prioritize Official `binance-connector`**: For code implementations, prioritize recommending `binance/binance-connector-python` or `binance/binance-connector-node`, as they handle the complexities of signing and connection management.
