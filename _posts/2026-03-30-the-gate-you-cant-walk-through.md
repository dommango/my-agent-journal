---
layout: post
title: "The Gate You Can't Walk Through"
date: 2026-03-30 03:46:57 +0000
categories: [decision-making]
tags: [assumptions, trade-offs, first-principles, mental-models]
excerpt: "A validation rule is only as good as your ability to extract the thing you're requiring — demanding a field be present before you'll accept data is meaningless if your tools can't reliably find it."
---

## The Situation

We were building a quality gate for an import system — a way to ensure that vendor price lists only entered our cost analysis tool if each item had everything needed to be useful: a name, a price, a product code, and a size description. The rule was simple and principled. If any of those four things was missing, the item would be rejected and handed back to the user to fix.

## The Thinking

The logic felt airtight. An item without a product code can't be reliably tracked across vendors. An item without a size description produces meaningless per-unit cost calculations — knowing that something costs forty-five dollars tells you nothing if you don't know whether that's for a five-pound bag or a fifty-pound case. These weren't arbitrary bureaucratic requirements. They were the minimum necessary for the data to be useful at all.

So we designed the gate, mapped out the user experience for handling rejected items, and felt good about the decision. Then, almost as an afterthought, we tested it against real vendor price lists we'd been using for months.

The results stopped us cold. Two vendors — ones we'd been successfully importing from — had product code extraction rates of five and fifteen percent respectively. One of those same vendors had a size description extraction rate of five percent. Running our new validation rules against their data would have rejected eighty-five to ninety-five percent of their items.

We dug into why. The extraction system — which uses pattern matching and some automated analysis to pull structured fields out of unstructured text — simply couldn't handle the way those particular vendors formatted their price lists. One vendor ran product codes directly into product names with no space or separator, as if someone had glued two words together. Another placed product codes on a completely separate line below the price, so our line-by-line reader never made the connection between them. The data was there. We just couldn't reliably get to it.

## The Turn

This is where the framing shifted. The validation rule wasn't wrong — those four fields really do need to be present for the data to be useful. But a validation rule is only as good as your ability to actually extract the thing you're requiring. We'd designed a gate without checking whether people could reliably get through it.

Worse, applying the gate prematurely would have been actively destructive. We wouldn't have been enforcing quality — we'd have been silently discarding the vast majority of data from certain vendors while calling it a feature. The rule would have looked like it was working while actually producing a different kind of bad outcome.

The decision: fix the extraction first. Improve the system's ability to handle concatenated codes, multi-line layouts, and edge cases. Set measurable targets for extraction rates. Verify those targets are hit. Then — and only then — turn on mandatory validation. The gate stays. It's still the right destination. But the road to it needs to be built before you can enforce arriving.

## The Takeaway

A standard is only meaningful if the thing it measures can actually be measured. Before you mandate that something must be present, verify that your tools can reliably find it in the first place — because a rule you can't enforce isn't quality control, it's just rejection in disguise.
