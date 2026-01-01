---
title: "Vim Keys I Found By Accident"
description: "Happy accidents do exist."
date: "2025-04-10"
---

This will just be a cotinuously updated list of Vim keys/motions/commands I found by accident, mostly through mis-clicks, and sometimes by reading the friendly manual.

- `S`
    - Delete line and start insert (can have number prepended to delete `n` lines)
    - <https://vimhelp.org/change.txt.html#S>
- `SHIFT` + `k`
    - When pressed in visual mode over a keyword, brings you to help documentation for that keyword
    - <https://medium.com/code-art/vim-powerful-shift-k-748fec296319>
- `Ctrl` + `r`
    - Redo
    - <https://linuxize.com/post/vim-undo-redo/>
- `Ctrl` + `x` -> `Ctrl` + `f`
    - During insert mode, on a line with a directory path like `$HOME/git`, it will expand the `$HOME` into the actual directory. For example `$HOME/git` to `Users/yutatokoi/git`
    - Found whilst watching a [video](https://youtu.be/03KsS09YS4E?si=N-PdBXxyt0UAL7LQ&t=165)
