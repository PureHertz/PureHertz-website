---
title: Quarto用技術文書テンプレート
date: 2025-08-23
date-modified: 2025-08-23
categories: [Quarto]
image: /common/code.jpg
---

## 概要

できるだけプレーンに近いMarkdownファイルから、それなりの見た目の日本語PDFを出力するためのQuartoテンプレートを作ってみました。GitHubに置いてあります。

- [PureHertz / QuartoTemplates](https://github.com/PureHertz/QuartoTemplates)

単一のMarkdownファイルから技術資料を作るための**technote**と、複数のMarkdownファイルを各章とする技術書を作るための**book**の2種類を用意してあります。

![technoteテンプレート](quarto_template_assets/technote.png)

![bookテンプレート1](quarto_template_assets/book1.png)

![bookテンプレート2](quarto_template_assets/book2.png)


Quartoについては、以下のリンクを参照してください。Quarto専用を含むMarkdownの表記方法も記載されています。

- https://quarto.org/

Quartoの他に以下が必要です。フォントはStaticフォントをインストールしてください。VariableフォントだとLaTeXのレンダリングに失敗する可能性が高いです。

- TinyTeX: Quartoインストール後に`quarto install tinytex`を実行してください。
- サンセリフフォント
  - [Noto Sans](https://fonts.google.com/noto/specimen/Noto+Sans)
  - [Noto Sans JP](https://fonts.google.com/noto/specimen/Noto+Sans+JP)
- セリフフォント
  - [Noto Serif](https://fonts.google.com/noto/specimen/Noto+Serif) (for book)
  - [Noto Serif JP](https://fonts.google.com/noto/specimen/Noto+Serif+JP) (for book)
- 等角フォント
  - [PlemolJP](https://github.com/yuru7/PlemolJP/releases/tag/v3.0.0)

## technote

`tecnote/`内は、`bxjsarticle`をもとにしたテクニカルノート用のテンプレートファイルセットです。Markdownファイル1つをPDF化します。

```default
> quarto render <markdown file path> --to pdf
```

でレンダリングしてください。

テンプレートのファイル構成は以下の通りです。

- `_metadate.yml`: YAMLヘッダーの設定ファイル
- `_preamble_technote.tex`: LaTeXのプリンブルファイル
- `quarto_template.md`: Markdownファイル
- `quarto_template_assets/`: 画像やその他の素材を格納するフォルダ
- `the-optical-society.cls`: 参考文献のスタイルファイル

Markdownファイルを作成し、YAMLヘッダーでタイトルなどを指定します。imageファイルなどの素材は、各章ごとに`quarto_template_assets`のようなフォルダを作成し、そこに配置して参照します。各章のMarkdownファイルと対応する素材フォルダを取り出せば、そのままbookテンプレートのひとつの章として使用できます。

全体の設定は`_metadata.yml`で行いますが、基本的には変更不要です。


## book

`book/`内は`bxjsbook`をもとにした技術書用のテンプレートファイルセットです。Chapterごとに複数のMarkdownファイルを用意してまとめてPDF化します。

```default
> quarto render
```

でレンダリングしてください。

テンプレートのファイル構成は以下の通りです。

- `_quarto.yml`: Quartoの設定ファイル
- `_preamble_book.tex`: LaTeXのプリンブルファイル
- `***.md`: 各章のMarkdownファイル
- `***.qmd`: メインコンテンツ以外のMarkdownファイル
- `***_assets/`: 各章の画像やその他の素材を格納するフォルダ
- `the-optical-society.cls`: 参考文献のスタイルファイル
- `_book/`: 出力フォルダ

章ごとにMarkdownファイルを作成し、YAMLヘッダーで章のタイトルを指定します。テンプレートでは、`quarto_template_1.md`と`quarto_template_2.md`の2つの章を用意しています。imageファイルなどの素材は、各章ごとに`quarto_template_1_assets`や`quarto_template_2_assets`のようなフォルダを作成し、そこに配置して参照します。各章のMarkdownファイルと対応する素材フォルダを取り出せば、そのままtechnoteテンプレートでも使用できます。

上記以外に、まえがき`index.qmd`とあとがき`postface.qmd`のMarkdownファイルも用意しています。`index.qmd`が無いと`quarto render`が通らないので注意してください。参考文献と奥付は`references.qmd`で自動生成します。参考文献を使用しない場合は、このファイルを編集して参考文献部分をコメントアウトしてください。

全体の設定は`_quarto.yml`で行います。必要箇所を変更して使用してください。


## その他

LaTeXエンジンにはLuaLaTeXを使用しているのですが、コンパイルにはなかなか時間がかかってしまいます。XeLaTeXの方が速いらしいのですが、LuaLaTeXの方が日本語の組版が安定しているようなので、こちらを採用しました。将来的にはXeLaTeXに切り替えるとか、Typstを使うとか、あり得るかもしれません。