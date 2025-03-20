---
title: "第四話　macOS を Nix で管理する方法を調べる"
description: "エンジニアになりたいとインターンに出て行った学生が Nix ユーザになってた　第四話"
date: "2025-03-20"
---

macOS で Nix を使用するガイドや事例、Homebrew から Nix に移行する方法を読んだ。あまりにも多いので、今回は資料のメモだけを書く。

- OPENLOGI で働くこのエンジニアの方は Determinate Systems インストーラを使っている：[Nixで整える開発環境](https://zenn.dev/mizunashi_mana/articles/19707d72b56c00#nix%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8B)
- macOS に Home Manager のみを使ってインストールすると、デスクトップアプリがアプリケーション一覧に表示されないらしい [開発マシンの環境セットアップをAnsibleからNixに移行した ](https://blog.handlena.me/entry/2025/02/migrate-from-ansible-to-nix/#%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E3%82%A2%E3%83%97%E3%83%AA%E3%81%8C%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E4%B8%80%E8%A6%A7%E3%81%AB%E8%A1%A8%E7%A4%BA%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84)
    - `nix-darwin` 経由の `Homebrew` でのインストールであれば、アプリケーション一覧に表示されるので、対策はある。
    - Nix マキシマリズムは諦めて、別途に Nix 経由ではなく、普通に Homebrew をインストールして、GUI アプリは Homebrew から直接ダウンロードするというのも一つの方法：<https://gist.github.com/orzklv/c7cdda429ec2f3fe88f0662c7c9925ec>
- [How to Learn Nix, Part 19: Switching from Homebrew to Nix](https://ianthehenry.com/posts/how-to-learn-nix/switching-from-homebrew-to-nix/)
    - `brew leaves` で depedency じゃない Homebrew formulae の一覧を取得できる。これは Homebrew からの移行時に大いに役に立ちそう。
- [How to migrate from Homebrew to Nix](https://gist.github.com/orzklv/c7cdda429ec2f3fe88f0662c7c9925ec)
    - Nix 経由でパッケージをインストールする方法は主に3つある：
        - `nix-shell -p <package-name>`: パッケージを少し試してみたい時に便利。
        - `nix-env -iA nixpkgs.<package-name>`: これは `brew install <package-name>` に一番近いが、命令的（imperative）であるため、"the Nix way" ではない。
        - パッケージを configuration Flake に追加する：これぞ宣言的（declarative）で、"the Nix way" な方法。
    - このように分けるのは自分の Nix に対する認識を変えた。希望として、Nix には Homebrew に一時的なシェルや開発環境も構築できる上位互換であって欲しいと思っていた。`brew install` のコマンド一つ実行すればパッケージが手に入るように、`nix install` 的なコマンドを求めていた。けど Nix は違うということを覚悟するべき。
- [Setup nix, nix-darwin and home-manager from scratch on an M1 Macbook Pro](https://gist.github.com/jmatsushita/5c50ef14b4b96cb24ae5268dab613050)
    - Nix、`nix-darwin`、Home Manager を一からインストールするスクリプト
- [Reproducible macOS Configurations with Nix](https://victorpierre.dev/blog/declarative-macos-configurations-with-nix/)
    - この人は Nix と `nix-darwin` を使っているが、Home Manager は使っていない。よく考えればこれは可能であるのだが、`nix-darwin` を使っているのを見てきた人たちは漏れなく Home Manager も使っていた。
    - [Why I'm Ditching Nix Home Manager - And What I'm Using Instead](https://youtu.be/U6reJVR3FfA?si=wEL4KpyFmyiYL-zn)
        - この人は過去に Home Manager を使っていたが、GNU Stow に戻った。
        - Home Manager を使用すると、システムの dotfile の変更を反映させるために `home-manager switch` を実行して変更を同期させないといけない。これは Lazy で管理する Neovim プラグインにも適用する。
- [Homebrew管理下のCLIをNixに移してみる](https://zenn.dev/kawarimidoll/articles/0a4ec8bab8a8ba)
    - Determinate Systems インストーラを使う際の注意点：`--determinate` フラグをインストールコマンドに追加するとカスタムの "Determinate Nix" がインストールされ、これは "Nix" とは別物であって、他のソフトウェアと上手く連携できなくなるかもしれない：<https://github.com/LnL7/nix-darwin/issues/149#issuecomment-2442971641>。`--determinate` をインストールコマンドから削除しても、インストール中に "Determinate Nix" をインストールするかを聞かれるので、"No" と答えるように注意しなければならない。　
        - これは `nix-darwin` と干渉しているから発生する問題みたいだが、この問題は2025-02に両者によって改善された？<https://determinate.systems/posts/nix-darwin-updates/> とはいえ、スタンダードじゃない "Nix" をインストールするのは初心者にとっていずれにせよ分かりづらくなるだろう
            - `nix-darwin` は macOS の設定に限らず、Nix のインストールも管理しようとしていた。Determinate も Nix のインストールを管理しようとしているためコンフリクトしていた。でも2025-02のアップデートにより `nix-darwin` 側による Nix インストールの管理をオフにできる。
    - Homebrew から Nix への移行ガイドとしてはこの記事がとても役に立ちそう。Flake を使った "the Nix way" なパッケージインストールについて詳しく書いてある。
- [Homebrew管理下のCLIをNixに移してみる Home Manager篇](https://zenn.dev/kawarimidoll/articles/9c44ce8b60726f)
    - 上の便利なシリーズの続き。
- [Homebrew管理下のGUIもNixに移してみる nix-darwin篇](https://zenn.dev/kawarimidoll/articles/271c339c5392ce)
    - 上の便利なシリーズの続き。
- [Nixing Homebrew: Streamlining package management on your machine](https://dev.to/synecdokey/nix-on-macos-2oj3)
    - この人は `nix-darwin` 非推奨派みたい。あまりにも `nix-darwin` が嵌入的であると感じているため。
    - ただ Home Manager の使用はシェルの設定のために推奨している。
- 私が使うターミナルエミュレータ Ghostty の開発者、そして Terraform などを手がける HashiCorp 創業者 Mitchell Hashimoto の NixOS：<https://github.com/mitchellh/nixos-config>
    - 彼は macOS の GUI アプリケーションを使ったり、Home Manager を使用しているが、VMWare Fusion で NixOS の VM を立ち上げて、そっちでターミナルやその他開発ツールを使っている。
