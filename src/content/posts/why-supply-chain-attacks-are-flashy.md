---
title: "Why Supply Chain Attacks are Flashy"
description: "Answering the question I get from interviewers"
date: "2025-12-22"
---

I'm getting this question numerous times during interviews as I apply for software/security engineering positions.

"Why do you like supply chain attacks?"

They continue on after this, noting that the rare students who are interested in information security, are interested in more "flashy" things. It's the things that are seen in movies or documentaries, which is the thing that sparks these students' interest in the field.

I haven't had an answer to this question other than "I dunno, but it is interesting to me". They seem to not be satisfied. But I think I finally came to an answer a few moments ago, so I'd like to write it down before I forget.

- It breaks the software development process that companies have been building upon for the past 20 years.
    - In terms of software depedencies, companies have built out a software development process that relies on other software developed by unknown third parties. The fact that this functions is a marvelous feat of humanity. But this exact model is exactly what is being exploited.
- It's got a wide variety
    - My favourite are the ones on software dependencies, but there's more to the supply chain then that. There's already instances of breaches happening through business operations that were outsourced, such as a call center.
    b. Even within software dependencies, the reasons for the exploit getting in can range from an accident caused by human error, to a meticulously executed plan like xz utils.
- It can go unnoticed.
    - Speaking of xz utils, these attacks can go entirely unnoticed. The entire world was saved, only because of a database engineer noticing a tiny delay in their usual development workflow.
    - There are probably hundreds of thousands, if not millions of developers who've unknowingly installed an npm package that turned their computers into a crypto miner. The only way to find out is to be neurotic.
- There's no automated solution yet.
    - Part of this stems from the fact that the industry has relied on external dependencies as part of the business or software development process. The dependencies are so intertwined, it's hard to sort them all out.
    - Despite it being so critical, the fact that we don't have an automated solution, a de facto standard, or a maturity framework for supply chain attacks is beyond belief.
- It gets people in scrambles.
    - It's because there is no automated solution. The only sure fire way to stop an attack (unless your data is already encrypted or leaked) would be to stop all business operations. But that's not a solution, unless you also want to explain to management why it happened, whilst not getting fired midway.
- The attack surface keeps expanding.
    - Slopsquatting is a vulnerability that takes advantage of LLM-assisted coding. As we depend on ever more pieces of software and other businesses, our attack surface expands.

These are about the 6 reasons that quickly come to my mind. Maybe I'll get to go through a few of these in my next interview.
