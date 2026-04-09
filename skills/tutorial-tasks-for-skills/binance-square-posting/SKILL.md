---
name: binance-square-posting
description: |
  Create and post Binance Square content (text, images, links), check post status, and share guidelines and best practices.
  Typical: new post, post status, content rules, engagement tips.
  Boundaries: square-post as primary; optional web_search for topics; heavier content generation may use other creative skills.
metadata:
  version: 1.0.0
  author: Binance
  openclaw:
    skillKey: tutorial-binance-square-posting
    homepage: https://github.com/binance/binance-skills-hub/tree/main/skills/tutorial-tasks-for-skills/binance-square-posting/SKILL.md
license: MIT
---

# Binance Square Posting Task

## Description

**Task Description**: Assists users in creating and posting content on Binance Square, including text, images, and links. It also helps with checking the status of posted content and provides guidance on content guidelines and best practices.

**Typical User Intents**: Creating a new post on Binance Square; checking the status of a post; understanding content guidelines; getting tips for better engagement.

**Skill Boundaries**: This task primarily uses the `square-post` skill. For complex content creation (e.g., generating images or detailed articles), it may connect to other content generation skills.

---

## Recommended Skills Combination

| Role | Skill | Purpose |
|------|--------|------|
| Primary | `square-post` | For creating and managing posts on Binance Square. |
| Auxiliary | `web_search` | To research trending topics or find inspiration for content. |

---

## Plan

### Status Check and Communication for Unsupported Cases

- **Pre-planning Checks**: Does the user have content ready to post? Are they asking for content creation assistance? Is the query about post status or guidelines?
- **If Unsolvable**: If the `square-post` skill fails, guide the user to check their Binance account permissions or the Binance Square platform status. For content policy violations, advise them to review the official Binance Square content guidelines.

### A. Structured Pipeline (DAG)

| Step | Action |
|------|------|
| **1. Content Gathering** | Ask the user for the content they want to post. If they need help creating content, move to the content generation step. |
| **2. Content Generation** | (Optional) If the user needs content, use `web_search` to find relevant information or ideas. For text-based content, you can help draft a post. |
| **3. Posting** | Use the `square-post` skill to post the content to Binance Square. Handle any options like adding images or links. |
| **4. Status Check** | After posting, use the `square-post` skill to check the status of the post and confirm it's live. |
| **5. Guidance** | If the user asks for tips, provide best practices for Binance Square, such as using relevant hashtags, engaging with comments, and posting consistently. |

---

## Usage Guide

- **Content First**: Ensure you have the content from the user before attempting to post.
- **Authentication**: The `square-post` skill requires authentication. Ensure the user has linked their Binance account.
- **Content Guidelines**: Remind users to adhere to Binance Square's content policies to avoid their posts being removed.
