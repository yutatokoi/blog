---
title: "Nix修行 part 5 - Homebrew から Nix に移行する–CLI と macOS 設定編"
description: "Nix修行 part 5"
date: "2025-03-22"
---

## `nix-darwin` をインストールしてみる

[動画チュートリアル](https://youtu.be/Z8BL8mdzWHI?si=Yn7nXOb4R8y1x9u0)と [`nix-darwin` リポジトリ](https://github.com/LnL7/nix-darwin)を参照しながらインストールしようとしました。

数ヶ月前の動画にも関わらず、インストール手順が公式の最新の方法と違うのに驚きました。本当に Nix はまだまだ発展途上だと思わされる。

インストール中になぜだかわからないエラーにぶつかり、ひとまず断念した。Flakes の設定が上手くできていなかったからかな？そもそも Flakes についてよくわかってないし、良い機会だから調べてみよう。

## Flakes について調べる

参照：<https://nix.dev/concepts/flakes>

### そもそも Flakes とは？

ルートディレクトリに `flake.nix` ファイルがあるファイルシステムのこと。

### "普通"の Nix と何が違うの？

"普通"の Nix が持つ機能に加えて以下のような挙動が追加されている：
- `flake.nix` ファイル内では特定のスキーマが指定されている
    - （推測）この方が明確に構造化されていることによって統一性があるのが良い
- 他の Flake を簡単に参照できる
    - 他の Flake への参照はデフォルトで特定のバージョンにロックされ、アップデートは手動ではなくプログラムで行える。
- `flake.nix` ファイルが実行される前に、Flake ディレクトリ全体が Nix store にコピーされる
    - メリット：キャッシュを活用できるため、変更部分だけを実行して、残りはキャッシュを参照できる
    - デメリット：一部に変更を加えるだけでも Flake ディレクトリ全体をコピーしないといけない
- 外部変数、外部パラメータ、その他 impure な値は許容されない
    - 再現性を担保するため

### なぜ実装から数年経つ今も experimental で、一部では反対されているのか

導入されたのは [Nix 2.4](https://wiki.nixos.org/wiki/Flakes) （2021-11-01のリリース）

詳しくは [Why are flakes controversial?](https://nix.dev/concepts/flakes#why-are-flakes-controversial) のパートで書かれているが、まとめると以下のようなところ：

- Flakes の設計が定まっていない状態で実装が開始された
- （一部の面において）Flakes でもミュータブルなステートを扱うため、その点では `nix-channel` と変わらない
- パラメータが使えないため、扱いづらい
- 最初の実装が破壊的変更を導入するものだった

最後の点が理由でまだ experimental にされているのだと思う。恐らく Nix 全体の整理ができて、今後の方針が定まったら v3 に上げる予定。バージョンを上げるタイミングで experimental ではなくなるのだろう。

一部で物議を醸していて反対されているのは、このような問題があって、不安定な feature であるにも関わらず、初心者へ利用が広く推奨されているから。

## `nix-darwin` をインストールしてみる（再挑戦）

今回は上手く行った。前回挑戦した時からさらにインストール手順が変わっている気がする。

現時点でデフォルトは `/etc/nix-darwin/flake.nix` で `nix-darwin` の設定を記述すること。試しに Neovim と Trivy を `nixpkgs` からインストールしてみた：

```
{
...
  outputs = inputs@{ self, nix-darwin, nixpkgs }:
  let
    configuration = { pkgs, ... }: {
      environment.systemPackages =
        [ pkgs.neovim
          pkgs.trivy
        ];
...
    };
   };
  };
}
```

これで Nix 経由で Neovim と Trivy がインストールできたはず。

```
> which nvim
/opt/homebrew/bin/nvim

> which trivy
/run/current-system/sw/bin/trivy
```

Trivy でちゃんと Nix でパッケージのインストールが可能だとわかった。ただ既に Homebrew 経由で Neovim はインストールしてあって、`$PATH` には Nix より先に Homebrew が来ている。

```
> echo $PATH
...:/Users/yutatokoi/.local/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/Users/yutatokoi/.nix-profile/bin:/run/current-system/sw/bin:/nix/var/nix/profiles/default/bin:...
```

`PATH` 変数は `.zshrc` や `.config/fish/config.fish` などで変更します。

変更後は Nix でのインストールを参照できていて、今まで通りに Neovim を使えてます。

```
> which nvim
/run/current-system/sw/bin/nvim
```

この勢いで `brew leaves` にあった残りの formulae を `/etc/nix-darwin/flake.nix` に追加した。移行する16の formulae は全て search.nixos.org で見つかったし、`texliveFull` 以外は Homebrew で使用しているのと同じ最新のバージョンだった。

## `fish` をデフォルトのシェルにする方法

`environment.systemPackages` に `pkgs.fish` を追加するだけでは `fish` をデフォルトのシェルとして使うことはできず、macOS デフォルトの `zsh` のままです。

こちらの Issue に対処法が書いてあります：<https://github.com/LnL7/nix-darwin/issues/1237>

## macOS の設定を `/etc/nix-darwin/flake.nix` で定義する

`nix-darwin` の公式ドキュメントには各設定の名前や型が載っているものの、どの数値が何、あるいはパラメータでどれくらいの設定に対応しているのかが不明なことが多いので、外部の資料を参照する必要があります。例えば KeyRepeat に関する設定の閾値はこちらのユーザが記述してくれていました：<https://github.com/ryan4yin/nix-config/blob/9d26022139576b5f5ee221206d796c40a9d095e5/modules/darwin/system.nix#L80-L85>

`system.defaults.universalaccess.*` の設定を記述するにはターミナルアプリケーションにフルディスクアクセス権限を付与しなければいけません。`System Settings > Privacy & Security > Full Disk Access` で権限付与できます（<https://github.com/LnL7/nix-darwin/issues/1049>）。

## 結果

<https://github.com/yutatokoi/dotfiles/commit/1f45a70f04ad2007f1b4edaece1a487c94bc6388>

良い感じに構成できたと思います。残る作業は主に GUI アプリケーションの管理でしょうか。あとは各種 GUI アプリケーションの設定の管理までこのファイル一つで出来ると嬉しいですね。

## その他参考資料

- `nix-darwin` 公式ドキュメント：<https://daiderd.com/nix-darwin/manual/index.html>
- `nix-darwin` のオプションを階層構造で表示している非公式ドキュメント：<https://mynixos.com/nix-darwin>
- これは今回使わなかったが、便利そう：[`nix-homebrew`](https://github.com/zhaofengli/nix-homebrew)
