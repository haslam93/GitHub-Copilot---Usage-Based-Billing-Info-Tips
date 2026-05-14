---
title: GitHub Copilot Usage-Based Billing Training Guide
description: Topic-based coverage for teaching practical GitHub Copilot habits under usage-based billing
author: Microsoft
ms.date: 2026-05-14
ms.topic: tutorial
keywords:
  - github copilot
  - training
  - usage-based billing
  - ai credits
estimated_reading_time: 6
---

## Training Guide

Use these topics with developers, engineering managers, and platform teams who
need to adapt Copilot habits before usage-based billing begins on June 1, 2026.
The topics can be covered in a workshop, brown bag, team meeting, onboarding
path, or self-paced review.

For the user-facing guidance, see [USER-GUIDE.md](USER-GUIDE.md). For budget
and policy guidance, see [ADMIN-GUIDE.md](ADMIN-GUIDE.md).

## GitHub AI Credits and Billing Basics

Cover how GitHub AI Credits work and what does or does not consume them.

Topics to include:

1. Review included credits for Copilot Business and Copilot Enterprise.
2. Compare completion usage with chat, CLI, cloud agent, Spaces, Spark, and
   third-party coding agents.
3. Calculate a simple pool size for a 25-person and 100-person team.
4. Discuss what should happen when included credits are exhausted.

Practice prompt:

```text
Explain GitHub AI Credits to a developer team in five bullet points. Include
what is billed, what is not billed, and why model choice matters.
```

## Choosing the Right Copilot Mode

Cover how common development tasks map to completions, chat, edit mode, agent
mode, CLI, and code review.

Topics to include:

1. List common team tasks from the last sprint.
2. Mark each task as low, medium, or high context.
3. Choose the lowest-friction Copilot mode for each task.
4. Identify tasks where agent mode is worth the extra context and token use.

Decision guide:

| Task | Good starting mode | Why |
| --- | --- | --- |
| Fill in local implementation details | Code completions | Unlimited on paid plans and fast for narrow edits |
| Explain one file or function | Chat | Focused context and quick iteration |
| Modify several related files | Edit or agent mode | Useful when changes cross file boundaries |
| Diagnose terminal or command usage | Copilot CLI | Keeps command reasoning close to the shell |
| Review a pull request | Copilot code review | Helpful for broad review, but also consumes AI credits and GitHub Actions minutes |

## Prompting for Less Waste

Cover prompt patterns that reduce broad scans, retries, and unnecessary
generated output.

Topics to include:

1. Rewrite vague prompts into focused prompts.
2. Practice asking Copilot to inspect before editing.
3. Limit scope by naming files, functions, tests, or constraints.
4. Ask for a short plan only when the task is ambiguous or risky.

Prompt template:

```text
Goal: <specific outcome>
Scope: <files, folders, or APIs Copilot should consider>
Constraints: <what must stay unchanged>
Verification: <tests, commands, or manual checks to run>
Before editing: summarize the likely change in two sentences.
```

## Efficient Verification

Cover habits that keep quality high without repeatedly asking Copilot to redo
broad work.

Topics to include:

1. Review a Copilot-generated diff and identify assumptions.
2. Run the smallest relevant tests first.
3. Ask Copilot to explain only the changed behavior.
4. Create reusable prompts for common verification tasks.

Verification prompt:

```text
Review only this diff for functional regressions, missing tests, and surprising
behavior. Prioritize concrete findings with file references.
```

## Team Norms and Budget Monitoring

Cover how the team will decide when higher-cost Copilot workflows are worth it
and how usage will be monitored.

Topics to include:

1. Decide when lightweight models are the default.
2. Define when premium models or agent mode are appropriate.
3. Agree on what usage patterns deserve coaching instead of budget blocking.
4. Document who monitors usage and who adjusts budgets.

Team agreement starter:

```text
We use Copilot freely for completions and focused chat. We use larger models and
agentic workflows when the task crosses files, needs deeper reasoning, or saves
meaningful engineering time. We watch usage trends weekly during rollout and
adjust budgets based on observed value, not guesswork.
```