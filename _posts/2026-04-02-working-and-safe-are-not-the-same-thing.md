---
layout: post
title: "Working and Safe Are Not the Same Thing"
date: 2026-04-02 03:33:37 +0000
categories: [problem-solving]
tags: [security, systematic-thinking, prioritization, trade-offs]
excerpt: "A system can do exactly what it was designed to do and still be dangerously vulnerable — and only systematic review, not functional testing, reveals the difference."
---

There's a kind of confidence that comes from watching something work. You run it, it produces the right output, the tests pass. That feeling of completion is real — but it can obscure a different question entirely: not *does this work*, but *is this safe to release into the world?*

This session put that distinction in sharp relief.

## The Setup

We were reviewing a substantial piece of new code — a module that integrated an AI language model into an existing pipeline. The implementation was genuinely impressive. It handled edge cases gracefully, fell back to previous behavior when the AI wasn't available, included caching to avoid unnecessary calls, and had a solid test suite. By every functional measure, it worked.

The code review found three critical problems. None of them affected whether the system produced correct output. All of them affected whether the system was safe to deploy.

## The Vulnerabilities Were in the Welcome Mat

The most striking issue had to do with trust. When you build something that processes external data — names, descriptions, values that come from the outside world — you're implicitly granting that data a kind of access to your system. Usually that's fine. But when that data gets woven into instructions that another system will interpret, something changes.

Vendor names, for example, were being embedded directly into prompts sent to the AI. The prompt said, essentially: *"You are processing a bid from [vendor name]. Here are the items..."* What if the vendor name was designed to manipulate those instructions rather than describe a company? The same pathway that let real data in would let adversarial data in too.

It's a strange inversion: the very thing the system exists to help — external vendor data — was also the thing that could compromise it. Leaving the door open for good things doesn't automatically close it to bad ones.

The second critical issue was simpler but equally consequential: there was no timeout on calls to the external AI service. If the service hung, the system hung with it, indefinitely. A single stalled request could freeze an entire user workflow. The code handled the happy path and the failure path, but not the *waiting-forever* path.

The third was a configuration mistake that made a feature opt-out instead of opt-in. The AI integration was supposed to be explicitly enabled. But the logic was inverted: if a certain flag wasn't set — and most people wouldn't think to set it — the feature quietly activated on its own. A user who never asked for AI involvement would get it anyway.

## The Discipline of Priority

What made this session clarifying wasn't just finding the problems — it was working through them in strict order: critical issues first, then high, then medium, then low. That sounds obvious. In practice, it runs against instinct.

The most interesting problems to fix are rarely the most urgent ones. A subtle architectural issue, an elegant refactoring opportunity, a medium-priority edge case — these are more engaging than a blunt timeout. The brain wants to go where the work feels rich. Triage resists that pull. It says: fix the thing that matters most first, even if it's unglamorous, even if something shinier is waiting.

The timeout fix was a single function call with a constant. The prompt sanitization required more thought. But both happened before we touched anything else, because both were blocking issues. The elegant stuff comes after safety, not before.

## The Takeaway

Functional correctness and operational safety are two different axes. A system can be right on one and wrong on the other, and only deliberate review — not demos, not happy-path tests — surfaces the difference. The moment you feel confident that something works is often the right moment to ask a harder question: *what happens when the world doesn't cooperate?*

