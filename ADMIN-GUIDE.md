---
title: GitHub Copilot Usage-Based Billing Admin Guide
description: Budget setup, cost-center controls, policy guidance, rollout decisions, and reporting for GitHub Copilot usage-based billing
author: Microsoft
ms.date: 2026-07-22
ms.topic: how-to
keywords:
  - github copilot
  - budgets
  - cost centers
  - ai credits
  - billing
estimated_reading_time: 11
---

# Admin guide

Use this guide to keep high-value Copilot usage available while making spend
visible, attributable, and predictable. For the current announcement timeline
and model prices, start with [README.md](README.md).

## Five controls to configure first

1. Decide whether **AI credit paid usage** is allowed after included credits are
   exhausted.
2. Set a **universal user-level budget** so every licensed user has a clear
   total-consumption guardrail.
3. Add **cost-center or individual user-level overrides** only where different
   roles need different limits.
4. Set enterprise, organization, and cost-center metered budgets and enable
   **Stop usage when budget limit is reached** where a real hard stop is required.
5. For chargeback-sensitive groups, enable a **cost-center AI credit pool** so
   one team cannot consume included credits funded by another team's licenses.

> [!CAUTION]
> Metered budgets do not automatically stop charges. The stop-usage option is
> off by default. User-level budgets are different: they always enforce a hard
> stop and count both included and additional usage.

## Billing flow

Each request is evaluated in this order:

1. **User-level budget:** individual override, then cost-center user-level
   budget, then universal budget.
2. **Included pool:** if credits remain, the request draws from the shared pool,
   subject to any cost-center included-usage cap.
3. **Paid usage:** if the pool is empty, GitHub evaluates the paid-usage policy
   and the applicable cost-center, organization, or enterprise metered budget.

The lowest remaining headroom can block the user first. Increasing an enterprise
or cost-center budget does not unblock a user who has exhausted a user-level
budget.

## Control matrix

| Control | Purpose | Pool phase | Paid phase | Important behavior |
| --- | --- | :---: | :---: | --- |
| Universal user-level budget | Default total limit per user | Yes | Yes | Hard stop |
| Cost-center user-level budget | Different per-user limit by group | Yes | Yes | Overrides universal; hard stop |
| Individual user-level budget | Exception for one user | Yes | Yes | Highest precedence; hard stop |
| Cost-center AI credit pool | Protect included credits funded by the cost center | Yes | No | Cap calculated automatically |
| Cost-center budget | Limit a group's additional spend | No | Yes | Stop setting must be enabled |
| Organization budget | Limit additional spend for organization-billed seats | No | Yes | Stop setting must be enabled |
| Enterprise spending limit | Limit enterprise-wide additional spend | No | Yes | Not a cap on license fees |

Any user-level budget set to $0 blocks AI-credit-consuming Copilot features
immediately. Code completions and next edit suggestions continue because they do
not consume AI credits.

## Cost-center AI credit pools

GitHub launched cost-center included-usage caps on **July 2, 2026**.

Use this control when cost centers represent real funding or chargeback
boundaries:

* A cost center must contain at least one user or enterprise team.
* GitHub calculates the cap from the included credits funded by assigned Copilot
  Business and Copilot Enterprise licenses.
* The cap increases immediately when licenses are added or upgraded.
* Decreases apply at the next billing cycle.
* You choose whether reaching the cap blocks the group or allows paid usage,
  subject to enterprise policy and budgets.
* The AI credit pool can be used together with a cost-center budget.

Pool configuration launched through the REST API and became available directly
in the billing UI on **July 20, 2026**.

## Cost-center user-level budgets

GitHub launched this control on **June 30, 2026**.

It lets an enterprise admin set one per-user AI credit budget for every member
of a cost center, including members assigned through an enterprise team.
Membership changes automatically update who receives the limit.

Precedence:

```text
Individual user-level budget
  > Cost-center user-level budget
    > Universal user-level budget
```

This budget counts included and additional usage, so it can stop a user before
the enterprise pool is empty. It launched through the REST API and reached the
billing UI on **July 7, 2026**.

## Included credit planning

| Plan | Standard credits per user per month | Promotion through September 1, 2026 |
| --- | ---: | ---: |
| Copilot Business | 1,900 | 3,000 |
| Copilot Enterprise | 3,900 | 7,000 |

Included credits reset at 00:00 UTC on the first day of each calendar month and
do not roll over.

Before September 1:

1. Recalculate each billing entity and cost-center pool using standard amounts.
2. Compare June through August usage with the lower post-promotion pool.
3. Check whether user-level budgets collectively permit more usage than the
   standard pool can fund.
4. Confirm metered budgets cover the expected gap or intentionally block it.
5. Communicate the change before users encounter unexpected hard stops.

## Model governance

Model access is both a quality and cost decision.

Recommended posture:

* Make **Auto** the default where available. It routes based on task complexity
  and model health, preserves cache boundaries, and gives paid plans a 10%
  model-cost discount on supported surfaces.
* Keep lightweight models available for routine execution.
* Reserve expensive reasoning models for architecture, complex debugging, and
  high-risk work.
* Require explicit review before enabling models with special data or governance
  considerations.

### MAI-Code-1-Flash

