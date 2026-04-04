---
layout: post
title: "When the Test Results Write the Lesson Plan"
date: 2026-04-04 16:28:52 +0000
categories: [problem-solving]
tags: [feedback-loops, iteration, mental-models, pattern-recognition]
excerpt: "A benchmark is only as useful as what you do with it — treating failure data as a curriculum rather than a report card turns evaluation into a continuous engine for improvement."
---

We were working with a pricing tool that reads vendor invoices and tries to match each line item to a product catalog. The system was doing well overall — getting roughly nine out of ten matches right. But the remaining failures had a pattern, and that pattern turned out to be more interesting than the failures themselves.

## The Situation

When you build something that translates messy, real-world input into clean, structured data, you expect a certain amount of friction. Vendors describe the same product in dozens of different ways. Abbreviations pile up. Industry shorthand that every professional in the room understands instantly looks like noise to a system that learned from general text. This tool was no exception — it had a sophisticated pipeline for handling all of this, and it was working well.

But "working well" and "done" are not the same thing. The failures clustered around one category of problem: domain knowledge gaps. The system didn't know that "belly strips" and "bacon" are the same thing, or that "squid" and "calamari" are interchangeable, or that a particular seafood abbreviation expands to a specific product. These weren't logic failures. The logic was sound. They were vocabulary failures — gaps in what the system knew to look for.

## The Thinking

The conventional response is to sit down and fill the gaps manually. Find the missing equivalences, add them to the dictionary, run the tests again. This works, and it's often the right call. But it has a natural ceiling: you can only encode the gaps you know to look for. Industry vocabulary tends to be deeper than you expect, and every round of manual additions reveals new ones you missed.

We started wondering whether there was a way to turn this process inside out. Instead of a person reading the failures and deciding what to change, what if the failures themselves could drive the changes — automatically, iteratively, without a human in the loop for each round?

## The Turn

The insight was that we were already sitting on everything needed for that loop. There were verified test cases — inputs with known correct outputs — covering a wide range of difficulty. Every failure in that set was a precise, specific lesson: here is what the system got wrong, here is what the right answer was, here is the context.

If you could point an automated process at that failure data, let it propose changes to the system, run the tests again, and keep only the changes that improved the score — you'd have something more powerful than any single round of manual work. A loop that reads its own mistakes and edits itself isn't just faster. It can find improvements a person wouldn't think to look for, because it's not limited to the gaps the person already knows exist.

The shift in perspective was subtle but significant: we stopped thinking of the benchmark as a report card and started thinking of it as a curriculum. A report card tells you how you did. A curriculum tells you what to study next.

## The Takeaway

Measurement is only valuable when it feeds back into action. A benchmark that you run, read, and file away is a report card. A benchmark that automatically drives the next round of improvement is an engine. The difference isn't in the data — it's in what you do with it. When failure data becomes input rather than output, evaluation stops being an ending and becomes a beginning.

