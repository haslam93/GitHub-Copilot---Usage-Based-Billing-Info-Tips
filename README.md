---
title: GitHub Copilot Usage-Based Billing Learning Guide
description: A practical guide for using GitHub Copilot intentionally as usage-based billing begins on June 1, 2026
author: Microsoft
ms.date: 2026-05-14
ms.topic: guide
keywords:
  - github copilot
  - usage-based billing
  - ai credits
  - developer productivity
estimated_reading_time: 12
---

## Learn to Use GitHub Copilot Smartly Under Usage-Based Billing

GitHub Copilot is moving from request-based billing to usage-based billing on
June 1, 2026. This repo is a compact learning kit for developers, team leads,
and billing owners who want to keep using Copilot effectively while understanding
how model choice, context size, agents, and budgets affect cost.

The goal is not to use Copilot less. The goal is to use Copilot with clearer
intent: choose the right mode, give the right context, verify output quickly, and
avoid expensive loops that do not improve the result.

Source docs:

* [Models and pricing for GitHub Copilot](https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing)
* [Usage-based billing for organizations and enterprises](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-organizations-and-enterprises)

> [!IMPORTANT]
> GitHub says the pricing and billing methods described in the referenced docs
> start on June 1, 2026. Review the live GitHub docs before making billing or
> procurement decisions, because model availability and pricing can change.

## What changes on June 1, 2026

GitHub Copilot Business and Copilot Enterprise usage is measured with GitHub AI
Credits. Copilot interactions consume tokens, including input tokens, output
tokens, and cached tokens. Each model has its own token price, and GitHub
converts the resulting usage into AI credits.

Key facts to remember:

* 1 GitHub AI Credit equals $0.01 USD.
* Copilot Business includes 1,900 AI credits per assigned user per month.
* Copilot Enterprise includes 3,900 AI credits per assigned user per month.
* Existing Business and Enterprise customers receive promotional monthly
  included credits from June 1 through September 1, 2026.
* Included AI credits are pooled at the billing entity level, not held in
  isolated buckets per user.
* Code completions and next edit suggestions are not billed in AI credits for
  paid plans and remain unlimited.
* Copilot Chat, Copilot CLI, Copilot cloud agent, Copilot Spaces, Spark, and
  third-party coding agents consume AI credits.
* After the pooled credits are exhausted, additional usage either continues at
  published rates or is blocked, depending on policy settings.
* User-level budgets can halt a user's Copilot access even when the broader
  organization still has pooled credits available.
* There is no automatic fallback to lower-cost models when a budget is exhausted.

## Included AI credits

| Plan | Standard AI credits per user per month | Promotional credits per user per month, June 1 to September 1, 2026 |
| --- | ---: | ---: |
| Copilot Business | 1,900 | 3,000 |
| Copilot Enterprise | 3,900 | 7,000 |

Example: an organization with 100 Copilot Business users receives a shared pool
of 190,000 standard AI credits per month. During the promotional period, that
same organization receives 300,000 AI credits per month.

## How model pricing works

All prices in the tables below are per 1 million tokens. These are the
usage-based billing rates GitHub lists for June 1, 2026.

A small prompt to a lightweight model can cost a fraction of a credit. A long
agent session using a frontier model across multiple files can cost more because
it consumes more input, output, and cached context.

### OpenAI models

| Model | Release status | Category | Input | Cached input | Output |
| --- | --- | --- | ---: | ---: | ---: |
| GPT-4.1 | GA | Versatile | $2.00 | $0.50 | $8.00 |
| GPT-5 mini | GA | Lightweight | $0.25 | $0.025 | $2.00 |
| GPT-5.2 | GA | Versatile | $1.75 | $0.175 | $14.00 |
| GPT-5.2-Codex | GA | Powerful | $1.75 | $0.175 | $14.00 |
| GPT-5.3-Codex | GA | Powerful | $1.75 | $0.175 | $14.00 |
| GPT-5.4 | GA | Versatile | $2.50 | $0.25 | $15.00 |
| GPT-5.4 mini | GA | Lightweight | $0.75 | $0.075 | $4.50 |
| GPT-5.4 nano | GA | Lightweight | $0.20 | $0.02 | $1.25 |
| GPT-5.5 | GA | Powerful | $5.00 | $0.50 | $30.00 |

GPT-4.1 and GPT-5 mini are included models. GPT-5.4 pricing applies to prompts
with 272K tokens or fewer.

### Anthropic models

Anthropic models include a cache write cost in addition to cached input.