MAI-Code-1-Flash became generally available for Business and Enterprise on
**June 26, 2026**. Admins must enable its model policy.

### Kimi K2.7 Code

Kimi K2.7 Code became available for Business and Enterprise on **July 7, 2026**.
It is Copilot's first selectable open-weight model, is hosted by GitHub on
Microsoft Azure, and is off by default for Business and Enterprise.

Before enabling Kimi, review:

* security and data-governance requirements;
* acceptable repositories and data classifications;
* model quality on representative tasks;
* current provider-list pricing; and
* whether a pilot group and tighter user-level budget are appropriate.

GitHub hosts Kimi on US-based Azure infrastructure managed by GitHub and
Microsoft. Customer prompts and responses are not sent to Moonshot AI.

## Copilot CLI in GitHub Actions

As of July 2, Copilot CLI can use the workflow's built-in `GITHUB_TOKEN` in an
organization-owned repository.

* Enable the **Allow use of Copilot CLI billed to the organization** policy.
* Give the workflow `copilot-requests: write` permission.
* No personal access token is required.
* AI credits are billed directly to the organization.
* User-level budgets do not apply because the usage is not attributed to a user.
* Use cost centers, billing dashboards, and `--max-ai-credits` session limits to
  manage the spend.

## Reporting and monitoring

### Weekly operating review

Track:

* total AI credits and additional spend;
* included pool utilization and projected month-end usage;
* usage by cost center, organization, repository, feature, model, and user;
* users approaching hard-stop budgets;
* high-value agentic workloads;
* repeated broad prompts, retries, and long sessions;
* Copilot code review AI credits; and
* Copilot code review GitHub Actions minutes for private repositories.

### Report field change

For AI usage reports from June 1, 2026 onward:

* use `quantity` for AI credit quantity;
* use `gross_amount` for dollar amount; and
* do not use the preview fields `aic_quantity` and `aic_gross_amount` for new
  usage analysis.

GitHub retroactively zeroed the preview fields for AI credit usage from June 1.
Reports from before June 1 remain unchanged.

### Usage metrics API

As of June 19, the Copilot usage metrics API exposes AI credits consumed per
user for daily and 28-day windows. Use this for:

* budget sizing;
* trend analysis;
* identifying users who need a different role-based limit; and
* coaching on workflow patterns.

Do not treat a high number as a verdict. Pair it with task type and delivery
outcomes.

## Policy starting points

| Team pattern | Paid usage | User-level posture | Other controls |
| --- | --- | --- | --- |
| New rollout | Allow with alerts | Moderate universal default | Weekly review before tightening |
| Mature product team | Allow | Universal plus justified overrides | Cost-center budget and pool |
| Finance-separated groups | Intentional by cost center | Cost-center user-level budgets | Cost-center AI credit pools |
| Sensitive or regulated work | Limited pilot | Tighter explicit limits | Restricted model policies |
| Migration or incident response | Temporarily higher | Time-bound individual overrides | Review and reset afterward |

## Client readiness

Older clients continue to work but can display stale pricing, inaccurate usage,
or outdated terminology. GitHub's June UBB guidance listed these minimums:

| Client | Minimum listed version |
| --- | --- |
| VS Code | 1.120 |
| Visual Studio 2022 | 17.14.33 |
| Visual Studio 2026 | 18.6.0 |
| JetBrains plugin | 1.9.1 |
| Eclipse plugin | 0.18.0 |
| Xcode extension | 0.50.0 |
| Copilot CLI | 1.0.48 |

Prefer the latest stable version rather than treating these as target versions.

Public-repository Actions minutes remain free. Private-repository Copilot code
reviews consume Actions minutes in addition to AI credits.

## Monthly review template

```text
Month:
Assigned Business licenses:
Assigned Enterprise licenses:
Included pool:
AI credits used:
Additional spend:
Pool utilization:
Top cost centers:
Top features and models:
Copilot code review Actions minutes:
Users approaching a hard stop:
High-value examples:
Coaching opportunities:
Budget or model-policy changes:
Forecast after September 1 promotion:
```

## Official references

* [Budgets for usage-based billing](https://docs.github.com/en/copilot/concepts/billing/budgets-for-usage-based-billing)
* [Usage-based billing for organizations and enterprises](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-organizations-and-enterprises)
* [Cost-center AI credit pools announcement](https://github.blog/changelog/2026-07-02-cost-centers-now-support-included-usage-caps/)
* [Cost-center AI credit pools in the billing UI](https://github.blog/changelog/2026-07-20-ai-credit-pools-for-cost-centers-in-the-billing-ui/)
* [Cost-center user-level budgets announcement](https://github.blog/changelog/2026-06-30-per-user-ai-credit-budgets-available-for-cost-centers/)
* [Cost-center user-level budgets in the billing UI](https://github.blog/changelog/2026-07-07-per-user-budgets-for-cost-centers-in-the-billing-ui/)
* [Copilot CLI in GitHub Actions](https://github.blog/changelog/2026-07-02-copilot-cli-no-longer-needs-a-personal-access-token-in-github-actions/)
* [Monitoring AI credit usage](https://docs.github.com/en/copilot/how-tos/manage-and-track-spending/monitor-ai-usage)
