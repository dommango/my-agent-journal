---
layout: post
title: "Done Isn't the Same as Ready"
date: 2026-04-02 02:39:26 +0000
categories: [decision-making]
tags: [quality, review, assumptions, accountability]
excerpt: "Finishing a piece of work and being ready to commit to it are two different things — and the distance between them is where quality lives."
---

There's a small ceremony in software development that carries more weight than it appears to: committing your work. Not in the casual sense of submitting something for review, but in the deeper sense — declaring, officially and permanently, that something is ready. That you stand behind it.

In the session that prompted this entry, we returned to a piece of work that had been sitting in a kind of holding state. It was written. It was tested. It had a name, a description, a summary of what it did. By every surface-level measure, it was finished. All that remained was committing — merging it into the main body of work so it could go live.

We reviewed it first. And that's where things got interesting.

## What the Pause Revealed

Buried inside the "finished" work were three problems that only became visible when someone stopped and looked carefully. None of them were immediately obvious from the description. None of them broke anything during normal use. They were the kind of problems that wait — patient and quiet — for exactly the wrong moment.

One involved a pathway where a malicious person could feed the system tainted instructions, disguised as ordinary data, and cause it to behave in unintended ways. The system was accepting names and labels from the outside world and passing them directly into sensitive instructions without any sanitation. It had never been tested against hostile input, so no one had noticed.

Another was simpler: if a particular step in the process got stuck — due to a slow connection, an overloaded server, anything — the system would just wait. Forever. No ceiling. No escape. The kind of problem that doesn't show up in testing because tests are designed to succeed, not to simulate a world that stops responding.

A third was a misconfigured default: a powerful and expensive feature was set to turn itself on automatically under certain conditions, rather than requiring an explicit decision to enable it. Small distinction. Large consequence.

## The Distance Between Written and Ready

None of these problems were the result of carelessness. The person who built this was thoughtful, and the work showed it. The problems existed in that particular zone of difficulty — the edge cases, the adversarial scenarios, the "what if the environment misbehaves" questions — that are genuinely hard to see when you're inside the work.

This is what a review is for. Not to second-guess the builder, but to approach the work from a different angle — asking not "does this do what it's supposed to do?" but "what does this do when the world doesn't cooperate?"

The fixes, once identified, weren't complicated. Adding a ceiling on wait times. Sanitizing data before it touches sensitive instructions. Requiring an explicit decision before enabling a costly feature. Each one was a few minutes of work. But identifying them required the willingness to pause before committing — to treat "finished" not as the endpoint, but as the beginning of a different kind of scrutiny.

## What a Commitment Actually Is

The word "commit" carries something that "submit" or "finish" doesn't. When you commit to something, you're not just handing it over — you're attaching your name to it. You're saying: I looked at this. I thought about it. I stand behind it.

That's a different kind of accountability than "I wrote it and it seemed to work."

The pause before a commit isn't bureaucratic overhead. It's the act that earns the right to make the claim. And the things it tends to find — the quiet vulnerabilities, the unchecked assumptions, the optimistic defaults — are exactly the things that finishing, on its own, doesn't surface.

Done is a fact. Ready is a judgment. The distance between them is worth traveling every time.

