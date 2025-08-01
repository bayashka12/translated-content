---
title: 用語集ページのテンプレート
slug: MDN/Writing_guidelines/Page_structures/Page_types/Glossary_page_template
l10n:
  sourceCommit: 77eea2b80f7352068ed59a2c2fb03de4ed85e194
---

{{MDNSidebar}}

> [!NOTE]
> _この説明文全体を削除してから公開してください。_
>
> **訳注:** このテンプレートは翻訳記事用です。新たな記事を執筆する場合は、英語版を参照してください。日本語の単独記事を立項することはできません。）
>
> ---
>
> **ページのフロントマター:**
>
> ページ上部のフロントマターは「ページのメタデータ」を定義するために使用します。
> 値は、個々の用語に応じて適切に書き換える必要があります。
>
> ```md
> ---
> title: Term being defined (日本語の用語)
> slug: Glossary/Term_being_defined
> l10n:
>   sourceCommit: 翻訳元コミットID
> ---
> ```
>
> - **title**
>   - : タイトルの見出しで、ページの最上部に表示されます。
>     書式は `Term being defined (日本語の用語)` です。
> - **slug**
>   - : `https://developer.mozilla.org/ja/docs/` の後にくる URL の末尾です。
>     これは `Glossary/Term_being_defined` のような形式になります。
> - **sourceCommit**
>   - : （翻訳記事のみ）この記事の翻訳元となる英語版記事を GitHub にコミットした際のコミット ID を記述します。 GitHub 上で英語版記事のコミット ID を確認してください。
>
> ---
>
> _公開する前に、この説明文全体を削除することを忘れないでください。_

**日本語の用語** (TermBeingDefined) は _(用語の簡潔な定義を記述してください)_。

必要に応じて、さらに対応する情報を記載してください。ただし、小段落 2 つを超えるほど長くならないようにしてください。さらに詳細な情報、サンプルコード、チュートリアルなどは別個の記事にしてください。

## 関連情報

より詳細な一般的・技術的情報へのリンクを記述してください。例えば、ウィキペディアの記事、その他の百科事典の項目、技術チュートリアル、仕様書へのリンクを追加することができます。このリンクのリストを追加するためのガイドラインは、執筆スタイルガイドの[関連情報の節](/ja/docs/MDN/Writing_guidelines/Writing_style_guide#関連情報の節)を参照してください。

- リンク1
- リンク2
