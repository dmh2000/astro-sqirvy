---
author: David Howard
pubDate: 2025-07-04
title: 'Algothromorphism'
postSlug: algothromorphism
featured: true
draft: false
tags:
  - LLM
  - Coding
  - Anthropomorphism
  - AI
description: 'LLMs are not normal'
---

# LLMs are not normal software : what are they?

**Anthropomorphism is the attribution of human traits to non-human entities**. In software, this often extends to describing programs as if they have intentions or desires. However, what you are describing is not about human traits, but rather about projecting traditional software logic—deterministic, rule-based, “if-then-else” thinking—onto LLMs, which are fundamentally non-deterministic, pattern-based, and adaptive.

## Possible Terms and Concepts

| Concept              | Description                                                                                     | Example Usage                                                                                            |
| -------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Algothromorphism     | Projecting the behavior of traditional algorithms onto non-algorithmic systems.                 | “Algothromorphism can mislead users of LLMs to assume they are trained for specific inputs and outputs." |
| Logicomorphism       | Attributing conventional logic or rule-based reasoning to systems that do not operate that way. | “Logicomorphism leads people to expect LLMs to always follow strict rules.”                              |
| Deterministification | Treating inherently non-deterministic systems as if they were deterministic.                    | “Deterministification is common in early LLM adoption.”                                                  |
| Softwaromorphism     | Attributing software-like, coded, or procedural logic to non-software systems.                  | “Softwaromorphism obscures how LLMs really work.”                                                        |

These are neologisms—not established terms, but logical extensions of existing language patterns (as with anthropomorphism). Of these, logicomorphism or Algothromorphism most directly capture the idea of attributing traditional, rule-based logic to LLMs, which are instead driven by statistical pattern recognition and learned behaviors.

**Here's an example of algothromorphism in action**: In late 2024, Anthropic came out with the Model Context Protocol as a way to add functionality to an LLM based AI system. _This can lead to the assumption that somehow there is specific 'MCP' logic that is specifically coded into LLMs._ But, if that were so, only Anthropic LLMs would be exepected to have it. Or, how do MCP's work with LLMs that were created before the the MCP spec was created? In fact LLMs are not specifically trained to respond to MCP specs in a context, the LLM just treats it like any other input in the context. (MCP servers don't talk directly to LLM's anyway. The client agent does that)

**ERRATA: The above paragraph is not quite correct. Most LLMS have dedicated support for some form of 'function calling' that is treated differenly from normal string context. For example, Gemini 2.0 has a spec for tool calling, but not MCP. Gemini 2.5 has built in support for MCP definitions. It's up to the agent/client to send the appropriate function calling context to the LLM.**

Supporting Context

- Traditional software is deterministic, following rigid, pre-coded logic.
- LLMs are non-deterministic, relying on learned patterns, not explicit rules.
- Projecting software logic onto LLMs can lead to misunderstandings about their capabilities and limitations.

“Conventional Software is grounded in logic and rigid rules that determine its behavior. LLMs, on the other hand, display learned behaviors that aren’t always rooted in pure logic and preset rules.”

## Summary

**Algothromorphism (my choice for best neologism) is the mistaken attribution of conventional, rule-based software logic to LLMs, which operate fundamentally differently.**
