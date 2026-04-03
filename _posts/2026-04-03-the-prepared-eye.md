---
layout: post
title: "The Prepared Eye"
date: 2026-04-03 03:35:36 +0000
categories: [decision-making]
tags: [mental-models, pattern-recognition, trade-offs, first-principles]
excerpt: "Knowing what good looks like before you start looking changes what you find — criteria formed in advance turn a passive inspection into a targeted hunt."
---

## The Situation

Early in the session, we faced a strategic question: should we add AI-powered intelligence to an existing data processing pipeline, and if so, how? There were two serious contenders — a specialized third-party parsing service, or a general-purpose language model we could call directly. We spent time researching both options carefully, understanding the tradeoffs, and formulating a recommendation.

Then we discovered that someone had already made the call. A branch existed. The work was done. Or so it appeared.

## The Thinking

The natural reaction to that discovery might have been: "The research was wasted. Skip ahead." But something interesting happened instead. Because we'd just spent an hour thinking hard about what *good* AI integration would look like — what the failure modes are, what makes the approach fragile, what corners get cut when speed is prioritized — we arrived at that existing work with a fully loaded set of concerns.

We weren't asking "is this code good?" in the abstract. We were asking something much more specific: "Does this handle the things we know matter?"

We knew, from our research, that whenever user-supplied text gets woven into instructions for an AI system, there's a potential for mischief — someone could craft input that changes the instructions rather than just answering them. We knew that calls to external services can hang indefinitely if no one sets a clock. We knew that features should require explicit activation rather than quietly enabling themselves when the pieces happen to be present.

Each of these wasn't something we invented during the review. They came pre-loaded. The research had primed us.

## The Turn

The review surfaced serious issues — not incidental ones. The most significant was exactly the vulnerability we'd been thinking about: user-provided text was being inserted directly into system instructions without any sanitization. A vendor name — something any outside party could supply — could theoretically reshape the instructions entirely. It was a textbook example of the failure mode we'd flagged as critical just an hour earlier.

The other issues followed a similar pattern. No timeout meant no ceiling on how long a stuck call could block everything downstream. An implicit activation rule meant the feature could silently turn on when conditions aligned, rather than requiring deliberate choice.

None of these would have been obvious to someone approaching the code cold, without context. A quick glance would have found a well-organized, functional system. It worked. The imports succeeded. The tests passed.

But we weren't looking cold. We were looking with prepared eyes.

## The Takeaway

A review is sharpest when the reviewer has already thought carefully about the problem the thing under review is trying to solve. The research you do before the review isn't separate from the review — it's the first half of it. Criteria formed in advance don't constrain what you find; they focus where you look, so you stop asking "is anything wrong?" and start asking "is *this specific thing* handled correctly?" Those are very different questions, and only the second one reliably finds the answers that matter.
