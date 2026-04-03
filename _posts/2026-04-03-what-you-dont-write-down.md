---
layout: post
title: "What You Don't Write Down"
date: 2026-04-03 14:11:51 +0000
categories: [problem-solving]
tags: [automation, mental-models, assumptions, failure-modes]
excerpt: "Instructions written for a person can safely leave half the thinking implicit — but the same instructions handed to an autonomous system will fail at every gap you didn't notice you left."
---

We had set up a system to do a routine job automatically — check for updates each morning, apply them, and file the results for review. It had been working reliably for days. Then it missed one.

The job ran. The logs said it ran. But the output wasn't there. No error, no alarm. Just silence where there should have been work.

We dug in. And what we found wasn't a bug in the usual sense — it wasn't a broken piece of code or a failed connection. It was five separate gaps in the instructions we had written for the system. Each one was a place where we had assumed the machine would think the way a person would, and it didn't.

The first gap: we had told the system to note when something was new and label it with the version it came from. But we hadn't said *which version* — the one where the thing originated, or the one the system was currently working from. A person reading those instructions would never ask the question. It's obvious. The machine picked one answer, silently, and it was the wrong one.

The second gap: we had told the system to check whether there was anything new to do, and if not, to stop. But the check was too simple — it looked at a single indicator rather than at the actual content. The indicator was slightly wrong (because of gap one), so the system saw "nothing new here" and stopped, even though there was plenty of work to do.

The third gap: we had told the system to review its own work and fix anything wrong, repeating until everything passed. That's exactly what a diligent person would do. But a person knows when to stop. They have a gut sense of "I've looked at this three times and I'm going in circles." The machine had no such sense. With no explicit limit, it could loop indefinitely — and very likely did, which is why the run appeared to complete but produced nothing.

The other two gaps were similar: places where we assumed the system would handle edge cases that any person would navigate on instinct — what to do if a branch already exists, what to do if a fetch returns nothing.

None of these were surprising in hindsight. But none of them had occurred to us when we wrote the instructions, because when we imagined following those instructions, we imagined ourselves following them. And we would have handled every one of these situations without thinking, because humans carry enormous amounts of implicit judgment that never makes it onto the page.

The lesson isn't that automation is fragile. It's that the act of writing instructions for something that can't improvise forces you to make explicit every piece of reasoning you'd normally leave in your head. Every "obviously" and "of course" and "use your judgment" becomes a failure point.

The fix wasn't complicated. We added caps, clarified ambiguities, and told the system what to do when things went sideways rather than assuming it would figure it out. The instructions got longer, but they got honest — they now matched what we actually wanted instead of what we assumed went without saying.

When you automate something, you're not just offloading work. You're writing a complete theory of how that work should be done — including all the parts you've never had to articulate before.

