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
- Integer overflows result in panicks at run-time when normally compiled. When compiled with the `--release` flag, it will wrap. But wrapping can be checked for with builtin methods. Great way to deal with this set of errors as these are also reliability concerns.
- `char` is Unicode, not ASCII
- Indexing the `i`-th element of a tuple `x` is written: `x.i`
- "Arrays" are fixed-size and stored on the heap. I think Python is the only language I know that calls variable-sized lists "arrays".
- Indexing an array outside its bounds results in a panick at run-time. Fabulous. I wish C had this.
- Functions don't have to be defined/declared before the caller function. Great. One of the things that were tedious in C.
- Non-Rust-specific-thing that was neat: a function takes "paramaters" as variables, and takes "arguments" as concrete values of those paramters.
- Some tinkering I did showed me how to directly print the return value of a function: `println!("the value of return_five() is {}", return_five());`. This is neat since you don't have to deal with placeholders in control strings like in C.
- No special way of writing multi-line comments. It's just `//` for each additional line.
- Non-Boolean types will not be converted to a Boolean in places like `if` expressoins. This was a feature in other languages that was convenient once I got used to it, but was confusing at first.
- Loop labels were a thing that I was curious why it didn't exist when I first learned the `break` statement. After picking up a few more languages, I just assumed it was a thing that wasn't possible, but Rust's got it.

### Chapter 4

- Listing 4-3 makes it look like Rust's ownership allows for "GC-like" convenience, but the performance of a non-GC language.
- Was scared of this being extremely hard, but chapter 4.1 makes ownership look like something that's not that hard? Maybe it's because I've only been introduced to the beginning of it, and I haven't built anything with it. But it just seems like it's trying to cleverly take care of heap allocated memory in order to avoid forgetting to free, double-free, etc.
- Chapter 4.2 still keeps me feeling the same way as 4.1. Seems like most of the rules are simple enough? I would think that knowing of these issues at compile-time is far better than having to track them down after it has panicked when you run it.
- Slices was not the feature I expected to see in Rust. I'm happy it exists, as slicing is a feature I find convenient in Python, which I haven't come across in any of the other languages I've touched.
