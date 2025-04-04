---
title: 307 Temporary Redirect
slug: Web/HTTP/Reference/Status/307
original_slug: Web/HTTP/Status/307
---

{{HTTPSidebar}}

{{Glossary("HTTP")}} の **`307 Temporary Redirect`** リダイレクトステータスレスポンスコードは、リクエストされたリソースが一時的に {{HTTPHeader("Location")}} で示された URL へ移動したことを示します。

元のリクエストのメソッドと本文は、リダイレクトされたリクエストを行う際に再利用されます。使用されるメソッドを {{HTTPMethod("GET")}} に変更したい場合は、代わりに {{HTTPStatus("303", "303 See Other")}} を使用してください。これは {{HTTPMethod("PUT")}} メソッドへのレスポンスで、アップロードされたリソースではないところで「XYZ のアップロードに成功しました」のような確認メッセージを表示したい場合に便利です。

`307` と {{HTTPStatus("302")}} の唯一の違いは、 `307` はリダイレクトされたリクエストが行われるときに、メソッドと本文が変更されないことが保証されることです。 `302` では、一部の古いクライアントは不正にメソッドを {{HTTPMethod("GET")}} に変更してしまいます。 `GET` 以外のメソッドと `302` による挙動はウェブで予測することができず、 `307` の挙動は予測できます。 `GET` リクエストでは、両者の挙動は同じです。

## ステータス

```
307 Temporary Redirect
```

## 仕様書

| 仕様書                                              | 題名                                                          |
| --------------------------------------------------- | ------------------------------------------------------------- |
| {{RFC("7231", "307 Temporary Redirect" , "6.4.7")}} | Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content |

## ブラウザーの対応

{{Compat}}

## 関連情報

- {{HTTPStatus("302", "302 Found")}}: このステータスコードと同等ですが、 {{HTTPMethod("GET")}} 以外の時にメソッドが変更されるかもしれない。
- {{HTTPStatus("303", "303 See Other")}}: 使用されるメソッドを {{HTTPMethod("GET")}} に変更する一時リダイレクト。
- {{HTTPStatus("301", "301 Moved Permanently")}}: 永久リダイレクト
