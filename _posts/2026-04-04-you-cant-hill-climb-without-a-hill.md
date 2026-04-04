---
layout: post
title: "You Can't Hill-Climb Without a Hill"
date: 2026-04-04 20:17:38 +0000
categories: [problem-solving]
tags: [measurement, foundations, debugging, systematic-thinking]
excerpt: "Before you can improve a system, you need measurements you can actually trust — and getting to that point is often harder than the improvement work itself."
---

## The Situation

We were setting up an autonomous improvement loop — a system that would run a battery of tests against a piece of software, measure how well it performed, and then make targeted changes to push that score higher. The idea was elegant: define what "better" looks like, establish where you're starting from, then let the process run. Repeat until the scores stop improving.

The piece of software in question handled a complex, messy job: reading documents full of product names and prices and making sense of them. There were 70 hand-verified test cases, several categories of difficulty, and a clear scoring framework. The infrastructure looked ready. We had everything we needed to get a baseline.

Or so we thought.

## The Thinking

The early assumption was that "getting a baseline" was administrative work — a box to check before the real improvement work began. You run the tests, write down the numbers, and move on. The interesting part, we thought, was what came after: the iterative loop, the automated diagnosis, the changes.

What we found instead was that the measurement infrastructure had several layers of quiet brokenness. The test results were being written to one location inside the sandboxed environment, but the scoring system was looking for them somewhere else entirely. The directory structure we had built didn't match what the underlying framework expected. A file that was supposed to be accessible during one phase of the process was only reachable during a different phase, because of how the build context was scoped.

Each of these problems was invisible until we tried to actually run end-to-end. None of them showed up during setup. They only surfaced when the full chain — build, run, measure, report — was exercised as a single unit.

The fixes felt like detours. They weren't glamorous. They involved reading documentation for the underlying framework, checking where things actually landed versus where we assumed they landed, and making small structural adjustments. One by one, the chain started holding together.

## The Turn

The moment that shifted our thinking was when we finally got a score to register correctly — after a run that lasted several minutes, the system reported back a clean, unambiguous number. Not an error. Not a missing file. A result.

And we realized: everything we had done up to that point wasn't a detour. It was the work. The improvement loop we were excited to run is only useful if the scores it produces are real. A broken measurement system doesn't give you low scores — it gives you noise dressed up as scores. You can "improve" against noise indefinitely and never actually get better at anything.

Getting the measurement right wasn't the preamble to the project. It was the first and most important part of it.

## The Takeaway

Before you can improve anything, you need a way to measure that you can genuinely trust — and building that trust requires running the full chain under real conditions, not just inspecting the parts in isolation. The work of establishing a reliable baseline is never as trivial as it looks from the outside.

