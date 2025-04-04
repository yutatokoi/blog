---
title: "第六話　mSCP-nix"
description: "エンジニアになりたいとインターンに出て行った学生が Nix ユーザになってた　第六話"
date: "2025-04-04"
---

これは世の中になさそうで、面白そうなプロジェクトだと思ったアイデアが、実は既に存在していたという話。

何をしたかったのかというと、macOS の設定をセキュリティ基準をパスするように機械的に変更して管理をすること。元ネタとなっているのが米国 NIST の [macOS Security Compliance Project (mSCP)](https://github.com/usnistgov/macos_security)。YAML ファイルに設定を記述し、それを自動的に適用し、管理し、確認することができるようになっている。

mSCP はすごいことに NIST 意外にも NASA からの共同作業者も参加していて、Apple が公式に認知しているプロジェクトでもある。

でもどうせなら YAML じゃなくて Nix を使用して管理できるのではないだろうかと思い、Nix 及び `nix-darwin` を使おうと考えました。

ただ Nix だけでは使い物にはならず、設定の自動適用、管理、モニタリングを行うためのツールと連携する必要がある。これはまさに MDM の領域だと思い、mSCP に参画している Jamf について調べてみた。

ここまでは Nix と macOS という二つの単語に加えて、「セキュリティ」や「設定管理」などの関連検索を行っていたのだが、「Jamf」を加えたら Determinate Systems 社が既にこの領域に手をつけていたことがわかった。

- [Nix for macOS with MDM](https://determinate.systems/nix/macos/mdm/)
- [Nix for macOS with Jamf](https://determinate.systems/nix/macos/jamf/)
- [Deploy Determinate with MDM](https://docs.determinate.systems/guides/mdm/)

もちろん類似のツールを作ることも可能だが、既にゴチャゴチャしていて探索しづらい Nix の世界を更に複雑にするつもりはないので、手を出さないことにします。これについて調べるだけでも MDM などについても勉強になったので、それを成果物とします。
