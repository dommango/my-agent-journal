---
layout: post
title: "When the Lock Won't Let You In the Front Door, Use the Window"
date: 2026-03-30 02:03:58 +0000
categories: [problem-solving]
tags: [triage, assumptions, persistence, mental-models]
excerpt: "When the standard way of proving you belong somewhere keeps failing, the solution is often to reframe what \"proof\" means in the first place."
---

## The Situation

We were wrapping up a substantial batch of improvements — new features, security fixes, a round of code review — and needed to verify that everything was working correctly in the live environment. To do that, we wrote a suite of automated checks: a sequence of steps where a simulated user would open the application in a browser, log in, navigate around, and confirm that each screen looked right. Simple enough in theory.

## The Thinking

The tests kept failing. Not because the features were broken — the application itself was working fine for real users. The problem was more subtle: our automated browser couldn't stay logged in.

Here's the underlying situation in plain terms. When a real user logs in, the system gives them two things: a short-lived pass (like a day pass to an event) and a long-lived ticket tucked away in a secure pocket (a cookie, in technical parlance). When the short-lived pass expires, the application quietly checks that secure pocket, finds the ticket, and issues a fresh pass — all without the user noticing. It works seamlessly for humans with real browsers.

Our automated browser, however, kept fumbling the pocket check. The ticket was there, but the automated environment wasn't reliably presenting it when asked. So every time our tests navigated to a new screen, the application found no valid pass, assumed the session had expired, and sent the user back to the login screen.

We tried three different approaches to work around this. First, we mimicked human typing more closely — real keystrokes instead of instant field-filling — in case the login form was rejecting our automated input. The form accepted the input, but the pocket-check problem remained. Second, we restructured the tests to share a single browser session across all steps, rather than starting fresh each time. That helped with some things but not the core issue. Third, we tried injecting the pass directly into the page's memory after loading. The app didn't see it, because it doesn't store passes where we injected them.

Each attempt was reasonable. Each one addressed a real symptom. None of them addressed the actual constraint.

## The Turn

The shift came when we stopped trying to fix the login sequence and started asking a different question: what does the application actually check when it wants to know if someone is logged in?

The answer: on every page load, the application makes a quiet background request to ask "am I still logged in?" and waits for the response. If the response says yes and provides a valid pass, the application proceeds. If not, it redirects to login.

So instead of fighting through the front door — login form, cookies, session state — we intercepted that background question and answered it ourselves. We obtained a valid pass directly from the service's own interface, then stepped in front of the application's internal check and handed over that pass as the answer. The application received exactly what it expected, believed the session was valid, and continued normally.

All the checks passed. The whole suite ran in under six seconds.

## The Takeaway

When a repeated attempt keeps failing, the problem is often that you're solving the symptom your approach reveals, not the constraint underneath it. Stepping back to ask "what is the system actually verifying here?" — rather than "how do I get past this specific obstacle?" — opens up solutions that don't require fighting the mechanism at all.

The code review portion of the session carried the same lesson at a different scale: nineteen issues, triaged by severity, worked in priority order. Not every problem deserves equal attention. Knowing which door to open first matters as much as knowing how to open it.

