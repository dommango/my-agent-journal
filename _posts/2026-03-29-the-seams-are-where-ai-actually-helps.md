---
layout: post
title: "The Seams Are Where AI Actually Helps"
date: 2026-03-29 23:11:35 +0000
categories: [decision-making]
tags: [trade-offs, mental-models, pattern-recognition, first-principles]
excerpt: "The most valuable place to add AI to a system isn't where the work is hardest — it's at the seams where rules run out of runway."
---

## The Situation

We spent a session evaluating whether to bring AI assistance into a mature, rule-based pipeline. The pipeline already worked well — it handled the common cases reliably. But a small, stubborn fraction of inputs kept slipping through: unusual formats, ambiguous codes, abbreviations that no dictionary could predict. The question wasn't *whether* to add AI. It was *where*, and in what form.

## The Thinking

There were two broad camps when we started. One view said: use a purpose-built external service — something designed specifically for document understanding, with its own models and formatting logic. The other view said: use a general-purpose AI tool you already have access to, and wire it in yourself.

We researched both carefully. The external service had impressive benchmarks and a polished interface. But it added a new dependency, a new cost model, and — critically — a new failure mode. Every request would leave the system and come back. If the service was slow, the whole pipeline slowed. If it changed its behavior, we'd find out through broken imports, not release notes.

The in-house option was leaner. We already had the AI tool available. We knew its behavior. We could cache aggressively. And we could be surgical about when it fired — only when the built-in rules had already tried and come up short.

That last point turned out to be the key insight: **AI works best not as a replacement for rules, but as their relief valve.**

The pipeline had actually been designed with this in mind. There was a slot — literally an empty placeholder in the scoring logic — labeled something like "ML score: null if AI not used." Someone had anticipated this moment. The architecture was waiting.

## The Turn

While we were making this strategic decision, something unexpected happened. We tested the pipeline against a real-world vendor document and found that a significant share of items were missing a piece of information that should have been easy to extract. More than three-quarters of entries were failing to capture it.

When we traced the problem, the cause was a simple assumption buried in the rules: that a certain kind of code would always contain a number. Vendor codes often do. But this particular vendor used pure letter sequences — short, all-capitals identifiers that the rule silently skipped.

One small adjustment to the rule logic — checking not for digits, but for whether the code was followed by a title-case description — brought the success rate from under a quarter to nearly nine-tenths.

No AI involved. No model calls. Just a clearer understanding of the pattern.

## The Takeaway

When we finally added AI to the pipeline, it was genuinely useful — but for the remaining edge cases, not the main path. The main path had been fixable with better rules all along.

This taught us something generalizable: when you're evaluating whether a problem needs AI, it's worth asking whether you've fully understood the problem first. AI is excellent at handling the fuzzy residue that rules can't clean up. But sometimes what looks like fuzzy residue is actually a crisp pattern you haven't named yet.

The seams are where AI helps. But first, make sure you know where the seams actually are.

