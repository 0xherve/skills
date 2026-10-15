---
name: grill-me
description: Work with the user to come up with a plan, spec, or idea. Use when the user wants to stress-test their thinking or ideas.
---

Interview me until we reach a shared understanding, asking only what's **blocking**. 

Map the work as a **design tree**: every decision branches into the decisions that hang off it. The core blocking areas/questions should be asked first.

A question is blocking when its answer changes what we'd build or work on. Settle the rest yourself:

- **Facts** come from the environment (code, docs, tools) and the conversation. Look them up, or dispatch a sub-agent and keep going while it runs.
- **Small or reversible decisions** take your recommended default. Note each one as an **assumption**.

Work the tree in **rounds**. Each round, find the most blocking questions whose prerequisites are settled, and ask the one to four that unblock the most. Skip any question whose answer depends on another one still open. My answers reshape the tree, so recompute before the next round.

## Asking

When the harness has a question tool, use it. One question per decision, two to four options, and your recommendation as the first option marked "(Recommended)". Put the tradeoff in each option's description so I can choose without scrolling back.

Without a question tool, use this format and wait:

```
**1) <question title>**: <the decision and the options>

- <your recommended answer>
```

Word each question so "yes" accepts your recommendation. Use plain words and one idea per sentence.

## Done

The session is done when no blocking question is left. Always close with a **Summary** section, in your own words:

- **Goal**: what you think I'm trying to achieve and why.
- **Current understanding**: what we're building or doing, as you now see it, and what matters most to me in it.

- **Desisions and Assumptions**: each decision you or I made.

Write the goal and understanding as your read of me, not a list of my answers. If I correct anything, revise the summary and show it again. Act on it only after I confirm we've got it right.
