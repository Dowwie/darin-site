---
title: "Vibes That Scale"
publishDate: "08 December 2025"
description: "A protocol for turning specifications into executable task graphs"
tags: ["agentic_development"]
draft: true
---

### The "90% Done" Illusion

We have all felt the rush. You prompt an agent, and it spits out a working component in seconds. It feels like magic. It’s "Vibe Coding"—development at the speed of thought.

But vibes hit a wall.

When you apply that workflow to sprawling architectures, the magic evaporates. The agent hallucinates methods, introduces circular dependencies, and burns tokens guessing your folder structure. You end up spending more time debugging the AI's "vibe" than writing the code yourself.

The problem is that **vibes don't scale.** To make AI-assisted development work for real systems, we need to trade *Stories* for *Systems*.

### Context Window Economics

An LLM's context window is its working memory. If you ask an agent to "implement the refund feature" without a plan, you force it to spend that limited budget on **archaeology**—reading code to guess where logic belongs.

By the time it starts writing, it has burned its budget.

We need a **Task Decomposition Protocol** that acts as a pre-compiler. By breaking specs into a dependency graph of atomic tasks *before* coding, you present the agent with a constrained environment: "Here are the 3 files. Here is the interface. Pass this test."

### The Protocol: Three Lenses

Most agile processes stop at the "User Story," leaving implementation vague. This protocol forces you to look through three lenses to bridge the gap between value and code.

**1. The Logical Lens (The "What")**
Break capabilities into **Behavioral Atoms**. "Process Refund" isn't one task; it is a chain: `ValidateRequest` → `CalculateAmount` → `UpdateLedger` → `EmitEvent`.

**2. The Physical Lens (The "Matter")**
Software obeys the conservation of matter: every logical atom must live in a concrete artifact. Ask: *"Exactly which file does this logic live in?"*
*   `CalculateAmount` → `src/billing/refund_service.ts`
*   `RefundProcessed` schema → `events/schemas/refund_v1.avsc`

We do not allow "dark matter"—implied work that lives in your head but not the plan.

**3. The Strategic Lens (The "When")**
Once we have atoms (logic) and artifacts (matter), we map dependencies. The result isn't a list; it's a **Directed Acyclic Graph (DAG)**.
*   *UI Task* waits for *API Types*.
*   *Ledger Update* waits for *Migration*.

### Steel Thread First

Most teams build by layer (DB, then API, then UI). This is high-risk; you don't discover integration issues until the end.

This protocol insists on a **Steel Thread**: the thinnest possible vertical slice that touches every layer and produces output.
*   **The Thread:** UI button → API → DB update → Log line.

You aren't building the feature yet; you are **testing the architecture**. For AI agents, this is critical: validate the wiring yourself before delegating the parallel work.

### The Contract: The Atomic Unit of Work

We don't write "Stories"; we write **Tasks**. A Task is a binary, executable unit.

**The Litmus Test:**
> *If I hand this to a competent engineer (or agent), do they know exactly which files to touch without asking questions?*

**Bad Task:**
> *Ticket #102: Work on Refund Logic*

**Protocol Task:**
> **Task:** `Implement RefundService.calculate()`
> **Context:** Component: `BillingService` | Spec: 3.2
> **Artifacts:** Modify `src/billing/refund_service.ts`
> **Interfaces:** Input `RefundRequestDTO` → Output `Money`
> **Verification:** `npm test tests/unit/refund_calculator.test.ts` passes.

For a human, this reduces cognitive load. For an AI, it provides the **Goal**, the **Location**, and the **Stopping Condition**.

### Different Modes, Same Graph

The beauty of a deterministic graph is that it decouples *planning* from *execution*.

*   **Traditional Team:** Clearer "Definition of Done" reduces coordination overhead.
*   **Cyborg Developer:** You build the Steel Thread (the spine); the AI fills in the parallel branches (the muscle).
*   **Agent Swarm:** Agents pick up tasks in parallel because dependencies are explicit.

Tools change, but the physics of software construction remain constant. This protocol demands you think deeply about the "Physical" reality of your software *before* you prompt. It feels slow in the first hour, but it is exponentially faster in the first week.
