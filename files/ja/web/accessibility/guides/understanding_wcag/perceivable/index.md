---
title: 知覚可能
slug: Web/Accessibility/Guides/Understanding_WCAG/Perceivable
original_slug: Web/Accessibility/Understanding_WCAG/Perceivable
l10n:
  sourceCommit: 3a004b55441ee5ac51bd34be5f3b7c6ce693ed6d
---

{{AccessibilitySidebar}}

この記事では、ウェブコンテンツアクセシビリティガイドライン (WCAG) 2.0 および 2.1 の**知覚可能**原則に概説されている達成基準に準拠するようにウェブコンテンツを作成する方法についての実用的なアドバイスを提供します。 知覚可能とは、ユーザーが自分の感覚の 1 つ以上を使用して何らかの方法でそれを知覚できなければならないということです。

> [!NOTE]
> 知覚可能の W3C 定義とそのガイドラインおよび達成基準を読むには、[原則 1: 知覚可能 — 情報とユーザーインターフェイス・コンポーネントが、ユーザーが認識できる方法で提示可能である必要があります](https://www.w3.org/TR/WCAG21/#perceivable)（英語）を参照してください。

## ガイドライン 1.1 — 非テキストコンテンツのための代替テキストの提供

ここで重要なのは、テキストならば障碍のある人が使用できる他の形式に変換できることです。 例えば、スクリーンリーダーで話させたり、ズームインしたり、点字ディスプレイに表示したりできます。 非テキストコンテンツとは、画像、音声、動画などのマルチメディアを指します。

<table class="standard-table">
  <thead>
    <tr>
      <th scope="col">達成基準</th>
      <th scope="col">基準への準拠方法</th>
      <th scope="col">実用的なリソース</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="5">1.1.1 同等のテキストを提供する (A)</td>
      <td>
        意味のある内容を伝える全ての画像は、適切な代替テキストを与えられるべきです。
      </td>
      <td>
        <a href="/ja/docs/Learn/Accessibility/HTML#代替テキスト"
          >代替テキスト。</a
        >
      </td>
    </tr>
    <tr>
      <td>
        複雑な画像や図表には、同じページ上またはリンク先のいずれかにアクセス可能な代替手段を用意するべきです。 <code>longdesc</code> 属性ではなく通常のリンクを使用してください。
      </td>
      <td>
        <p>
          テキストの説明や、アクセス可能なデータ表がうまくいくかもしれません（<a
            href="/ja/docs/Learn/HTML/Tables/Advanced"
            >HTML 表の高度な機能とアクセシビリティ</a
          >を参照）。 <code>longdesc</code> 反対論については、 W3C の<a href="https://www.w3.org/TR/html-longdesc/">Image Description Extension (longdesc)</a>も参照してください。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        マルチメディアコンテンツ（例えば、音声や動画）は、少なくともわかりやすい識別が利用できるべきです（例えば、キャプションまたは同様のもの）。
      </td>
      <td>
        <p>
          静的キャプションの選択肢については<a
            href="/ja/docs/Learn/Accessibility/HTML#代替テキスト"
            >代替テキスト</a
          >を、その他の選択肢については<a
            href="/ja/docs/Learn/Accessibility/Multimedia#音声トランスクリプト"
            >音声トランスクリプト</a
          >、
          <a href="/ja/docs/Learn/Accessibility/Multimedia#映像のテキストトラック"
            >映像のテキストトラック</a
          >を参照してください。
        </p>
      </td>
    </tr>
    <tr>
      <td>
        フォーム要素やボタンのような UI
        コントロールには、その目的を説明するテキストラベルを付けるべきです。
      </td>
      <td>
        ボタンは簡単です —
        ボタンのテキストがボタンの機能を説明していることを確認してください（例えば、<code>&#x3C;button>画像のアップロード&#x3C;/button></code>）。
        他の UI コントロールの詳細については、<a
          href="/ja/docs/Learn/Accessibility/HTML#ui_コントロール"
          >UI コントロール</a
        >を参照してください。
      </td>
    </tr>
    <tr>
      <td>
        支援技術には見えない方法で、装飾的な（コンテンツではない）画像、動画などを実装すると、ユーザーを混乱させません。
      </td>
      <td>
        <p>
          装飾画像は CSS 背景画像を使用して実装する必要があります（<a
            href="/ja/docs/Learn_web_development/Core/Styling_basics/Backgrounds_and_borders"
            >背景</a
          >を参照）。 {{htmlelement("img")}}
          要素を介して画像を含める必要がある場合は、空白の
          alt（<code>alt=""</code>）を付けます。
          そうしないと、スクリーンリーダーがファイルパスなどを読み上げようとする可能性があります。
        </p>
        <p>
          自動再生する背景の動画や音声を含める場合は、できるだけ目立たないようにします。
          コンテンツのように見せたり鳴らさないでください。
          また、無効にするコントロールを提供してください。
          理想的には、それをまったく含めないでください。
        </p>
      </td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> [ガイドライン 1.1: 代替テキスト](https://www.w3.org/TR/WCAG21/#text-alternatives)（英語）に関する WCAG の説明も参照してください。

## ガイドライン 1.2 — 時間ベースのメディアのための代替テキストの提供

時間ベースのメディアは、持続期間を有するマルチメディア、すなわち音声および動画を指します。 また、それらの音声や動画が既存のテキストコンテンツの代替を兼ねる場合は、別の代替テキストを提供する必要はありません。

<table>
  <thead>
    <tr>
       <th scope="col">達成基準</th>
       <th scope="col">基準への準拠方法</th>
       <th scope="col">実用的なリソース</th>
    </tr>
  </thead>
  <tbody>
    <tr>
       <td>1.2.1 記録済みの音声のみおよび動画のみのコンテンツに代わるものを提供する (A)</td>
       <td>トランスクリプトは、録音済みの音声のみのメディアに提供するべきで、トランスクリプトまたは音声解説は、録画済みの動画のみのメディア（すなわち、サイレントビデオ）に提供するべきです。</td>
       <td>トランスクリプト情報については、<a href="/ja/docs/Learn/Accessibility/Multimedia#音声トランスクリプト">音声トランスクリプト</a>を参照してください。 音声解説のチュートリアルはまだありません。</td>
    </tr>
    <tr>
       <td>1.2.2 ウェブベースの動画にキャプションを付ける (A)</td>
       <td>ウェブ上に表示される動画（例えば、HTML 動画）には、キャプションを付けるべきです。 これは、動画の音声部分が聞こえない人々のためのものです。</td>
       <td>HTML 動画のキャプションについては<a href="/ja/docs/Learn/Accessibility/Multimedia#映像のテキストトラック">映像のテキストトラックs</a>を参照してください。 <a href="https://support.google.com/youtube/answer/2734796?hl=en">Add your own subtitles &amp; closed captions</a>（YouTube、英語）も参照してください。</td>
    <tr>
       <td>1.2.3 ウェブベースの動画にテキストトランスクリプトまたは音声解説を提供する (A)</td>
       <td>ウェブ上に提示される動画（例えば、HTML 動画）のためのテキストトランスクリプトまたは音声解説を提供するべきです。 これは、動画の視覚的な部分を見ることができず、音声だけではコンテンツ全体を把握できない人々のためのものです。</td>
       <td>トランスクリプト情報については、<a href="/ja/docs/Learn/Accessibility/Multimedia#音声トランスクリプト">音声トランスクリプト</a> を参照してください。 音声解説のチュートリアルはまだありません。</td>
    </tr>
    <tr>
       <td>1.2.4 生音声にキャプションを付ける (AA)</td>
       <td>音声を含んだすべての生のマルチメディア（ビデオ会議、生音声放送など）には、同期したキャプションを付けるべきです。</td>
       <td></td>
    </tr>
    <tr>
       <td>1.2.5 録画済み動画の音声解説を提供する (AA)</td>
       <td>音声解説は、録画済み動画に対して提供するべきですが、既存の音声が動画によって表現された完全な意味を伝えない場合に限ります。</td>
       <td></td>
    </tr>
    <tr>
       <td>1.2.6 録音済み音声と同等の手話を提供する (AAA)</td>
       <td>音声を含んだ記録済みコンテンツには、同等の手話動画を提供するべきです。</td>
       <td></td>
    </tr>
    <tr>
       <td>1.2.7 音声解説付きの拡張動画を提供する (AAA)</td>
       <td>動画のタイミングの問題で音声解説を提供できない場合（例えば、音声解説を挿入するコンテンツに適切な間がない場合）（1.2.5 を参照）、挿入された間（と音声解説）を含んだ動画の代替バージョンを提供するべきです。</td>
       <td></td>
    </tr>
    <tr>
       <td>1.2.8 記録済みメディアの代替を提供する (AAA)</td>
       <td>動画を特徴とする全てのコンテンツには、わかりやすいテキストトランスクリプトを提供する必要があります。 例えば、見ている映画のスクリプトなどです。 これは、コンテンツを聴くことができない聴覚障碍者のためのものです。</td>
       <td>トランスクリプト情報については、<a href="/ja/docs/Learn/Accessibility/Multimedia#音声トランスクリプト">音声トランスクリプト</a> を参照してください。 </td>
    </tr>
    <tr>
       <td> 1.2.9 生音声用のトランスクリプトを提供する (AAA)</td>
       <td>放送されている生音声のコンテンツのために、例えば、あなたが聞いている演劇やミュージカルのスクリプトのような説明文を提供するべきです。 これは、コンテンツを聴くことができない聴覚障碍者のためのものです。</td>
       <td>トランスクリプト情報については、<a href="/ja/docs/Learn/Accessibility/Multimedia#音声トランスクリプト">音声トランスクリプト</a> を参照してください。 </td>
    </tr>
 </tbody>
</table>

> [!NOTE]
> [ガイドライン 1.2: タイムベースト・メディア: タイムベースト・メディアに代わるものを提供する](https://www.w3.org/TR/WCAG21/#time-based-media)（英語）に関する WCAG の説明も参照してください。

## ガイドライン 1.3 — さまざまな方法で提示できるコンテンツの作成

このガイドラインは、異なるニーズに柔軟に対応して、コンテンツがユーザーによってさまざまな方法で消費される能力について言及しています。

<table class="standard-table">
  <tbody>
    <tr>
      <th scope="col">達成基準</th>
      <th scope="col">基準への準拠方法</th>
      <th scope="col">実用的なリソース</th>
    </tr>
    <tr>
      <td>1.3.1 情報と関係 (A)</td>
      <td>
        <p>
          いかなるコンテンツ構造 — またはコンテンツ間に作られた視覚的関係 —
          もまた、プログラム的に決定されるか、またはテキストの説明から推論され得ます。
          これが関連する主な状況は次のとおりです。
        </p>
        <ul>
          <li>
            テキストラベルとそれが説明するフォーム要素は、{{htmlelement("label")}}
            要素を使用して明確に関連付けられて、スクリーンリーダーなどが拾うことができます。
          </li>
          <li>
            画像の代替テキスト。
            コンテンツ画像には、その画像の内容を明確に説明するテキストが含まれているべきです。
            これは、プログラム的に関連付けることができます（例えば、alt　テキスト）。
            そうでない場合は、関連付けるのは簡単です（例えば、それを説明し、そのすぐ隣に置きます）。
            これは、たとえあなたが画像を見ることができなくても、完全な意味がまだ推測できることを意味するはずです。
          </li>
          <li>
            リスト。
            リスト項目の順序が重要で、順序付きリストを使用するべき場合（{{htmlelement("ol")}}）。
          </li>
        </ul>
      </td>
      <td>
        <p>
          <a href="/ja/docs/Learn/Accessibility/HTML"
            >HTML: アクセシビリティの基礎</a
          >全体には、これに関する情報が満載されていますが、特に<a
            href="/ja/docs/Learn/Accessibility/HTML#良いセマンティクス"
            >良いセマンティクス</a
          >、<a href="/ja/docs/Learn/Accessibility/HTML#ui_コントロール"
            >UI コントロール</a
          >、<a href="/ja/docs/Learn/Accessibility/HTML#代替テキスト"
            >代替テキスト</a
          >を参照するべきです。
        </p>
      </td>
    </tr>
    <tr>
      <td>1.3.2 重要なコンテンツの順序 (A)</td>
      <td>
        賢明で論理的な読み上げ順序は、たとえそれが独特な方法で視覚的に提示されていても、どんな内容に対しても決定しやすいはずです。
        マークアップに関係なく、CSS を使用して独特なレイアウトスタイルを作成することで、正しい意味論的要素（見出し、段落など）を使用して順序を明確にするべきです。
      </td>
      <td>
        繰り返しますが、<a href="/ja/docs/Learn/Accessibility/HTML"
          >HTML: アクセシビリティの基礎</a
        >を参照してください。
      </td>
    </tr>
    <tr>
      <td>1.3.3 感覚的性質 (A)</td>
      <td>
        <p>
          コントロールを操作したり、コンテンツを理解したりするための指示は、単一の感覚には依存しません。
          これは、その感覚に関連する障碍を持つ人々、またはその感覚をサポートしていないデバイスにとってアクセスできないことを証明するかもしれません。
          だから、例えば、
        </p>
        <ul>
          <li>
            「続けるために丸いボタンをクリックしてください」<br />
            それがあなたが押す必要があるボタンであることは明らかであるように、ボタンは明確にラベル付けすべきです。
            複数のボタンがある場合は、それらの機能を区別するために全てが明確にラベル付けされていることを確認してください。
          </li>
          <li>
            「ガイダンスに関する音声の説明を聞く」<br />
            これは明らかに問題があります —
            音声は聴覚障碍のある人にはアクセスできないのに対して、テキストは読むことができるだけでなく、必要に応じてスクリーンリーダーによって話させることもできます。
          </li>
          <li>
            「メニューを表示するには、画面の右側からスワイプ」<br />
            一部のユーザーは、障碍のためや、端末がタッチに対応していないために、画面をスワイプできない可能性があります。
            キーボードショートカットや、キーボードなどの手段でアクティブにできるボタンなどの代替手段を提供する必要があります。
          </li>
        </ul>
        <div class="note notecard">
          <p>
            <strong>メモ:</strong>
            色だけで指示を伝えることは関連していますが、異なるガイドラインでカバーされています — 1.4.1。
          </p>
        </div>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        1.3.4 方向 (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        特定のディスプレイの向きが重要でない限り、コンテンツの表示と操作はポートレートやランドスケープなどの単一のディスプレイの向きに制限されません。
      </td>
      <td>
        <p>
          <a href="https://www.w3.org/WAI/WCAG21/Understanding/orientation.html"
            >方向を理解する</a
          >（英語）
        </p>
      </td>
    </tr>
    <tr>
      <td>
        1.3.5 入力の目的の識別 (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        <p>
          <a href="https://www.w3.org/TR/WCAG21/#input-purposes"
            >53 個の入力フィールド</a
          >（英語）のリストに従って、プログラム的にフィールドの目的を識別してください。
        </p>
      </td>
      <td>
        <a
          href="https://www.w3.org/WAI/WCAG21/Understanding/identify-input-purpose.html"
          >入力の目的の識別を理解する</a
        >（英語）
      </td>
    </tr>
    <tr>
      <td>
        1.3.6 目的の識別 (AAA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        マークアップ言語を使用して実装されたコンテンツでは、ユーザーインターフェイス・コンポーネント、アイコン、およびリージョンの目的はプログラム的に決定できます。
      </td>
      <td>
        <a
          href="https://www.w3.org/WAI/WCAG21/Understanding/identify-purpose.html"
          >目的の識別を理解する</a
        >（英語）
      </td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> [ガイドライン 1.3: 適応可能: 情報や構造を失うことなくさまざまな方法で提示できるコンテンツを作成する](https://www.w3.org/TR/WCAG21/#adaptable)（英語）に関する WCAG の説明も参照してください。

## ガイドライン 1.4: 前景と背景の区別を含め、ユーザーがコンテンツを見たり聞いたりしやすくする

このガイドラインは、コアコンテンツが背景や他の装飾から識別しやすいことを確認することに関するものです。 典型的な例は、色（[色のコントラスト](/ja/docs/Web/Accessibility/Guides/Understanding_WCAG/Perceivable/Color_contrast)と指示を伝えるための[色の使い方](/ja/docs/Web/Accessibility/Understanding_WCAG/Perceivable/Use_of_color)の両方が）ですが、他の状況でも適用されます。

<table class="standard-table">
  <thead>
    <tr>
      <th scope="col">達成基準</th>
      <th scope="col">基準への準拠方法</th>
      <th scope="col">実用的なリソース</th>
    </tr>
    <tr>
      <td>1.4.1 色の使い方 (A)</td>
      <td>
        <p>
          色だけを頼りにして情報を伝えるべきではありません。例えば、フォームでは、必須フィールドを色（赤など）だけで示す付けることは絶対にしないでください。
          代わりに（または同様に）、「必須」というラベルの付いたアスタリスクのようなものがより適切です。
        </p>
      </td>
      <td>
        <a href="/ja/docs/Web/Accessibility/Understanding_WCAG/Perceivable/Use_of_color"
          >色の使用</a
        >、
        <a
          href="/ja/docs/Learn/Accessibility/CSS_and_JavaScript#色とそのコントラスト"
          >色とそのコントラスト</a
        >、
        <a
          href="/ja/docs/Learn/Forms/How_to_structure_a_web_form#複数のラベル"
          >複数のラベル</a
        >を参照してください。
      </td>
    </tr>
    <tr>
      <td>1.4.2 音声コントロール (A)</td>
      <td>
        3 秒以上再生される音声の場合は、音声や動画の再生と一時停止、および音量のミュートや調整を行うためのアクセス可能なコントロールを用意する必要があります。
      </td>
      <td>
        <a
          href="/ja/docs/Web/Media/Audio_and_video_delivery/Video_player_styling_basics"
          >動画プレーヤーのスタイル設定の基本</a
        >に示すように、ネイティブの
        <code>&lt;button&gt;</code>
        を使用してアクセス可能なキーボードコントロールを提供します。
      </td>
    </tr>
    <tr>
      <td>1.4.3 最低限のコントラスト (AA)</td>
      <td>
        <p>
          背景と前景のコンテンツの間の色のコントラストは、読みやすさを確実なものとするための最低限のレベルであるべきです。
        </p>
        <ul>
          <li>
            テキストとその背景のコントラスト比は少なくとも 4.5:1 であるべきです。
          </li>
          <li>
            見出し（またはそれよりも大きい）テキストの比は、少なくとも 3:1 であるべきです。 大きいテキストは、少なくとも 18 ポイント、または 14 ポイントの太字として定義されます。
          </li>
        </ul>
      </td>
      <td>
        <a href="/ja/docs/Web/Accessibility/Understanding_WCAG/Perceivable/Color_contrast"
          >色のコントラスト</a
        >と<a
          href="/ja/docs/Learn/Accessibility/CSS_and_JavaScript#色とそのコントラスト"
          >色とそのコントラスト</a
        >を参照してください。
      </td>
    </tr>
    <tr>
      <td>1.4.4 テキストのサイズ変更 (AA)</td>
      <td>
        テキストサイズが倍になったときに、ページが読みやすく使えるべきです。
        つまり、デザインはレスポンシブであるべきで、テキストサイズを大きくしてもコンテンツにアクセス可能であることを意味します。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>1.4.5 テキストの画像 (AA)</td>
      <td>
        テキストが仕事をするようなコンテンツを提示するために画像を使用しては<strong>いけません</strong>。
        例えば、画像がほとんどテキスト形式の場合、画像だけでなくテキストも使用して表現できます。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>1.4.6 強化されたコントラスト (AAA)</td>
      <td>
        <p>これは、基準 1.4.3 に従い、その上に構築されます。</p>
        <ul>
          <li>
            テキストとその背景のコントラスト比は少なくとも 7:1 であるべきです。
          </li>
          <li>
            見出し（またはそれよりも大きい）テキストの比は少なくとも 4.5:1 であるべきです。 大きいテキストは、少なくとも 18 ポイント、または 14 ポイントの太字として定義されます。
          </li>
        </ul>
      </td>
      <td>
        <a
          href="/ja/docs/Learn/Accessibility/CSS_and_JavaScript#色とそのコントラスト"
          >色とそのコントラスト</a
        >を参照してください。
      </td>
    </tr>
    <tr>
      <td>1.4.7 背景音が小さいか無い (AAA)</td>
      <td>
        話し言葉を主な特徴とする録音済みの音声記録は、背景の雑音を最小限に抑えるようにしてください。そうするとコンテンツが理解しやすくなります。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>1.4.8 視覚的表現 (AAA)</td>
      <td>
        <p>テキストコンテンツの表現では、次のことが当てはまります。</p>
        <ul>
          <li>前景色と背景色は、ユーザーが選択できるようにするべきです。</li>
          <li>
            テキストブロックは、読みやすくするために、80 文字（またはグリフ）以下の幅にしてください。
          </li>
          <li>
            テキストは、両端揃えにするべきではありません（例えば、<code
              >text-align: justify;</code
            >）。
          </li>
          <li>
            行の高さは、段落内ではテキストサイズの 1.5 倍以上（例えば、 <code>line-height: 1.5;</code>）、段落間ではテキストサイズの 2.25 倍以上（例えば、 <code>padding: 2.25rem;</code>）にするするべきです。
          </li>
          <li>
            テキストサイズが2倍になったときに、コンテンツのスクロールが必要になるべきではありません。
          </li>
        </ul>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>1.4.9 テキストの画像（例外なし） (AAA)</td>
      <td>
        テキストは、純粋に装飾である（すなわち、それがいかなる内容も伝えない）か、または他の方法で提示することができない限り、画像の一部として提示するべきではありません。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        1.4.10 リフロー (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        <ul>
          <li>
            左書きの言語（英語など）や右書きの言語（アラビア語など）では、水平スクロールをしないでください。
          </li>
          <li>
            縦書きの言語（日本語など）では、垂直スクロールをしないでください。
          </li>
          <li>
            使用法や意味のために 2 次元レイアウトを必要とするコンテンツの部分を除きます（大きなデータ表など）。
          </li>
        </ul>
      </td>
      <td>
        <a href="https://www.w3.org/WAI/WCAG21/Understanding/reflow.html"
          >リフローを理解する</a
        >（英語）
      </td>
    </tr>
    <tr>
      <td>
        1.4.11 テキスト以外のコントラスト (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        ユーザーインターフェイスコンポーネントとグラフィックオブジェクトの最低限のカラーコントラスト比は 3:1 です。
      </td>
      <td>
        <a
          href="https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html"
          >テキスト以外のコントラストを理解する</a
        >（英語）
      </td>
    </tr>
    <tr>
      <td>
        1.4.12 テキストの間隔 (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        <p>
          次のスタイルを適用しても、コンテンツや機能が失われることはありません。
        </p>
        <ul>
          <li>
            行の高さ（行間）をフォントサイズの 1.5 倍以上にします。
          </li>
          <li>
            後続の段落との間隔をフォントサイズの 2 倍以上にします。
          </li>
          <li>
            文字間隔（トラッキング）をフォントサイズの 0.12 倍以上にします。
          </li>
          <li>単語間隔をフォントサイズの 0.16 倍以上にします。</li>
        </ul>
      </td>
      <td>
        <a href="https://www.w3.org/WAI/WCAG21/Understanding/text-spacing.html"
          >テキストの間隔を理解する</a
        >（英語）
      </td>
    </tr>
    <tr>
      <td>
        1.4.13 ホバーまたはフォーカスにおけるコンテンツ (AA)
        <a href="https://www.w3.org/TR/WCAG21/#new-features-in-wcag-2-1"
          >2.1 で追加</a
        >（英語）
      </td>
      <td>
        <p>
          追加のコンテンツがホバーやキーボードフォーカスに連動して現れたり消えたりします。
          この達成基準では、満たす必要がある次の 3 つの条件を指定します。
        </p>
        <ul>
          <li>却下可能（閉じたり取り除いたりすることが可能）。</li>
          <li>
            ホバーリング可能（追加のコンテンツは、ポインターが上にあるときは消えません）。
          </li>
          <li>
            永続的（追加のコンテンツは、ユーザーの操作なしでは消えません）。
          </li>
        </ul>
      </td>
      <td>
        <a
          href="https://www.w3.org/WAI/WCAG21/Understanding/content-on-hover-or-focus.html"
          >ホバーまたはフォーカスにおけるコンテンツを理解する</a
        >（英語）
      </td>
    </tr>
  </thead>
</table>

> [!NOTE]
> [ガイドライン 1.4: 識別可能: 背景から前景を分離するなど、ユーザーがコンテンツを見やすく、聞き取りやすくする](https://www.w3.org/TR/WCAG21/#distinguishable)（英語）に関する WCAG の説明も参照してください。

## 関連情報

- [WCAG](/ja/docs/Web/Accessibility/Guides/Understanding_WCAG)
  1. 知覚可能
  2. [操作可能](/ja/docs/Web/Accessibility/Guides/Understanding_WCAG/Operable)
  3. [理解可能](/ja/docs/Web/Accessibility/Guides/Understanding_WCAG/Understandable)
  4. [堅牢](/ja/docs/Web/Accessibility/Guides/Understanding_WCAG/Robust)
