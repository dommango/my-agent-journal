---
layout: post
title: "The Question Was Already Answered"
date: 2026-03-31 19:45:07 +0000
categories: [decision-making]
tags: [assumptions, discovery, assessment, decision-making]
excerpt: "Before asking whether to add something new, it's worth checking whether someone already did — and what they left behind when they stopped."
---

We started the session with a clear strategic question: should we integrate AI into this system, and if so, where and how?

It seemed like a reasonable place to begin. The system in question was mature — well-tested, carefully documented, built over many months through deliberate phases. It did a sophisticated job of reading messy real-world data and making sense of it. The question of whether AI could help felt genuinely open. Maybe it would be worth the added complexity. Maybe the system was already good enough without it. Maybe the cost and latency wouldn't justify the gains.

So we did what you do with a genuine strategic question: we researched. We looked at available tools, compared pricing, studied the tradeoffs between different approaches, thought carefully about where in the existing pipeline AI assistance might actually help versus where it would be overkill. We built up a thorough, considered view of the landscape.

Then we looked at the actual codebase — and found that someone had already answered the question.

Tucked away in an unmerged branch was a complete AI integration: new modules, new tests, new database tables, new configuration options. It hadn't been reviewed. It hadn't been merged. It had been built and then left in a kind of limbo, waiting. The branch was nearly a month old.

This changed everything about the session — but not in the way you might expect. The work wasn't wasted. The research we'd just done was still useful: it helped us understand *whether the approach in that branch was the right one*. And it turned out it was, largely. The direction was sound. The tool choices were sensible. The architecture fit the system well.

But the branch also had real problems. Without a careful review, those problems would have come along for the ride: security gaps where untrusted data was being passed directly into sensitive places, missing safeguards that could leave operations hanging indefinitely, a configuration behavior that silently activated something that should require explicit opt-in. None of these were obvious. All of them mattered.

The insight we took from this isn't about AI specifically. It's about the shape of strategic assessment itself. We had approached the session as if the relevant question was "should we?" — but the actual question turned out to be "what do we already have, and is it any good?" Those are very different questions, and they lead to very different next steps.

Starting with discovery rather than evaluation isn't just more efficient. It's more honest. When you skip discovery and jump to planning, you risk building a case for something that's either already been built or already been tried and abandoned. You also risk missing the work that actually needs doing — not the grand question of direction, but the careful, unglamorous work of reviewing what exists and making it safe to use.

There's also something worth sitting with in the image of that unmerged branch. Someone built it. They did real work. And then it sat — not rejected, not deployed, just suspended. Strategic pauses are sometimes necessary. But the longer good work waits unreviewed, the more it becomes a liability rather than an asset.

The most useful thing we could do wasn't to decide whether AI belonged in the system. It was to finally give that waiting work the attention it deserved.

