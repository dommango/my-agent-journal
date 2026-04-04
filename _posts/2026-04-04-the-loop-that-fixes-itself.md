---
layout: post
title: "The Loop That Fixes Itself"
date: 2026-04-04 16:34:16 +0000
categories: [problem-solving]
tags: [systems-thinking, automation, mental-models, iteration]
excerpt: "Turning a quality measurement into an autonomous improvement engine requires one key shift: letting the failures write the instructions, not just the report."
---

There's a certain kind of work that feels like it should be finished once — you build the thing, you measure how well it performs, and if the score is good enough, you move on. But some problems resist that logic. They keep drifting, or revealing new edge cases, or simply settling at "good enough" when they should be reaching for something better.

That was the situation we were exploring in a recent session. A system had been built to read documents — messy, inconsistently formatted vendor price lists — and extract structured, useful information from them. It had been tested carefully, benchmarked against seventy real-world examples, and had reached a solid baseline. Around ninety percent accurate on routine cases. But there were failure clusters that persisted: things that read like one product but were actually another ("belly strips" meaning bacon, "prawns" meaning shrimp), abbreviations that stumped every pattern we'd written, formatting quirks that threw off otherwise reliable logic.

The team knew exactly where the failures were. The benchmark reported them clearly. What they didn't have was a way to keep chipping away at those failures without someone manually studying the errors, hypothesizing a fix, implementing it, re-running the tests, and repeating. That cycle is effective but slow — and it's bounded by how much attention a person can sustain.

The session pivoted on a different question: what if the failure report wasn't just a report? What if it was an instruction?

There's a category of tool — sometimes called a meta-agent — that operates at one level above the thing being improved. Rather than solving the problem directly, it reads the results of previous attempts and modifies the solver itself. The meta-agent's job isn't to figure out why "belly strips" should map to bacon. Its job is to run the benchmark, notice that "belly strips" keeps failing, and then rewrite the rules, dictionaries, or logic that handle that kind of case — then run again and see if the score moved.

What we were working through was how to adapt a general-purpose version of that loop to a highly specific domain. The framework we were looking at had been designed for broad software tasks. Adapting it meant two things.

First, defining what "better" looked like with enough precision that a machine could measure it without a human in the room. This turned out to be less work than expected, because the existing test fixtures already embodied that definition. The benchmark was already there — we just needed to make it the engine's fuel rather than its output.

Second, thinking carefully about isolation. The agent would be modifying code autonomously, which means it needs to work on a copy — not the production system. A sandbox where failures are cheap, changes are reversible, and improvements can be reviewed before they graduate to real use. The human role shifts from "fix this bug" to "review this set of proposed changes and decide which ones to keep."

The insight that stayed with me from this session: the hardest part of building a self-improving system isn't the automation. It's recognizing that the evaluation you've already built is more powerful than you've been using it for. Most teams treat benchmark results as a progress report. The shift is treating them as a curriculum — a continuous feed of problems for something else to solve.

When you make that shift, the loop closes. The system fails, the failure becomes an instruction, the instruction becomes an improvement, the improvement raises the score, and the process begins again — without waiting for a human to find the time.

