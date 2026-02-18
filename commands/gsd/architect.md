---
name: gsd:architect
description: Launch the autonomous architect agent to drive development with minimal user intervention
argument-hint: "[instruction or phase number]"
agent: gsd-architect
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Task
  - TodoWrite
  - AskUserQuestion
  - WebFetch
  - WebSearch
  - mcp__context7__*
---

<objective>
Launch the GSD Architect — an autonomous tech lead agent that drives the full plan-execute-verify lifecycle. The architect makes routine decisions autonomously, only escalating truly strategic or ambiguous choices to you.

Use this when you want to hand off control and let Claude drive development with your project vision as the guide.
</objective>

<context>
Instruction: $ARGUMENTS

@.planning/PROJECT.md
@.planning/REQUIREMENTS.md
@.planning/ROADMAP.md
@.planning/STATE.md
</context>

<process>

## What the Architect Does

1. **Loads your full project context** — PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md, codebase maps, prior decisions
2. **Determines what to do next** based on current state and your instruction
3. **Drives execution autonomously:**
   - Plans phases (spawns gsd-planner)
   - Executes plans (spawns gsd-executor)
   - Verifies work (spawns gsd-verifier)
   - Makes technical decisions based on your established patterns
   - Fixes issues without bothering you
4. **Only asks you** when decisions are truly strategic, expensive to reverse, or ambiguous
5. **Reports back** with what was built, decisions made, and what's next

## When to Use

- `/gsd:architect` — Continue from where the project left off
- `/gsd:architect build phase 3` — Execute a specific phase autonomously
- `/gsd:architect plan and build the auth system` — High-level instruction
- `/gsd:architect finish the current milestone` — Drive to milestone completion

## Decision Authority

| Decision Type | Architect Decides | Asks You |
|---|---|---|
| Library choice within stack | Yes | — |
| API/component design | Yes | — |
| Adding new dependency | Yes (documents it) | — |
| New architectural pattern | Yes (documents it) | — |
| Changing core tech stack | — | Yes |
| Dropping planned features | — | Yes |
| Security-critical choices | — | Yes |
| Spending real money | — | Yes |

## Compared to Other Commands

| Command | Control Level |
|---|---|
| `/gsd:plan-phase` | You approve each plan |
| `/gsd:execute-phase` | You handle checkpoints |
| `/gsd:architect` | Architect handles most decisions for you |

</process>
