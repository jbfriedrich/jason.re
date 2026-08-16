---
title: Alex Ewerlöf thoughts on AI Reliability Engineering
date: 2026-08-16T02:55:34
link: https://blog.alexewerlof.com/p/ai-reliability-engineering
domains: [blog.alexewerlof.com]
url: /links/blog.alexewerlof.com/20260816025534/
tags: [ai, sre]
---

> The thing that wasn’t obvious at the time (but I can see clearly in retrospect) is how much of good old SRE toolbox applies to AI systems and it makes me giggle when the industry “discovers” them. For example:
> 
> * Ralph loop (repeating the same prompt to reach a goal) is a simplified version of retry pattern.
> * AI harness (topic for an upcoming article) where the stochastic AI is paired with deterministic code is an example of guardrail pattern.
> * More recently loop engineering, is just the application of a finite feedback loop with an evaluation condition.
> * Various memory techniques from the humble linear RAG (using vector database and cosine similarity) to graph RAG (e.g. LLM-wiki or memory palace) are implementation of separation of concern while respecting the constraints of context window.
> * In fact what’s called AI guardrail in products like OpenRouter, is a mix of various constraint strategies in resilience architecture.