| Model | Release status | Category | Input | Cached input | Cache write | Output |
| --- | --- | --- | ---: | ---: | ---: | ---: |
| Claude Haiku 4.5 | GA | Versatile | $1.00 | $0.10 | $1.25 | $5.00 |
| Claude Sonnet 4 | GA | Versatile | $3.00 | $0.30 | $3.75 | $15.00 |
| Claude Sonnet 4.5 | GA | Versatile | $3.00 | $0.30 | $3.75 | $15.00 |
| Claude Sonnet 4.6 | GA | Versatile | $3.00 | $0.30 | $3.75 | $15.00 |
| Claude Opus 4.5 | GA | Powerful | $5.00 | $0.50 | $6.25 | $25.00 |
| Claude Opus 4.6 | GA | Powerful | $5.00 | $0.50 | $6.25 | $25.00 |
| Claude Opus 4.7 | GA | Powerful | $5.00 | $0.50 | $6.25 | $25.00 |

### Google models

| Model | Release status | Category | Input | Cached input | Output |
| --- | --- | --- | ---: | ---: | ---: |
| Gemini 2.5 Pro | GA | Powerful | $1.25 | $0.125 | $10.00 |
| Gemini 3 Flash | Public preview | Lightweight | $0.50 | $0.05 | $3.00 |
| Gemini 3.1 Pro | Public preview | Powerful | $2.00 | $0.20 | $12.00 |

Gemini 2.5 Pro and Gemini 3.1 Pro pricing applies to prompts with 200K tokens or
fewer. Gemini 3 Flash has no long-context surcharge.

### xAI models

| Model | Release status | Category | Input | Cached input | Output |
| --- | --- | --- | ---: | ---: | ---: |
| Grok Code Fast 1 | GA | Lightweight | $0.20 | $0.02 | $1.50 |

### Fine-tuned GitHub models

| Model | Release status | Category | Input | Cached input | Output |
| --- | --- | --- | ---: | ---: | ---: |
| Raptor mini | Public preview | Versatile | $0.25 | $0.025 | $2.00 |
| Goldeneye | Public preview | Powerful | $1.25 | $0.125 | $10.00 |

Raptor mini uses GPT-5 mini pricing. Goldeneye uses GPT-5.1-Codex pricing.

## Smart Copilot habits

Start with the cheapest effective interaction. Ask a focused question, use a
lightweight model for routine work when available, and move to a more capable
model when the task needs deeper reasoning, larger context, or stronger code
review judgment.

Use this workflow:

1. Define the outcome in one or two sentences.
2. Attach or reference only the files needed for the task.
3. Ask Copilot to inspect before editing when the codebase is unfamiliar.
4. Prefer small implementation steps over one broad instruction.
5. Review diffs after each meaningful change.
6. Run targeted tests before asking for a larger verification pass.
7. Save repeated prompts as reusable instructions or prompt files.

## Cost-aware prompt patterns

Use specific prompts that reduce unnecessary context and retries:

```text
Inspect the files related to authentication routing and identify the smallest
change needed to fix the redirect loop. Do not edit files yet.
```

```text
Update only the validation function and its direct tests. Keep the public API
unchanged and explain any behavior that might affect callers.
```

```text
Summarize the failing test output, name the most likely root cause, and propose
one focused fix before changing code.
```

Avoid vague prompts that trigger broad exploration:

```text
Look at this repo and improve it.
```

```text
Fix everything and make the code better.
```

## What to track as a team

Track usage and quality together. Low cost is not a win if it creates more human
review time, but high model spend should map to work that needed it.

Useful metrics include:

* AI credits used by team, repository, cost center, and user
* Work types that drive the most agent usage
* Pull requests where Copilot reduced review or implementation time
* Repeated prompts that should become reusable instructions
* Tasks that can stay on completions, next edit suggestions, or lightweight chat
* Tasks that need premium models or coding agents

## Budget controls to configure

Billing owners can control spend with budgets at four levels:

* Enterprise budgets for all organizations, repositories, and cost centers under
  the enterprise
* Organization budgets for all repositories in one organization
* Cost-center budgets for one cost center
* User budgets for individual users

Budgets are set in USD, while usage appears in AI credits. Since 1 AI credit is
$0.01 USD, a $10 budget covers 1,000 AI credits.

A practical rollout pattern is to set alerts first, watch normal usage for a few
weeks, then add hard limits where needed. For user-level budgets, remember that a
$0 budget means no access.

## Learning path

Use the supporting docs in order:

1. [Learning topics](docs/learning-plan.md) for the concepts and habits to cover.
2. [Budget playbook](docs/budget-playbook.md) for team-level controls and
   rollout decisions.

## Repository goals

This repo should help a team answer three questions:

* Which Copilot features should we use for which work?
* How do model and context choices affect AI credit consumption?
* What budgets and habits help us keep high-value Copilot usage available?
