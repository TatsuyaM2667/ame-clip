# ame-clip

Wayland のクリップボードに入れる・出す小さなコマンド ame-copy / ame-paste(wl-copy・wl-paste の代わり)。

[ame-shell](https://github.com/TatsuyaM2667/ame-shell)(Wayland のデスクトップシェル)の一部を、単独で使えるように切り出したものです。
ame-shell は画面の要らない仕事を、1 つのことをして標準入出力でやりとりする小さなコマンドに分けています。これはその 1 つです。

## 使い方

```text
ame-copy / ame-paste: Wayland のクリップボードに入れる / 出す(wl-copy・wl-paste の代わり)。

  echo hi | ame-copy            標準入力をクリップボードに入れる(裏に残って、貼り付けられるたびに渡す)
  ame-copy -t image/png < a.png 種類を決めて入れる(省くと文字。PNG の頭なら image/png)
  ame-paste                     クリップボードの中身を標準出力へ(文字を優先)
  ame-paste -t image/png        その種類で出す
  ame-paste -l                  入っている種類の一覧
  ame-paste --watch             文字がコピーされるたびに、その中身を JSON の文字列 1 行で(終わらない。パスワード管理の「秘密」は除く)

1 つの実行ファイルで、呼ばれた名前(ame-copy / ame-paste)で動きを変える。
コンポジタの ext-data-control-v1 を使う(River 0.5 / wlroots 0.19 以降。River 0.3 には無い)。
ame-copy は、ほかのアプリがクリップボードを取るまで裏で動き続ける(wl-copy と同じ)。
終了コード: 0 できた / 1 画面につながらない・コンポジタが対応していない・空 / 2 使い方の誤り
```

## ビルド

```sh
zig build -Doptimize=ReleaseSafe   # zig-out/bin(Zig 0.13、libc・wayland-client・wayland-scanner)
zig build test
```

## このリポジトリについて

正本は ame-shell の `src/cmd/ame-clip.zig` です。このリポジトリは `scripts/split-repos.sh` が生成して同期しています。
直したいところがあれば ame-shell の方へお願いします。

ライセンス: GPL-3.0(ame-shell と同じ)
