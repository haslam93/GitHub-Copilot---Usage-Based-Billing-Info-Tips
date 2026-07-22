---
title: Tools to Optimize GitHub Copilot Usage
description: Chronicle, context management, cache preservation, session limits, and reusable guidance for efficient Copilot workflows
author: Microsoft
ms.date: 2026-07-22
ms.topic: guide
keywords:
  - github copilot
  - chronicle
  - cache
  - context
  - token optimization
estimated_reading_time: 7
---

# Tools to optimize usage

The best optimization tools do not simply shorten prompts. They show where
context is going, preserve reusable context, cap runaway sessions, and turn
successful patterns into durable guidance.

## Chronicle in GitHub Copilot CLI

GitHub announced the expanded Chronicle experience on **June 2, 2026**.
Chronicle queries your Copilot session history across CLI, cloud agent, code
review, VS Code, JetBrains, GitHub Copilot app, and GitHub.com when syncing is
available.

```text
/chronicle standup last 3 days
/chronicle tips
/chronicle cost tips
/chronicle improve
/chronicle search authentication
```

| Command | Use it for |
| --- | --- |
| `/chronicle standup` | Summarize recent work |
| `/chronicle tips` | Find workflow and feature improvements |
| `/chronicle cost tips` | Analyze token patterns and reduce cost |
| `/chronicle improve` | Generate improvements for custom instructions |
| `/chronicle search KEYWORD` | Find sessions containing a specific term |
| `/chronicle reindex` | Rebuild the local session index from session files |

Local session files are stored in `~/.copilot/session-state/`. The searchable
local index is stored in `~/.copilot/session-store.db`.

Session syncing is private to the user by default. Business and Enterprise admins
must allow **Store local sessions in the Cloud** before local sessions can be
queried across supported Copilot surfaces.

Chronicle has no separate published fee. Its generated summaries and analysis
use the Copilot CLI model path and should be treated as AI-credit-consuming CLI
interactions.

## Context inspection and compaction

Use `/context` to see how the current context window is divided among:

* system prompt;
* custom instructions;
* built-in tool definitions;
* MCP tool definitions;
* messages; and
* remaining free space.

Use `/compact` to summarize a long conversation before a new phase:

```text
/compact focus on decisions, changed files, and remaining tests
```

Copilot CLI begins automatic compaction at roughly 80% context usage. A manual
compaction is useful earlier when research is complete and implementation is
about to begin.

Start `/new` or `/clear` for an unrelated task. A clean session is usually
better than carrying a long, irrelevant history.

## Cache preservation

Prompt caching is valuable because agentic workflows repeatedly send the same
system prompt, file context, and tool schemas.

Keep these stable during a session:

* selected model;
* reasoning effort;
* context tier;
* enabled MCP servers; and
* enabled tools.

Changing them can invalidate the cache and make the next request rebuild the
full context as fresh input. GitHub documents cache expiry after 24 hours for
OpenAI models and 1 hour for most other models.

Use Auto model selection when possible. It routes at natural cache boundaries
and gives paid plans a 10% model-cost discount on supported surfaces.

## Session credit limits

Copilot CLI session limits are in public preview.

```text
/limits set max-ai-credits 50
/limits unset
```

For a non-interactive task:

```text
copilot -p "Run a focused review of this diff" --max-ai-credits 50
```

These are soft limits: a model response in progress can complete after the
threshold is reached. They supplement, rather than replace, monthly user-level
budgets.

Session limits are especially important for Copilot CLI in GitHub Actions. When
the CLI authenticates with `GITHUB_TOKEN`, usage is billed directly to the
organization and user-level budgets do not apply.

## Repository custom instructions

Use `.github/copilot-instructions.md` or `AGENTS.md` to give Copilot a compact
map of the repository:

* architecture and folder boundaries;
* required frameworks and patterns;
* known pitfalls;
* build, test, and lint commands; and
* clear output expectations.

Keep instructions short, specific, and based on observed behavior. Generic
pages of advice consume tokens on every run and can make the relevant rules
harder to find.

Use `/chronicle improve` to identify repeated mistakes, then add only the
instruction that prevents that concrete pattern.

## Toolset hygiene

Every MCP tool schema occupies context, even if the tool is never called.

* Enable only the toolsets relevant to the task.
* Prefer targeted file reads and filtered command output.
* Avoid sending whole logs when the error and surrounding lines are enough.
* Use specialized subagents for narrow work and cheaper models where available.

## Deterministic guardrails

Tests, linters, and security scans can reduce total token use even when they add
one extra step. They stop an agent from building additional work on an incorrect
assumption.

Recommended loop:

```text
Make one coherent change
  -> run the smallest deterministic check
  -> inspect the diff
  -> continue only if the signal is clean
```

## Optional prompt compression

[Caveman](https://github.com/JuliusBrussee/caveman/tree/main) is a third-party
skill that demonstrates terse, high-signal prompt and summary compression.
Treat it as an optional pattern, not an official GitHub billing tool.

Compression is useful for:

* handoffs that can be reduced to decisions, files, constraints, and next steps;
* long research results where only verified findings are needed;
* repeated setup text that belongs in custom instructions; and
* subagent summaries that can omit narrative.

Do not remove acceptance criteria, security constraints, or verification steps
just to save tokens.

## Weekly optimization routine

1. Run `/chronicle cost tips`.
2. Review the AI usage page by feature and model.
3. Find one repeated prompt or mistake to encode in custom instructions.
4. Identify sessions that should have used `/compact` or a new conversation.
5. Check whether large MCP toolsets are enabled unnecessarily.
6. Compare high usage with delivered value before changing budgets.

## Official references

* [Optimizing AI usage](https://docs.github.com/en/copilot/tutorials/optimize-ai-usage)
* [Copilot CLI Chronicle](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/chronicle)
* [Copilot CLI context management](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management)
* [Auto model selection](https://docs.github.com/en/copilot/concepts/models/auto-model-selection)
* [AI credit session limits](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/set-session-limit)
* [Copilot CLI in GitHub Actions](https://github.blog/changelog/2026-07-02-copilot-cli-no-longer-needs-a-personal-access-token-in-github-actions/)
