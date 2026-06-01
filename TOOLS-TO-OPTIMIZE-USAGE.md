---
title: Tools to Optimize GitHub Copilot Usage
description: Practical tools and workflows for reviewing GitHub Copilot usage patterns and reducing low-value token spend
author: Microsoft
ms.date: 2026-06-01
ms.topic: guide
keywords:
  - github copilot
  - usage-based billing
  - chronicle
  - caveman
  - token optimization
estimated_reading_time: 4
---

## Tools to optimize usage

The most useful optimization tools help you see where Copilot work creates
value, where prompts are getting too large, and where repeated loops are costing
credits without improving the result.

## Chronicle in GitHub Copilot CLI

Use `/chronicle` in GitHub Copilot CLI to review recent Copilot activity and
spot patterns that affect usage-based billing.

Good uses for `/chronicle` include:

* Summarizing recent coding sessions for a daily or weekly standup
* Finding repeated prompt patterns that should become reusable instructions,
  prompts, or skills
* Reviewing long-running sessions that may have carried too much context
* Identifying expensive loops where the same request was retried without adding
  better files, errors, or constraints

Use the output as a coaching signal. The goal is not to shame heavy usage; it is
to make high-value Copilot work easier to repeat and low-value loops easier to
avoid.

## Caveman repository

[Caveman](https://github.com/JuliusBrussee/caveman/tree/main) is a
skill that reduces token usage by compressing prompts and summaries into terse,
high-signal language. The same pattern is useful for Copilot workflows when
teams want to compress noisy prompts, long handoffs, or subagent summaries before
sending them back through Copilot.

Compression helps reduce repeated input tokens while preserving the work context
that the next turn actually needs.

Use Caveman-style compression when:

* A session summary includes long narrative sections that can be reduced to
  decisions, files, constraints, and next actions
* A subagent returns a broad research dump and the next step needs only the
  actionable findings
* A repeated workflow carries the same setup text across turns
* A prompt can be converted into shorter bullets, explicit file references, and
  concrete acceptance criteria

Pair compression with review. A shorter prompt is only better when it keeps the
constraints, risks, and verification steps that matter.

## Additional habits to pair with tools

* Start with the smallest useful context window and add files only when needed.
* Ask Copilot for a plan before a broad agentic change, then let it implement
  once the scope is clear.
* Prefer reusable prompts or instructions for repeated work instead of pasting
  the same setup text into every session.
* Use targeted checks, such as focused tests or linting, before asking Copilot to
  continue.
* Capture successful patterns in team guidance so better usage becomes the
  default path.