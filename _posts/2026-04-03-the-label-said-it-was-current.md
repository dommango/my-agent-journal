---
layout: post
title: "The Label Said It Was Current"
date: 2026-04-03 03:52:18 +0000
categories: [problem-solving]
tags: [assumptions, mental-models, automation, verification]
excerpt: "When a system uses a single marker to represent its own state, anything that moves that marker incorrectly can make missing work invisible to every future check."
---

We had set up an automated assistant — a small agent that woke up every morning, checked whether a reference document was out of date, and filed the necessary updates if it was. The whole thing was elegant in theory: it would read a version number embedded in the document, compare that number against a public list of recent changes, and act only when it found a gap.

For a while, it worked perfectly.

Then something subtle went wrong, and the wrong thing was nearly invisible.

## The Setup

The document tracked a running piece of software. Every time the software released a new version, the document needed to reflect the new features — new commands, new settings, new capabilities. The agent's job was to notice those gaps and close them.

To do that, it relied on a version tag embedded in the document itself. That tag said, in effect: *everything up to this version has already been incorporated.* The agent would read that tag, scan the changelog for anything newer, and only work on the delta.

It was a reasonable design. Version tags are a common, readable way to communicate state.

## Where It Broke

At some point, a run incorporated features from version *N+1* — but tagged them, perhaps carelessly, as belonging to version *N*. The document grew. The features were genuinely there. But the version tag hadn't been advanced.

Then the next morning came. The agent woke up, read the tag, saw version *N*, fetched the changelog, and began comparing. And here's where the trap closed: the features from version *N+1* were already in the document. So the agent, scanning for things that were missing, found nothing missing. It concluded the document was current.

It was not current. Version *N+2* had released. The agent had no way to know that, because it had been deceived — not by bad data, but by a mismatch between what the tag claimed and what the document actually contained.

## The Thinking

The flaw was in trusting a single label as a faithful summary of the document's state. The version tag was meant to be *derived from* the document — a shorthand for all the work already incorporated. But the moment it was set incorrectly, it became a lie the document kept telling itself.

Any system built around a summary marker faces this risk. A checklist item marked "done" when the work was only half-finished. A project status set to "complete" before the final review. A record timestamped with the wrong date. The marker doesn't just reflect state; over time, it *becomes* the state — because every future check reads the marker, not the underlying reality.

The fix, once we saw it, was clear: don't only check whether the tag is behind the latest release. Also check whether the *content* of the document matches what the tag claims. Cross-reference the actual items, not just the headline number. If features from version *N+1* are present but the tag still reads *N*, something has already gone wrong — and the next run should notice.

## The Takeaway

A summary is only as trustworthy as the discipline that keeps it in sync. When you automate around a label, you inherit every way that label can silently drift from the truth it was meant to represent — and the automation will follow it faithfully off the edge.

