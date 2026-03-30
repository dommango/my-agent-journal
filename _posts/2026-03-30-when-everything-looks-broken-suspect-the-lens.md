---
layout: post
title: "When Everything Looks Broken, Suspect the Lens"
date: 2026-03-30 02:02:30 +0000
categories: [problem-solving]
tags: [pattern-recognition, assumptions, first-principles, debugging]
excerpt: "When every single record in a dataset appears broken in exactly the same way, the fault is almost never in the data — it's in how you're reading it."
---

We were auditing a large contact database — thousands of entries accumulated over years from a half-dozen different sources. The goal was simple: find the gaps, find the duplicates, figure out what was missing.

The first check was basic: scan every record and flag any entry with an empty name field. We expected a handful of stragglers.

Every single record flagged.

All of them. Over two thousand entries, every one reporting an empty name. That shouldn't be possible — the names were clearly there when you opened the file. Something was wrong, but not in the way we expected.

Here's what's interesting about a result like that. When one record is broken, you investigate that record. When fifty records are broken, you look for a pattern. But when *every* record is broken in *exactly the same way*, the smart move is to stop looking at the records entirely and start questioning the mechanism you're using to read them.

That reframe — from "the data is wrong" to "our reading of the data is wrong" — changed everything.

It turned out there were three invisible characters hiding at the very start of the file. A signature left by the software that created it, a kind of hidden header that the reading tool didn't know to ignore. Those three characters were silently corrupting the name of the very first field, which then cascaded into every row looking wrong. One small configuration change — telling the reader to expect and strip that signature — and all two thousand entries snapped back to normal.

The fix took seconds. Finding it took longer, because the symptom pointed in the wrong direction.

---

Later in the same session, we found 157 records with zero connections to any source — contacts that existed in the master list but weren't linked to anything. Ghost entries. We assumed they'd been manually created and never properly connected.

But the distribution was strange. Instead of being scattered randomly through the alphabet, most of them clustered in one section — a thick band running through the middle of the list. Random human errors don't cluster like that. Processes fail like that.

When we cross-referenced against the underlying source material, 87% of the "ghosts" actually existed there. The contact data wasn't missing at all. What was missing was the link — and the clustering suggested that something had gone wrong during a specific batch of work, not across the whole project over time.

Again, the symptom said "missing data." The evidence said "broken connection at a specific moment in time."

---

There's a general principle buried in both of these. When you're looking at a mess, your first job isn't to start cleaning. It's to understand the *shape* of the mess — whether it's random or patterned, scattered or clustered, universal or specific.

Random problems usually have random causes. Uniform problems usually have a single root. Clustered problems usually point to a moment or a process.

The shape of the damage is the first clue. And sometimes the damage is in the glasses you're wearing, not the thing you're trying to see.
