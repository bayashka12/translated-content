---
title: HTTP/1.x のコネクション管理
slug: Web/HTTP/Guides/Connection_management_in_HTTP_1.x
l10n:
  sourceCommit: ad5b5e31f81795d692e66dadb7818ba8b220ad15
---

コネクション管理は、 HTTP の重要なトピックです。コネクションを開いたり管理したりすることは、ウェブサイトやウェブアプリケーションのパフォーマンスに大きな影響を与えます。HTTP/1.x では「短命な (short-lived) コネクション」、「持続的な (persistent) コネクション」、「HTTP パイプライン」といったモデルがあります。

HTTP は、クライアントとサーバーの間のコネクションを提供するトランスポートプロトコルを、たいてい TCP に依存しています。初期のころ、HTTP が使用するコネクションの制御モデルは 1 種類でした。それらのコネクションは短命です。リクエストの送信が必要になるたびに新たなコネクションを作成して、回答を受け取るとコネクションを閉じていました。

このシンプルなモデルは、先天的なパフォーマンスの制約を抱えていました。それぞれの TCP コネクションを開く処理は、リソースを消費します。いくつかのメッセージを、クライアントとサーバーの間で交換しなければなりません。リクエストの送信が必要になると、ネットワークの遅延や帯域がパフォーマンスに影響を与えます。現代のウェブページは、必要な情報を提供するために多くのリクエスト (1 ダース以上) を必要としており、初期のモデルが非効率であることを実証しています。

HTTP/1.1 で、新たなモデルを 2 種類導入しました。持続的なコネクションモデルは、連続したリクエストの間はコネクションを開き続けておくことで、新たなコネクションを開始するために必要な時間を削減します。 HTTP パイプラインモデルはさらに 1 歩進んで、回答を待っている間も複数の連続したリクエストを送信して、ネットワークの遅延の大部分を削減します。

![HTTP/1.x の 3 つのコネクションモデルにおけるパフォーマンスの比較: 短命なコネクション、持続的なコネクション、 HTTP パイプライン](http1_x_connections.png)

> [!NOTE]
> HTTP/2 では、コネクションの管理モデルをさらに追加しました。

