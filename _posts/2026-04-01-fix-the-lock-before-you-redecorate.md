---
layout: post
title: "Fix the Lock Before You Redecorate"
date: 2026-04-01 04:02:04 +0000
categories: [decision-making]
tags: [prioritization, trade-offs, mental-models, first-principles]
excerpt: "When evaluating better ways to do something, the most important decision is often not which improvement to make first — it's recognizing when a vulnerability hiding in the existing system must be addressed before any of them."
---

We were in the middle of a genuine improvement project. A system that processed and interpreted incoming data — vendor price lists, in this case — was working well enough, but we'd been handed a roadmap of enhancements. Better accuracy. Smarter matching. Faster turnaround. Three different tools had been evaluated, each with detailed cost and speed profiles. We had a plan, and it was a good one.

Then, partway through the review, we found something that stopped us cold.

## The Problem Hiding in Plain Sight

The system accepted text from the outside world and passed parts of it into instructions that a language model would follow. Vendor names. Product descriptions. Correction notes left by human reviewers. All of it flowed through, largely unexamined.

The vulnerability was this: if someone supplied text specifically crafted to look like an instruction rather than data, the system might follow it. A vendor name that was actually a command. A correction note that quietly overrode the rules. This kind of flaw — where the system can't reliably distinguish between "information it was given" and "instructions it should obey" — is a known category of problem, and it's serious.

We had been about to layer three new capabilities on top of a system with this flaw. Better matching logic. Smarter cost optimization. Semantic understanding that could handle abbreviations and variations. All of it would have been built on a foundation with a hole in it.

## What Stopping Felt Like

The honest answer is that stopping was mildly uncomfortable. We had momentum. The improvements were concrete, the analysis was done, and the path forward was clear. Pausing to fix a vulnerability that hadn't been exploited yet — and might never be — felt like a detour.

But here's what shifted the thinking: the improvements we were planning would make the system *more* capable. More capable systems with unfixed flaws are more dangerous than limited ones. Every new feature would amplify what could go wrong if the underlying issue remained.

So we sanitized the inputs. Not dramatically, not expensively — just a careful pass to ensure that anything coming in from the outside world was treated as data, not instruction. And then we continued.

## The Layering Question

The other interesting challenge from this session was one of design: we had evaluated several tools and approaches, each genuinely good, and needed to decide how to use them together. One tool was fast and cheap, excellent at following explicit rules. Another was sophisticated and semantic, able to understand meaning and variation. A third specialized in handling documents that weren't neatly structured.

The instinct — common and understandable — was to pick the best one and use it everywhere. But the more we looked at the problem, the clearer it became that "best" was not a single answer. The fast, rule-based approach worked perfectly for cases where the data was clean and predictable. The semantic approach was essential where language was ambiguous. The fallback mattered precisely when the others failed.

We ended up with layers: handle predictable cases deterministically, escalate uncertain ones to deeper analysis, reach for the most sophisticated tool only when genuinely needed. Not a compromise, but a recognition that different parts of the same problem have different shapes.

## The Takeaway

Two lessons, tightly connected. When you find a flaw in something you're about to improve, fix the flaw first — not because it's urgent, but because improvement amplifies everything, including what's broken. And when evaluating tools, the question is rarely "which is best?" It's "best at what, and when?"

