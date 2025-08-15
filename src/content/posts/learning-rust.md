---
title: "Learning Rust"
description: "Probably won't be dyeing my hair blue, but we'll see"
date: "2025-08-15"
---

This will be a continuously updated post as I go through my process of learning Rust. Some rambling notes as I go through the resources and learn the quirks of the language.

As someone who is interested in the security and reliablility of software, what better language to learn than the language so often touted as providing great safety features. Though I may end up working in a role that won't be writing out code to implement business logic (e.g. security engineer, SRE), learning Rust would let me understand with first-hand experience of the language's safety featurs, as well as let me say "why don't you guys write it in Rust" with more authority. Besides, seems like a fun language to learn (hopefully it doesn't break my brain and I don't dye my hair blue).

## The Process

- Read through the book once quickly to create mental hooks and a mapping of the important terminology/concepts
- Quiz with rust book: <https://rust-book.cs.brown.edu/>
- Katas: <https://github.com/rust-lang/rustlings>

## Going Through "The Book"

### Chapter 1

- All Rust programs start from the `main()` function. I like it as you always know where to start reading the code. This is the same as C too.

### Chapter 2

- I had heard that one of Rust's strong points is that variables are immutable by default. Doesn't that mean they're constants? Or can they be turned into mutable variables later?
- Cargo lets you build and view the documentation for all the depedencies you've pulled into your crate. This is fantastic not only for offline coding, but also to keep the documentation you view limited to avoid distractions.

### Chapter 3

- There are in fact constants, which are different to immutable variables. Constants must have their type explicitly declared, and can only be assigned values that are determined at compile-time, not one that could differ in run-time.
