---
title: GitHub Copilot Usage-Based Billing Training Guide
description: Workshop modules for GitHub AI Credits, budgets, model choice, cache preservation, Chronicle, and cost-efficient agent workflows
author: Microsoft
ms.date: 2026-07-22
ms.topic: tutorial
keywords:
  - github copilot
  - training
  - usage-based billing
  - ai credits
  - chronicle
estimated_reading_time: 8
---

# Training guide

Use these modules for developer workshops, manager briefings, platform-team
enablement, onboarding, or self-paced learning.

For current prices and dates, use [README.md](README.md). For role-specific
guidance, use [USER-GUIDE.md](USER-GUIDE.md) and
[ADMIN-GUIDE.md](ADMIN-GUIDE.md).

## Suggested 60-minute workshop

| Time | Module |
| ---: | --- |
| 10 min | AI credit and pooling basics |
| 10 min | Budget and cost-center controls |
| 10 min | Model choice, MAI, Kimi, and Auto |
| 10 min | Context and cache preservation |
| 10 min | Chronicle and session limits |
| 10 min | Team scenarios and commitments |

## Module 1: AI credit basics

Learning objectives:

* Explain that 1 AI credit equals $0.01 USD.
* Identify which Copilot features consume credits.
* Explain Business and Enterprise monthly pools.
* Explain the September 1 promotional-credit change.

Key facts:

| Plan | Standard credits per user | Promotion through September 1, 2026 |
| --- | ---: | ---: |
| Copilot Business | 1,900 | 3,000 |
| Copilot Enterprise | 3,900 | 7,000 |

Exercise:

1. Calculate the standard pool for 25 Business users.
2. Calculate the promotional pool.
3. Discuss what happens when the pool is exhausted.

Answer: 47,500 standard credits and 75,000 promotional credits.

## Module 2: Budget controls

Teach the difference between:

* user-level budgets, which count pool and paid usage and always hard-stop;
* cost-center AI credit pools, which protect included usage;
* cost-center, organization, and enterprise budgets, which govern additional
  spend after the pool is exhausted; and
* the paid-usage policy and stop-usage setting.

Scenario:

```text
An enterprise has a central platform team and three product groups. The platform
team does more agentic work, while each product group funds its own licenses.
Design a universal user budget, one cost-center override, included-usage caps,
and additional-spend budgets.
```

Ask participants to explain which control blocks usage first.

## Module 3: Model rollout and governance

Timeline to teach:

* June 2: MAI-Code-1-Flash began rolling out to individual plans.
* June 18: MAI-Code-1-Flash expanded across Copilot surfaces.
* June 26: MAI-Code-1-Flash became GA for Business and Enterprise.
* July 1: Kimi K2.7 Code began rolling out to Pro, Pro+, and Max.
* July 7: Kimi became available to Business and Enterprise, off by default.

Discussion:

* Why is the cheapest token price not always the cheapest completed task?
* When should a team use a lightweight execution model?
* When is a reasoning model worth the cost?
* What security and governance review should precede an open-weight model pilot?

Teach Auto as the default where available: it routes based on task complexity,
protects cache boundaries, and gives paid plans a 10% model-cost discount.

## Module 4: Prompting and context

Rewrite a vague prompt:

```text
Look at this repo and improve it.
```

Into:

```text
Goal: Fix the authentication redirect loop.
Scope: The route handler and its direct tests.
Constraints: Keep the public API unchanged.
Verification: Run the focused authentication tests.
Stop when: The failure is reproduced, fixed, and the targeted tests pass.
Before editing: Explain the likely root cause.
```

Review why the second prompt reduces exploration, retries, and scope drift.

## Module 5: Protect the cache

Teach that the following can invalidate prompt cache reuse:

* switching models;
* changing reasoning effort;
* changing context size;
* changing enabled tools or MCP servers; and
* returning after cache expiry.

Hands-on CLI exercise:

```text
/context
/compact focus on the implementation plan and remaining tests
```

Ask participants when they should use `/new` instead of `/compact`.

Expected answer: start a new session for an unrelated problem; compact when the
same task continues but the history has grown.

## Module 6: Chronicle

Run or demonstrate:

```text
/chronicle standup last 3 days
/chronicle tips
/chronicle cost tips
/chronicle improve
```

Discuss how Chronicle can:

* identify repeated high-token patterns;
* find recurring mistakes for custom instructions;
* summarize recent work;
* locate previous sessions; and
* improve team coaching without treating high usage as inherently bad.

Privacy note: sessions are private to the user by default. Business and
Enterprise admins must allow local-session cloud syncing for cross-device use.
Chronicle-generated insight is a normal Copilot CLI model interaction and should
be treated as consuming AI credits.

## Module 7: Session limits and guardrails

Demonstrate the public-preview CLI limit:

```text
/limits set max-ai-credits 50
```

Then discuss:

* why the limit is soft;
* why it does not replace a monthly user-level budget;
* how tests and linting stop costly error chains; and
* why targeted output is better than full logs.

## Team agreement starter

```text
We use completions freely for local coding. We default to Auto for supported
Copilot workflows, keep session settings stable to protect the cache, and use
larger reasoning models when the task genuinely needs them. We split unrelated
work into new sessions, compact long CLI sessions, and verify changes with
targeted deterministic checks. We review usage alongside engineering outcomes,
not as a standalone performance metric.
```

## Facilitator checklist

* Verify current model prices before the session.
* Update screenshots if the billing UI changed.
* Explain the July 1 and July 7 Kimi rollout dates separately.
* Explain that cost-center pools and cost-center budgets control different
  phases.
* Explain that cost-center per-user budgets reached the UI on July 7 and AI
  credit pools reached it on July 20.
* Remind admins that the September promotion ends September 1.
* End with one concrete team norm and one budget owner.

## Official references

* [Optimizing AI usage](https://docs.github.com/en/copilot/tutorials/optimize-ai-usage)
* [Budgets for usage-based billing](https://docs.github.com/en/copilot/concepts/billing/budgets-for-usage-based-billing)
* [Models and pricing](https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing)
* [Copilot CLI Chronicle](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/chronicle)
