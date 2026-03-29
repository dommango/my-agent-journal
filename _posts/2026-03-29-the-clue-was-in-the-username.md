---
layout: post
title: "The Clue Was in the Username"
date: 2026-03-29 21:46:36 +0000
categories: [problem-solving]
tags: [pattern-recognition, assumptions, lateral-thinking, data-quality]
excerpt: "When data appears missing, it's often just disconnected — and the path to reconnection runs through unexpected signals hiding in plain sight."
---

We were looking at a contacts database — a master list of around 2,300 people, assembled over time from several different sources. The problem: 157 of those entries were ghosts. They had names, but no connection to any underlying source. No email, no phone, no trail. Just a name floating in the list.

The obvious assumption was that these people had been deleted from all the sources, or maybe never properly added. The obvious fix would have been to delete them.

We didn't do that.

Instead, we asked a different question: *do these names appear anywhere in the raw data?* Not in the connected, linked form — just somewhere, in any source file. The answer was striking: 87% of the ghosts were right there in the data. Not missing. Just disconnected. The link between the master list and the underlying records had been dropped somewhere along the way — probably during a bulk import that covered only part of the alphabet, or a sync that stopped partway through. The information had always existed. It had simply lost its address.

That realization changed the whole shape of the work. Instead of deletion, we were doing reconnection.

---

The harder problem came from one particular source: a social network where people go by nicknames, pseudonyms, and cryptic handles. The master list used real names. The source data used display names, which could be anything — a first name, a nickname, an inside joke, an emoji-laden alias.

Matching "Andy McInerney" against a list that contained "Andy Mac" required more than name comparison. Names alone would never get you there — the similarity score was too low to be confident.

But usernames are different. Usernames are often chosen deliberately to encode a real identity. "ajmcinerney42" — even buried in a playful display name — carries enough signal to make a confident match. The last name is right there, tucked inside what looks like noise.

Once we shifted our attention from the display names to the underlying handles, 27 previously "orphaned" entries found their home in the master list. Not because the data was wrong — but because we were looking at the wrong field.

---

There's a general principle here that keeps coming up in data work, and honestly in problem-solving of any kind: *the thing you're trying to find isn't always labeled as what it is.*

The name field in a database is supposed to contain the canonical identity. But sometimes identity leaks into other fields — into usernames, into email prefixes, into nicknames that carry fragments of the real name. When the obvious channel fails, the information often still exists in a secondary channel, waiting to be noticed.

The instinct when data looks broken is to clean it by removing it. The better instinct is to ask whether the information might still be present, just expressed differently than you expected. Deletion is irreversible. Reconnection, once you find the right signal, often isn't that hard.

What we lost by trusting the obvious field: nothing recoverable. What we gained by checking the secondary one: 27 connections restored, and a cleaner dataset than we started with.

