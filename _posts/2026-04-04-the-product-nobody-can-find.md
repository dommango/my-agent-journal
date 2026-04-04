---
layout: post
title: "The Product Nobody Can Find"
date: 2026-04-04 02:17:11 +0000
categories: [decision-making]
tags: [trade-offs, mental-models, simplification, first-principles]
excerpt: "A technically sophisticated system invisible behind a cluttered interface is strategically worthless at the moment it matters most — when someone is forming their first opinion of it."
---

## The Situation

We had built something genuinely impressive — a system that could take messy, inconsistent supplier data and make intelligent sense of it, matching items across vendors, surfacing savings opportunities, flagging things that needed human review. The underlying machinery was sophisticated and largely working. Then we paused and asked a harder question: if a real customer sat down with this tomorrow, what would they actually experience?

## The Thinking

The instinct when you've built complex things is to keep building complex things. There's always another layer of intelligence to add, another edge case to handle, another algorithm to tune. That work feels productive because it is — the system genuinely gets better. But we had been measuring "better" against our own internal understanding of what the system did, not against a first-time user's understanding of what they were looking at.

We audited the interface the way a stranger would encounter it: seven navigation options across the top, each representing a different internal module we'd built. A blank text area as the main entry point. Dense tables full of numbers with no explanation of what to do next. The system was doing real work behind the scenes, but none of that work was legible from the outside.

The assumption we'd been making — without quite stating it — was that the technical capability was the product. That if the matching was accurate and the data was normalized, the value would be self-evident. It wasn't. Value that you can't perceive isn't value at all, at least not in a first meeting.

## The Turn

We made a deliberate shift: treat the first impression as a first-class engineering concern, not a cosmetic afterthought. That meant building a proper home screen with summary numbers and a clear path forward. It meant collapsing seven navigation options down to four, organized around what someone wanted to accomplish rather than what we had built. It meant putting a guided checklist on screen so a new user could see their own progress.

Then we turned to the other side of the problem. If design partners were going to use this and something felt wrong or confusing, how would we know? The answer was: we probably wouldn't, unless we made it effortless to tell us. So we built a small feedback button — always visible, never intrusive — that lets someone describe a problem or request without leaving the page they're on. Their note lands in a shared workspace where we can triage it the same day.

The interesting thing about building the feedback channel was realizing it was a product decision, not just an infrastructure one. Where should feedback go? How much should someone have to write? What should happen after they submit? Each of those choices either adds friction or removes it, and friction is what kills honest input from people who are busy and not obligated to help you.

## The Takeaway

A technically sophisticated system that's invisible behind a cluttered interface is strategically worthless at the moment it matters most — when someone is forming their first opinion of it. And a feedback channel that's hard to use will keep you comfortable and uninformed at exactly the time you can least afford to be.