特筆すべき重要なポイントとして、 HTTP のコネクション管理は隣接したノードの間のコネクション、すなわち[エンドツーエンド](/ja/docs/Web/HTTP/Reference/Headers#エンドツーエンドヘッダー)ではなく[ホップバイホップ](/ja/docs/Web/HTTP/Reference/Headers#ホップバイホップヘッダー)に適用されることがあります。クライアントと最初のプロキシーの間で使用するモデルと、プロキシーと宛先サーバー（または任意の中間プロキシー）の間で使用するモデルが異なることもあります。{{HTTPHeader("Connection")}} や {{HTTPHeader("Keep-Alive")}} といったコネクションモデルの定義にかかわる HTTP ヘッダーは、中間のノードが値を変更できる [ホップバイホップ](/ja/docs/Web/HTTP/Reference/Headers#ホップバイホップヘッダー)ヘッダーです。

関連するトピックとしては、 HTTP コネクションのアップグレードの概念、つまり HTTP/1.1 コネクションが TLS/1.0、 WebSocket、 又は平文の HTTP/2 のような異なるプロトコルにアップグレードされたことが挙げられます。この[プロトコルのアップグレードメカニズム](/ja/docs/Web/HTTP/Guides/Protocol_upgrade_mechanism)は他の場所でもっと詳しく文書化されています。

## 短命なコネクション

短命なコネクションは HTTP の初期のモデルであり、 HTTP/1.0 の既定のモデルです。それぞれの HTTP リクエストは、自身のコネクションで完結します。すなわち、各 HTTP リクエストの前に TCP のハンドシェイクが発生します。また、それらが連続します。

TCP のハンドシェイク自体は時間がかかる処理ですが、 TCP のコネクションはその負荷に適応しており、より持続するコネクションによって効率が向上します。短命なコネクションは TCP の効率化機能を使用しておらず、また新たなコールド状態のコネクションで送信することに固執するため最適な状態よりもパフォーマンスが低下します。

このモデルは HTTP/1.0 で使用する既定のモデルです ({{HTTPHeader("Connection")}} ヘッダーが存在しない、あるいはヘッダーの値が `close` である場合)。 HTTP/1.1 では、 {{HTTPHeader("Connection")}} ヘッダーで `close` の値が送信された場合に限り、このモデルを使用します。

> [!NOTE]
> とても古い (持続的なコネクションをサポートしていない) システムを扱う場合を除き、あえてこのモデルを使用する理由はありません。

## 持続的なコネクション

短命なコネクションには、大きな問題点が 2 つあります。新しいコネクションを確立するためにかなり時間がかかること、および下層の TCP コネクションは何度も使用するとき (ウォーム状態のコネクション) しかパフォーマンスが向上しないことです。これらの問題を緩和するため、 HTTP/1.1 より前から持続的なコネクションの概念が考えられてきました。あるいは、*キープアライブ接続*と呼ばれることもあります。

持続的なコネクションはしばらくの間開かれたままであり、いくつかのリクエストで再使用できます。よって新たな TCP ハンドシェイクにかかる時間を節約して、 TCP のパフォーマンス向上機能を活用します。このコネクションはいつまでも開かれたままにはなりません。アイドル状態のコネクションはしばらく後に閉じられます (サーバーは、コネクションを開き続けておくべき最小時間を決めるために {{HTTPHeader("Keep-Alive")}} ヘッダーを使用するでしょう)。

持続的なコネクションには欠点もあります。アイドル状態でもサーバーのリソースを消費しており、高負荷状態では {{Glossary("Denial of Service", "DoS 攻撃")}} を招く可能性があります。この場合、持続的ではない接続はアイドル状態になるとすぐに閉じられますので、パフォーマンスが向上するでしょう。

HTTP/1.0 の既定のコネクションは、持続的ではありません。 {{HTTPHeader("Connection")}} を `close` 以外の何か、通常は `retry-after` に設定すると、持続的になります。

HTTP/1.1 では既定で持続的であり、ヘッダーは不要になりました (ただし HTTP/1.0 へのフォールバックが必要な場合の防衛策として、通常はヘッダーを追加します。)。

## HTTP パイプライン

> [!NOTE]
> HTTP パイプラインは、現代のブラウザーでは既定で有効化されていません。
>
> - 不具合がある[プロキシー](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%82%AD%E3%82%B7)がまだ一般的であり、これらは開発者が容易には予見あるいは診断できない、奇妙かつ一定しない挙動の原因になります。
> - パイプラインの正しい実装は複雑です。転送するリソースのサイズ、効果的な [RTT](https://ja.wikipedia.org/wiki/%E3%83%A9%E3%82%A6%E3%83%B3%E3%83%89%E3%83%88%E3%83%AA%E3%83%83%E3%83%97%E3%82%BF%E3%82%A4%E3%83%A0) および帯域が、パイプラインによる改善に対して直接的な影響力を持ちます。これらがわからなければ、重要なメッセージがそうでないメッセージより遅れる場合があります。重要さの概念は、ページのレイアウト中に高まります!よって、 HTTP パイプラインはほとんどの場合でわずかな改善にしかなりません。
> - パイプラインは、 {{glossary("head of line blocking", "head-of-line blocking")}} の問題に左右されます。
>
> これらの理由により、パイプラインはよりよいアルゴリズムである*多重化*に置き換えられました。こちらは HTTP/2 で使用されています。

既定で、[HTTP](/ja/docs/Web/HTTP) リクエストは順次発行されます。次のリクエストは、現在のリクエストのレスポンスが到着してから発行されます。これはネットワークの遅延や帯域の制約を受けるため、次のリクエストがサーバーで*見える*ようになるまでにかなりの遅延が発生する可能性があります。

パイプラインは連続したリクエストを同一の持続的なコネクションで、回答を待たずに処理します。これは、コネクションの遅延を回避します。理論上は、2 つのリクエストを同じ TCP メッセージに収めた場合でもパフォーマンスが向上するでしょう。HTTP リクエストのサイズ面での需要は増え続けていますが、典型的な [MSS](https://ja.wikipedia.org/wiki/%E6%9C%80%E5%A4%A7%E3%82%BB%E3%82%B0%E3%83%A1%E3%83%B3%E3%83%88%E3%82%B5%E3%82%A4%E3%82%BA) （最大セグメントサイズ）の大きさならば、いくつかのシンプルなリクエストが十分に収まります。

パイプライン化できない HTTP リクエストもあります。 {{glossary("idempotent","べき等")}} なメソッドである {{HTTPMethod("GET")}}, {{HTTPMethod("HEAD")}}, {{HTTPMethod("PUT")}}, {{HTTPMethod("DELETE")}} だけが安全に再実行できます。これらは失敗しても、パイプラインの内容を再実行できます。

現在、すべての HTTP/1.1 に準拠するプロキシーやサーバーはパイプラインをサポートしているはずですが、実際は多くの制限があります。さまざまな理由で、現行のブラウザーはパイプラインを既定で有効化していません。

## ドメインシャーディング

> [!NOTE]
> 特別に必要である場合を除き、この非推奨の技術は使用しないでください。代わりに、 HTTP/2 に切り替えてください。 HTTP/2 では、ドメインシャーディングは有用ではありません。 HTTP/2 のコネクションは、並行した優先度がないリクエストをより上手に扱うことができます。また、ドメインシャーディングはパフォーマンスに悪影響を与えます。ほとんどの HTTP/2 実装では、最終的にドメインシャーディングに戻る [connection coalescing](https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/) と呼ばれる技術を使用しています。

HTTP/1.x のコネクションはリクエストが整理されることもなく連続するため、十分な帯域を使用できない状況では最適化できません。その解決策として、ブラウザーはそれぞれのドメインに対して複数のコネクションを開いて、リクエストを並行して送信します。既定では一度に 2 から 3 つのコネクションですが、現在は主に 6 つの並列したコネクションへ増えています。この数をさらに増やそうとすると、サーバー側で [DoS](/ja/docs/Glossary/Denial_of_Service) 防御が発動する危険性があります。

サーバーがウェブサイトやウェブアプリケーションのレスポンスを早くしたい場合、より多くのコネクションを開かせることが考えられます。例えば、すべてのリソースを同じドメイン `www.example.com` で持つのではなく、`www1.example.com`、`www2.example.com`、`www3.example.com` といった複数のドメインに分散させることができます。それぞれのドメインは*同じ*サーバーに名前解決されて、ウェブブラウザーはドメインごとに 6 つのコネクションを開きます（この例では、コネクション数が 18 に増加します）。この技術は*ドメインシャーディング*と呼ばれます。

![ドメインシャーディングを使用しない場合、クライアントは最大 2 つのリクエストが並列で実行されるドメインから 6 つの画像をリクエストします。ドメインシャーディングを使用すると、画像は 2 つのドメインから利用でき、クライアントは 4 つのリクエストを並列で実行し、画像をより短い時間でダウンロードすることができます。](httpsharding.png)

## まとめ

接続の管理が改善されたことで、HTTP のパフォーマンスが大幅に向上しました。HTTP/1.1 または HTTP/1.0 では、少なくともアイドル状態になるまでは持続的な接続を使用することが最高のパフォーマンスにつながります。しかし、パイプライン処理の失敗により、より優れた接続管理モデルが設計され、HTTP/2 に組み込まれました。

## 関連情報

- [HTTP の進化](/ja/docs/Web/HTTP/Guides/Evolution_of_HTTP)
- 用語集:
  - {{glossary('HTTP')}}
  - {{glossary('HTTP_2', 'HTTP/2')}}
  - {{glossary('QUIC')}}
  - {{glossary('Round Trip Time', 'ラウンドトリップタイム')}}
  - {{glossary('TCP slow start')}}
  - {{glossary('TLS')}}
  - {{glossary('TCP')}}
