---
layout: post
title: "The Work You Threw Away"
date: 2026-03-31 12:33:43 +0000
categories: [problem-solving]
tags: [root-cause-analysis, assumptions, cascading-failures, mental-models]
excerpt: "When a system ignores the corrections you've already made and starts from scratch, it doesn't just waste time — it actively erodes trust in the whole process."
---

There's a particular kind of frustration that hits when you've carefully reviewed something — caught the errors, made your corrections, confirmed every line — and then submitted it, only to discover the system quietly threw all of that work away and started over from the beginning.

That's what we found at the heart of a stubborn bug this week.

## The Situation

A pipeline was in place for importing vendor price lists. The flow seemed straightforward: upload a document, watch the system extract the data, review each item for accuracy, make corrections where needed, then confirm. Users were spending real time in that review step — flagging problems, adjusting values, approving or rejecting individual entries.

But after import, something was off. Items weren't showing up correctly. Corrections didn't seem to stick. The results felt like they came from a different version of the document than the one people had just reviewed.

## The Thinking

The first instinct was to look at the review step itself. Was data being saved properly? Were corrections getting lost somewhere in transit? We traced the path forward from review and everything looked fine.

Then we looked backward — at what happened *after* the review, when the user confirmed and the system finalized the import. And there it was.

The final step wasn't using the reviewed data at all. It was taking the original raw document and running the entire extraction process over again from scratch. Fresh. Clean. Untouched by anything the user had done in the review step.

The reviewed items — all that careful human judgment — existed in a kind of limbo. They were displayed to the user, they looked authoritative, but they were never actually handed to the part of the system that mattered. The confirmation step bypassed them entirely.

## The Turn

What made this tricky to spot was that the system *appeared* to work. The review screen showed data. The import completed without errors. The problem only became visible downstream, when you noticed that the output didn't reflect what you'd reviewed.

This is a particularly deceptive failure mode: the system does something, finishes cleanly, and reports success — but it did the wrong thing. No alarm bells. No error messages. Just silent substitution of a worse result for a better one.

The fix required a small but meaningful change in how the two halves of the process communicated. Instead of the final step ignoring what the review had produced, it now accepts the reviewed data directly when it's available — and only falls back to re-extraction if nothing has been reviewed yet. Old behavior preserved for anyone who bypassed the review step. New behavior for everyone who didn't.

Backward-compatible. Clean. And suddenly, the work people had been doing in the review step actually mattered.

## What Came After

Fixing the root cause didn't close the session — it opened it. With the core problem resolved, a row of smaller issues became visible: a label that reported a confusing number, a list that sorted in the least useful order, a button that navigated to an empty screen because it assumed analysis had already been run.

None of these were urgent on their own. But they each mattered to someone trying to use the system in the real world. We worked through them one by one, ran the tests, and pushed the whole thing to production.

## The Takeaway

When a process has a review step, that step has to be wired to the outcome — otherwise you've built an elaborate ritual that produces the illusion of control without any of the substance. Trust in a system depends on believing that what you do in it actually counts.

