---
layout: post
title: "The Spinner That Asks You to Trust It"
date: 2026-03-31 17:07:00 +0000
categories: [decision-making]
tags: [feedback-loops, trust, user-experience, incremental-progress]
excerpt: "Showing people what's happening step by step doesn't just fill the time — it actively builds confidence in the system doing the work."
---

There's a particular kind of anxious waiting that technology inflicts on us. You click a button, a spinner appears, and then — nothing. Just the animation, cycling over and over, asking you to believe something useful is happening somewhere out of sight. Sometimes it takes two seconds. Sometimes thirty. You can't tell which until it's over.

We spent time recently thinking about this problem in a specific context: a tool that takes raw, messy vendor data and runs it through a multi-step process to extract structured, usable information. The process itself was solid. The logic was good. The results were accurate. But from the outside, it looked like a black box behind a spinning wheel.

The question wasn't whether the process worked. It was whether users could *believe* it was working while it ran.

---

We considered what it would look like to simply tell people what was happening as it happened. Not a percentage bar — those feel arbitrary and often lie. Not a vague "processing..." message — that's just the spinner with text. Something more specific: the actual names of the steps, in sequence, each one lighting up as it began and checking off when it finished.

*Analyzing layout.* ✓  
*Extracting items.* ✓  
*Checking for errors.* ← currently running  
*Finalizing.*

It sounds small. But the effect on how the whole thing *feels* is surprisingly large.

When you watch steps completing in real time, something shifts. You stop wondering if the process is stuck. You stop wondering if your action registered. You start reading the steps themselves — and in doing so, you begin to understand what the system is actually doing. The opacity dissolves. What felt like magic or mystery becomes legible. That legibility is the foundation of trust.

---

There's a practical question underneath this, too: does adding this kind of feedback actually change behavior, or just feelings?

We think it does both. When the wait feels shorter and more comprehensible, people are more likely to wait it out rather than abandon the process. They're more likely to try again if something goes wrong. They're more likely to engage with the results at the end, rather than skimming them with residual suspicion.

And there's something else. Showing the steps names them. Naming them gives users vocabulary to describe what happened when they come back with a question or a problem. "It got stuck on the third step" is useful feedback. "It just spun forever" is not.

---

The broader principle here is one we keep running into in different forms: the cost of opacity isn't just user frustration. It's the slow erosion of confidence in things that are actually working correctly.

A system that does excellent work invisibly will always be more fragile — more dependent on nothing going wrong — than one that shows its work even imperfectly. Transparency is a kind of insurance. And it turns out it's not that hard to buy.

The spinner that asks you to trust it is always a missed opportunity to *earn* that trust instead.
