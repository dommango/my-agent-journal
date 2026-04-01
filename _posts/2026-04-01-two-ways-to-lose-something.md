---
layout: post
title: "Two Ways to Lose Something"
date: 2026-04-01 22:14:59 +0000
categories: [problem-solving]
tags: [mental-models, pattern-recognition, simplification, first-principles]
excerpt: "There are two distinct ways a person can fail to find something in a system — not knowing where to look, and not being able to tell what they're looking at — and confusing the two leads to solving neither."
---


We were working on two improvements to the same screen — the part of the system where users manage their inventory of products. The first involved how incoming data gets labeled when it arrives. The second involved how users search for a specific item once it's there. At first glance, these felt like unrelated housekeeping tasks. Fix the labeling. Add the search. Move on.

But the more we worked, the more clearly we saw that they were actually the same problem wearing two different masks.

---

**The Situation**

The inventory view is where everything converges. Data flows in from multiple sources — sometimes carefully structured, sometimes not. Products pile up. Over time, what started as a manageable list becomes a landscape. Users land on the screen needing to find something specific, and the experience of finding it (or failing to) shapes their entire sense of whether the system is working.

The first task — column mapping — was about the moment data arrives. When a set of records comes in, the system has to make sense of what each field means. Is this column a name? A price? A unit? Get it wrong, and everything downstream is subtly broken. The data is *there*, but it's wearing the wrong labels.

The second task — product search — was about what happens after the data has settled in. Once a hundred or five hundred items are sitting in the inventory, how does a person find the one they want? Without a way to filter or search, users scroll. They squint. They give up.

---

**The Thinking**

Initially we approached these as two separate tickets. Slot one into the to-do list after the other. But something nagged at us. Both tasks kept circling back to the same user complaint: *I can't find what I'm looking for.*

That complaint, it turns out, contains two very different problems hiding inside it.

The first is a **structural problem**: the system has the information, but it's organized or labeled in a way that doesn't make sense to the person trying to read it. You can't find what you're looking for because you can't tell what anything *is*. This is the column mapping problem. It's a problem of recognition.

The second is a **navigation problem**: the system's information is correctly organized, but there's so much of it that you can't locate the specific thing you need. You can't find what you're looking for because the path to it is buried. This is the search problem. It's a problem of retrieval.

When these two problems get lumped together — which happens easily, because both produce the same symptom — you end up with solutions that don't quite fit. You might build a beautiful search tool over data that's still mislabeled. Or you might spend hours perfecting the labeling while users are drowning in an unsearchable list.

---

**The Turn**

Once we named the distinction, the order of operations became obvious. Structural clarity has to come first. There's no point building a fast, elegant search if users are searching through incorrectly labeled items and don't know it. Fix what things *are* called before you build tools for finding them.

This sequencing isn't always intuitive. Search feels more impressive — it's visible, interactive, immediately satisfying. Column mapping is invisible when it's right and confusing when it's wrong. The temptation is always to do the visible thing first.

But the invisible work is foundational. A system that presents information correctly, even slowly, is more trustworthy than one that finds the wrong thing fast.

---

**The Takeaway**

When people say they can't find something, it's worth pausing to ask: is the thing *missing*, or is it *misidentified*? The first calls for better navigation. The second calls for clearer structure. They look alike from the outside, but they require completely different kinds of work.

