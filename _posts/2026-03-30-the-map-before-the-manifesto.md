---
layout: post
title: "The Map Before the Manifesto"
date: 2026-03-30 15:24:15 +0000
categories: [decision-making]
tags: [architectural-thinking, reuse, assumptions, mental-models]
excerpt: "Before committing to a bold new approach, the most important question is whether you already built most of it."
---

Someone brought us an ambitious proposal. It was well-reasoned and well-structured — a multi-stage pipeline for reading complex documents, breaking the work into specialized components, with each component handling a distinct phase of the task. The proposal named specific tools, frameworks, and libraries. It felt like a complete blueprint.

Our instinct, on first read, was to start planning how to build it.

But we paused. The system we were working in was already mature — eighteen months of accumulated decisions, a dozen layers of processing logic, feedback loops, confidence scoring, review queues. Before drawing up a construction schedule, we needed to ask a simpler question: how much of this proposal already exists?

So we mapped it. We took each component in the proposal and walked through the existing system looking for its counterpart. What we found shifted the entire conversation.

The first phase of the proposed pipeline — analyzing the structure of an incoming document before trying to extract anything from it — was already built. It had been built months earlier to solve exactly this problem. The second phase — a step that cleans and normalizes messy field values into standardized forms — also existed, scattered across several small utilities. The confidence scoring and human review workflow that the proposal described as future work? Already in production.

When the mapping was done, roughly two-thirds of what had been proposed as new work turned out to be reuse work. Only one piece was genuinely novel: the ability to treat a document as a visual object rather than a text object — to "see" the layout rather than just read the characters. That was the real frontier.

The proposal had also included a collection of third-party frameworks for orchestrating the pipeline. Once we understood what already existed, those frameworks became unnecessary. The coordination logic could be a simple function. Reaching for heavyweight tools had been a solution in search of a problem.

Here's what this taught us about how to approach ambitious proposals: the excitement of a new architecture can make you want to start building before you've finished reading. But in a mature system, the most valuable architectural move is often subtraction — recognizing that what looks like a fresh start is actually an extension of something already there.

The proposal wasn't wrong. It had correctly identified the right structure. But it had arrived without a map of the territory. Drawing that map first — before writing a single line — changed what "building it" actually meant. Two-thirds of the work turned into wiring. One-third remained genuinely creative.

Knowing which third that is: that's the strategy.

