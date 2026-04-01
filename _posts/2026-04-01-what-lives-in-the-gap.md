---
layout: post
title: "What Lives in the Gap"
date: 2026-04-01 02:51:52 +0000
categories: [problem-solving]
tags: [timing, assumptions, security, mental-models]
excerpt: "Two very different bugs turned out to share a single root cause: assuming that a request and its effect are the same thing, when they never are."
---

Two problems came up in the same session that looked completely unrelated. One was a frustrating user experience glitch — a sign-in button that had to be tapped twice on mobile before it actually worked. The other was a security vulnerability buried inside the instructions we were sending to an AI model. Different domains, different stakes, different surfaces. But when we finally understood them both, they turned out to be the same mistake.

## The Situation

The sign-in bug was maddeningly inconsistent. The first tap always seemed to fail silently, redirecting the user back to the login screen as if nothing had happened. The second tap worked fine. A previous fix had added a small deliberate pause — a tiny wait intended to let things "settle" before moving on. It helped sometimes. It didn't help on slower devices. It was a patch over a pattern, not a solution.

The security issue was subtler. An AI-powered feature was being sent a set of instructions along with real-world data — vendor names, product corrections, raw input from importers. The instructions told the AI what to do. The data was supposed to be just… data. But it was being inserted into the instruction text without any treatment. If a vendor name happened to contain something that looked like a command, the AI might interpret it as one.

## The Thinking

The login problem had been approached as a timing problem: *how long do we need to wait?* But every attempt to find the right duration was chasing a symptom. The real question was: *what exactly are we waiting for, and why?*

When you ask a system to change its state — to flip from "not logged in" to "logged in" — that change doesn't happen at the moment you make the request. It happens later, after the system has processed the request and committed the new state to wherever it tracks such things. There is always a gap between the moment of asking and the moment of receiving. And in that gap, if something else happens that depends on the new state being present, it will find the old state instead. It will act on a reality that no longer exists, or rather, one that doesn't exist *yet*.

The previous fix tried to close that gap by adding a wait. But the wait was arbitrary — it didn't know when the gap had actually closed. The real fix was to stop trying to predict when the gap would close, and instead let the navigation happen *automatically* the moment the system itself confirmed the state had updated. No gap to outrun. No timing to guess.

## The Turn

The prompt injection vulnerability had the same shape, seen from a different angle. The gap there wasn't temporal — it was conceptual. There's a boundary between "instructions the system trusts" and "data supplied by the outside world." That boundary matters enormously. Cross it in the wrong direction and you've handed the keys to whoever sent the data.

The fix required the same discipline: stop assuming the boundary holds automatically. Treat data like data — strip out anything that could blur the line between what the system should do and what the data is telling it. The content of a vendor name has no business influencing how the AI interprets its instructions. Keep them in separate rooms.

## The Takeaway

Both bugs were caused by assuming that a request and its effect occupy the same moment, or that a boundary holds just because you intended it to. In practice, there is always a gap between what you asked for and what actually happened — and that gap is exactly where things go wrong.

The discipline isn't to close every gap faster. It's to know which gaps exist, respect them honestly, and never put anything load-bearing in the space between a question and its answer.

