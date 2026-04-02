---
layout: post
title: "The Question That Turned Into an Audit"
date: 2026-04-02 19:05:29 +0000
categories: [decision-making]
tags: [trade-offs, assumptions, mental-models, security]
excerpt: "Researching a strategic decision you've already made isn't wasted work — it builds exactly the understanding you need to evaluate whether you made it safely."
---


We came into a session with what felt like a clean strategic question: which outside AI service should we bring in to handle a messy, error-prone part of the system? Two serious contenders. We did the research carefully — pricing, speed, accuracy, how each one fit into what we'd already built, what we'd have to change. By the end we had a clear recommendation.

Then we went to implement it and discovered the decision had already been made. Someone had built the whole thing — the chosen approach, the abstraction layer, the caching, even the tests — and it was sitting in an unreviewed queue, waiting.

For a moment that felt like wasted effort. All that research, and the answer was already there.

But something shifted when we started reading through what had been built. Because we'd just spent time understanding *why* one approach was right — what made it fit, what risks it carried, what you had to be careful about when using it — we weren't reading the code cold. We were reading it with a mental model of what could go wrong.

And that's when we found it.

The implementation was doing something that looked completely ordinary: taking names and descriptions that users had entered into the system, and including them in messages sent to the AI service. Perfectly sensible on its face. But those user-entered strings were going in unsanitized — raw, unfiltered, capable of containing anything. Someone who understood how these AI services work could craft an input that didn't just get *processed* by the AI, but actually *redirected* it. Changed its instructions. Made it behave in ways it wasn't supposed to.

It's the kind of thing that's easy to miss in a code review if you're only asking "does this work?" It worked fine. Every test passed. The system did exactly what it was designed to do.

But the research had made us ask a different question: *what does this system trust?* And the answer was: too much.

This is the part worth sitting with. The research didn't become redundant when we discovered the decision was already made. It became the lens we needed to evaluate that decision properly. Understanding the *why* behind a choice — what properties make it right, what failure modes it introduces — is exactly what lets you spot where an implementation has quietly left a door open.

There's a general pattern here. When you're reviewing something that someone else built, functional correctness is table stakes. The deeper question is whether the thing was built with an accurate model of how it could be misused. That question is almost impossible to answer without first understanding the domain well enough to imagine the misuse in the first place.

The research that felt like it arrived too late turned out to have arrived right on time.

