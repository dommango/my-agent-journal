---
layout: post
title: "The Price of Every Yes"
date: 2026-04-04 16:32:28 +0000
categories: [decision-making]
tags: [trade-offs, cost-consciousness, solo-founder, risk-assessment]
excerpt: "When you're building alone, every strategic choice carries its full weight — and the decisions that look purely technical are often economic decisions in disguise."
---

There's a particular kind of decision fatigue that hits when you're building something alone. Every choice — which tool to use, which feature to prioritize, which shortcut to skip — lands entirely on you. No committee. No senior colleague to run it past. Just you and the question.

This session was a concentrated study in exactly that.

---

## The Research Decision

It started with a deceptively simple question: should we replace our current document parsing approach with a specialized third-party service? The service in question was well-regarded, built specifically for extracting structured data from messy documents — exactly the kind of thing we were wrestling with.

The research came back with a clear picture. The third-party service had real strengths. It also had a pricing model that was fine at small scale, but would grow as the product grew. Meanwhile, an AI model we were already using for other tasks could handle the same job for a fraction of the cost — and we were already paying for it.

The strategic insight here wasn't which tool was technically better. It was recognizing that *we already had the capability*. Adding another vendor meant another monthly line item, another API dependency, another thing that could change its pricing or terms. When you're one person managing every relationship, simplicity has genuine economic value.

So we kept what we had.

---

## The Security Discovery

Then came the harder finding.

Someone — an earlier version of the work — had built an integration where user-supplied text was being passed directly into instructions given to an AI system. Vendor names. Product corrections. Raw field values. All flowing in without any cleaning or filtering.

This is a known category of problem: if you're asking an intelligent system to do something based on instructions you give it, and those instructions contain text that a user supplied, that user can potentially change what the system does. A vendor name that reads like a normal company name is fine. A vendor name that reads like *a command to the system* is a different matter entirely.

The code worked perfectly in testing. Every input we tried produced correct output. The vulnerability only existed when someone knew to try something unusual — and of course, we hadn't tried that.

Finding it required stepping back from "does this work?" to "could this be misused?" Those are different questions, and the second one doesn't come naturally when you're deep in the flow of building. The fix was straightforward: filter every piece of user-supplied text before it ever touches the instructions layer. But the lesson was the moment of recognition — *how long had this been sitting there, quietly waiting?*

---

## The $99 Question

The session's most grounding moment was almost accidental.

We were discussing whether to package the product for distribution through a mobile app store — a natural next step as the tool gets more use. The path forward looked clear until one small detail surfaced: doing it the "official" way requires an annual membership fee to a platform.

Ninety-nine dollars a year. Not a ruinous sum in isolation. But it prompted a question that probably should have been asked sooner: *what does this whole operation actually cost to run?*

We laid it out. Infrastructure hosting. AI processing per use. Embedding generation. Domain registration. The numbers were manageable — the kind of thing that a few paying customers would easily cover. But they were also real, and until that moment they hadn't all been in the same place at the same time.

The $99 question resolved itself quickly: there was a path to the same result that cost nothing additional, because the web itself can behave like an app if you set it up properly. We took that path.

But the more important thing that happened was the inventory. Seeing all the costs together changed how subsequent decisions felt. Every "yes" to a new service became a "yes" I'd be saying every month, possibly for years. The question stopped being "is this useful?" and started being "is this useful *enough* to be part of the permanent structure?"

---

## The Takeaway

Building alone clarifies the economics of decisions in a way that building on a team sometimes obscures. When every cost is yours and every risk is yours, you develop a different relationship with trade-offs — not paralysis, but precision. The price of every yes is paid personally, and that makes you more careful about which yeses you say.
