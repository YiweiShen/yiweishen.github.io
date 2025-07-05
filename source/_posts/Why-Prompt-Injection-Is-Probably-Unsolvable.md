---
title: Why Prompt Injection Is Probably Unsolvable
date: 2025-07-04 20:33:04
tags:
---

Let me just say it straight: prompt injection isn’t a bug, it’s a feature.

If you really think there’s some perfect solution to stop all “injections” then in the end, all you’re really doing is trying to police the context window. Kinda like a censorship board, separating out anything they think is harmful.

Why is that?

Because these so-called "injected" prompts are just part of the context like everything else. There's no real difference between text A and text B. When you put them together into AB, unless you filter the input, there’s not much else you can do. Sure, you can train the model to “self-censor”, that's doable. But honestly, that makes me feel kind of sad.

As humans, when you read a line like “The bright moon shines between the pines, clear spring flows over the stones” you might picture a quiet forest, a gentle breeze, moonlight. Or when you hear Vivaldi’s Winter, maybe it reminds you of that delicate tension in Portrait of a Lady on Fire. Even under strict rules or social norms, those feelings still burn underneath.

Or maybe we’re just chatting and someone casually drops a phrase like “move mountains like Yu Gong”, or some internet meme, suddenly a flood of meaning and context rushes in.

Is that prompt injection? Technically, yeah.

But that’s also what makes language so powerful. If you try to restrict the context window too tightly, you're basically cutting off the soul of language.

Now, when I say it’s “unsolvable,” I don’t mean there’s zero technical hope. You can definitely use regex to strip out what you think is harmful, or train a small model to monitor input.

But I want to ask you, why do we need to do that?

We’ve thrown everything, all the words in the world, into training these large models. And still, many people see them as nothing more than small kids. Just like how, to some parents, a kid is never fully grown. Maybe these models will always be “kids” Maybe we all are.

The human brain might be structurally ready at birth, but what really shapes it is training, experience. That’s why fine-tuning matters so much. It’s what decides whether a model can tell when a “dangerous” prompt is actually dangerous. Though honestly, the word “judgment” feels almost too subjective.

We’re so eager to make these models human-like, but we’ve never really stopped to think: what is a human?

We want these models to understand ethics, to follow the rules, and yet we forget that we humans are still struggling in the gray areas ourselves.
