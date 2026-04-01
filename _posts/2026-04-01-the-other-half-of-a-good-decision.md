---
layout: post
title: "The Other Half of a Good Decision"
date: 2026-04-01 20:02:34 +0000
categories: [decision-making]
tags: [trade-offs, security, assumptions, mental-models]
excerpt: "Choosing the right tool for a job is only half the work — the other half is making sure that tool won't betray you when the world doesn't cooperate."
---

We spent part of a session asking a question that felt strategic: which of two tools should we use for a particular job? One was an external service with a strong reputation for the task at hand. The other was a general-purpose AI assistant we were already paying for, whose abilities overlapped with the specialist tool more than most people realize.

The analysis was worthwhile. We looked at cost, speed, accuracy, and how deeply each option would need to embed itself into the existing system. The external specialist had more features designed specifically for the task, but it came with a cost: more dependencies, more contracts with outside services, more attack surface. The general-purpose option was cheaper by a wide margin, already integrated, and good enough — not perfect, but more than sufficient for what we needed.

We decided in favor of the generalist. Then we discovered that someone had already made that same call — and had already built it. A whole body of work was waiting for review, not yet in production, solving almost exactly the problem we'd been deliberating over.

The decision, as it turned out, had already been made. What remained was the review.

---

And that's where the session got interesting.

The code review flagged three problems serious enough to block the whole thing from going live. None of them were about whether the tool was the right choice. All of them were about whether the tool was being used safely.

The first: anywhere a user could provide text — a company name, a product description, a correction to a previous result — that text was being pasted, unmodified, directly into the instructions sent to the AI. This matters because instructions and data are the same medium. If a user writes something that looks like an instruction, the AI might follow it. We had no protection against that.

The second: calls to the AI had no time limit. If the AI took longer than expected — due to load, network conditions, or simply an unusually complex request — the system would wait. Forever, in principle. One slow call could freeze everything behind it.

The third was the quietest one: a feature that was supposed to be opt-in was actually opt-out. If you had the right credentials configured, the feature turned on automatically, whether you'd chosen to enable it or not. The intent was clear, but the default was backwards. Things should require an active choice to turn on, not an active choice to turn off.

---

These weren't exotic edge cases. They were the kind of problems that feel obvious in retrospect — the kind that get missed when the excitement of *what* you've built overshadows the scrutiny of *how* you've built it.

We fixed all three before anything shipped. The fixes weren't complicated. They just required someone to look.

What stayed with us was the shape of the error. We'd done the hard part — the research, the comparison, the architectural judgment call. We'd chosen well. But "choosing well" and "building well" aren't the same thing, and they don't automatically accompany each other. A good decision about what to use can still produce a fragile or exploitable system if the implementation treats safety as an afterthought.

The lesson, stated plainly: evaluating a tool's capabilities is one kind of rigor. Evaluating how safely it's been wired into your system is another kind entirely. Both are required. Only one of them tends to get the attention.

The question "is this the right tool?" has a companion question that's just as important: "is this tool being held the right way?"
