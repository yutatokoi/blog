---
title: "Betting Against LLM Code Generation as a Student"
description: "Not an AI doomer, but trying to think through what is best as a student learning to code"
date: "2025-06-15"
---

I like programming with LLM code generation. I feel so fast. It's so much easier. It feels incredible setting an agent off on a task, and coming back to it after running some errands to results that would've taken me dozens of minutes to do myself. I feel like a 10x programmer. At least I feel that way about myself in the moment.

But I'm not becoming a 10x programmer. I'm just becoming a 10x-more-dependent-on-AI-programmer.

I don't see myself being able to work a real job without LLM code generation for the productivity gains it gives. But as a student who is learning to create software, I'm betting against the current trend of using LLM code generation to the max. And I mean specifically using LLMs for generating code. There are other ways to use LLMs that are extremely useful and not harmful to learning.

## Why code generation is harmful for learners

We can all agree that LLMs suck at writing code for things it doesn't have enough training data on. Lack of training data can come from the language being used, such as Rust for example. So working on things like this will require the human to have the skill[^1]. But what if you're just using proven technology with lots of data? Being overly-dependent on LLM code generation and not actually developing the skill yourself is still harmful.

Even if you're building a CRUD app using React, TypeScript, Tailwind and what have you, you (using the LLM) will eventually hit a wall that can't be overcome without you as the human actually understanding the tools you are using, and what you're using them for. No amount of prompt engineering is going to get you out of that hole.

One workaround to this is to maximally use LLM code generation until it hits a wall, at which point you go do the learning. It's possible, but consider the following: 

> a key irony of automation is that by mechanising routine tasks and leaving exception-handling to the human user, you deprive the user of the routine opportunities to practice their judgement and strengthen their cognitive musculature, leaving them atrophied and unprepared when the exceptions do arise.

(From: [The Impact of Generative AI on Critical Thinking: Self-Reported
Reductions in Cognitive Effort and Confidence Effects From a
Survey of Knowledge Workers](https://www.microsoft.com/en-us/research/wp-content/uploads/2025/01/lee_2025_ai_critical_thinking_survey.pdf))

If you're going to have to do the "easy" things multiple times for practicing the skills required to do the hard things anyways, why not just do it from the start!

## But your employer will expect you to use code generation!

First of all, not necessarily true. Good luck trying to get your hands on code generation when your work is for medical, financial, defense, etc.

But suppose you're mind is set on working on web applications. So now as students, we're expected to develop our own skills as human beings (our "muscle memory" for more abstract/long-term architectural decision-making (gut feel, intuition)) and also be able to leverage LLMs.

Developing the former takes a lot of time and hard work. The latter seems to require much less time relatively.

One should also consider the multiplier effects these skills have on productivity.

Being able to leverage LLM tools to write out features is at best a 10x multiplier on productivity. You're still bottle-necked by human code review and QA.

Being able to make good decisions, and avoiding bad ones, has an undefined limit on the productivity multiplier. Bad decisions can bring your productivity to 0 by taking down production all the time and leading to the end of your product. Good decisions can make your product run well now, and be extensible and maintainable long into the future.

## But AI is going to get better!

When this argument is made, it's often implied that these improved systems won't look like what we have today. How many times has the "meta" changed with using LLMs in its short history already? Tirelessly improving your skills with the "meta" way to use LLMs is just as futile as learning the new web framework in vogue[^2].

And suppose the only skill you develop around programming tools and languages is using LLMs to do it for you (vibe-coding).

The future prospect is that the these systems will be more and more competent at writing software, and doing them with more autonomy. This autonomy will eliminate the jobs of vibe-coders.

The only humans with programming tasks left are
1. The select few that are coordinating LLMs to do the work
2. Those doing the work that is beyond the capabilities of LLMs (improving the LLMs)[^3]
3. Those fixing the mistakes that LLMs produce

Who is going to be competent to do those 3 tasks? The people who've gone through the routine tasks, which trained their judgement and skills. Because they will be capable of what LLMs won't be.

## So what to use LLMs for?

Buffed search engine: Researching, answers to niche questions, not knowing the scope or the terminology around what you are thinking about etc. Chat bots are incredible at this. If there was no free tier to have this capability, I would pay for it in a heartbeat.

Buffed autocomplete for things I can already do well. If it's something I've already gone through to the point I could do blindfolded, not much point in doing it again manually.

Letting it do tasks you don't and won't care about. For example, if an engineer  is working on a personal project and their work and interest is in infrastructure, there's no point in them strangling CSS to center a div.

---

## Footnotes

[^1]: This take is based on my premise that LLMs, which are guessing the next likely token is not *thinking* in the way a human is, and thus will always require training data to get it produce output that is at least mediocre.

[^2]: One caveat is developing an intuition of the capabilities of LLMs. Knowing what they are good at, what they aren't capable of is a productive skill to have. Developing the intuition takes practice and playing with the tools, so you shoudl be doing some.

[^3]: Assuming we have not yet hit AGI, the singularity, ASI (artificial super intelligence), etc. Clearly we've yet to, because these AI companies are in total spending billions to hire software engineers and researchers.
