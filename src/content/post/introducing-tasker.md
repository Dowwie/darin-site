---
title: "Tasker: Multi-agent Development with Claude Code"
publishDate: "22 December 2025"
description: "Introducing Tasker:  Agentic Development Framework using Spec-driven Planning and Execution with Claude Code "
tags: ["ai", "engineering"]
---

<div align="center">
<img src="https://github.com/Dowwie/tasker/blob/main/assets/logo.jpg" alt="Logo" width="100%" style="display: block; margin-top: 0; margin-bottom: 0; max-width: 100%;"/>
</div>


[Tasker](https://github.com/Dowwie/tasker) is a multi-agent architecture built with Claude Code that facilitates planning and implementation through a simple UI: `/plan` and `/execute`. It features a TUI dashboard for monitoring progress (tmux required).

The project began by taking a deep dive into task decomposition, developing a [protocol](https://github.com/Dowwie/tasker/blob/main/docs/protocol.md) for it and then using it as the basis for agentic planning. The task decomposition protocol is at the heart of the planning stage of Tasker.


## Tasker Execels at Large Projects

You can go a really long way with Claude Code using off-the-shelf capabilities for planning and implementation. I often do, using prompts like these:

**Planning:**
```
review {spec} and @README.md. then, review the source code. we're just planning,
converting specs to well-documented, self-contained tasks. These tasks will be
worked on by sub-agents, who need sufficient context to do a good job. Figure out
a concurrency strategy that you can apply across your task dependencies, where you
may safely spawn asynchronous sub-agents to work on tasks. Save a Task DAG
dependency graph along with the plan to plan.md
```

**Execution:**
```
I want you to read {specs} and {plan}. Use a concurrency strategy where you may
safely spawn asynchronous sub-agents to work on tasks in waves. Then, for each
task in the plan, spawn a sub-agent, concurrently when safe to do so, giving the
sub-agent the task and instruction to implement a solution for the task, and also
give it a full copy of {specs} for context about the project. Tell the sub-agent
to review the specs and the source code for the project before starting.
```

**This simple pattern works well for small changes whereas Tasker excels for larger projects.**


## Observations and Insights

I built Tasker in December 2025 and tested it across several Python projects of varying scope. To evaluate performance, I developed rubrics comparing implementations built with off-the-shelf Claude Code against those built with Tasker. Tasker consistently scored as well as, if not better than, the baseline.

Tasker currently uses skills and sub-agents powered by Opus 4.5 with unoptimized prompts. Typically, you wouldn't want an LLM to author prompts for production use since skilled engineers can still do a better job designing them. Given this limitation and the current results, I expect an optimized version of Tasker to perform even better. This is a promising start.


## Next Steps

Take a look at [the Github repo](https://github.com/Dowwie/tasker/tree/main) and give Tasker a try.

