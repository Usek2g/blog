---
layout: post
title:  "【ブックレビュー】OAuth 徹底入門"
date:   2024-07-28 12:20:27 +0900
categories: bookreview
img: oauth-thorough-introduction.jpg
 # Add image post (optional)
tags: [security,programming] # add tag
description: OAuth2.0の仕組みから構築への実用的な指針までの詳細な解説
---
CISSPの勉強中ですが、かなり寄り道してOAuthの勉強をしていました。
OAuth、というか正確にはOpenId Connectを業務で利用しており、業務のアプリチームの会話についていかなくてはいけないことと、業務内でよく使われているのであればそれについて理解しなければ、その実装のセキュリティリスクについて想像もできないことから今回この本を取りました。そもそもその両者の違いがネットで調べてもちんぷんかんぷんだったのもあります。

OAuthはどういう場所で使われているかというと、一時期は流行ったＸ(旧twitter)と連携し、過去のツイートを分析し、診断結果をツイートする診断メーカーをイメージすると良いかと。診断メーカーを利用する際皆さんはtwitterのIDとパスワードでブラウザで認証し、その際「過去の自分のツイートを読み取ること」「自分のアカウントでツイートすること」を許可にチェックを入れてボタンを押すはずです。この"許可"こそがOAuthです。以下が登場人物です。

- リソース所有者・・・私たち
- クライアント・・・・診断メーカー
- 保護対象リソース・・twitter（投稿機能や過去の投稿データ）　←単なるデータ置き場ではなく、認可サーバが返すアクセス・トークンを元に処理を行うため"保護対象リソースサーバ"のほうが役割のイメージが湧くと思います
    - 認可サーバ・・・twitter側の認可サーバ
        - 認可エンドポイント・・・・・Web API。ここに向けてクライアントは認可を求める
        - トークンエンドポイント・・・

OAuthはクライアントにリソース所有者が自身が実行できる保護対象リソースの権限の一部を委譲させ、代わりに実行させるプロトコルです。そしてリソース所有者の権限を委譲する機能を持つのが認可サーバ。認可を行う認可エンドポイントは”認可コード”をクライアントに返します。クライアントはこの認可コードをトークン・エンドポイントに対して送付すると、トークンエンドポイントは保護対象リソースへアクセスするためのアクセス・トークン（投稿ができるよ、この人のタイムラインを閲覧できるよ、という情報を持ったクレデンシャル）をレスポンスで渡します。このアクセストークンを使ってクライアントは保護対象リソースにアクセスします。

OAuthは「誰がこの認可の委譲を許可したよ」「どの権限を付与したよ」は分からず、「権限の委譲が行われたよ」というトークンを認可サーバからクライアントに返すプロトコル。そのトークンを分割して必要な情報を解釈するのはクライアントと保護対象リソースサーバの間で行われます。

文章で読んでも「？」となってしまうのは分かります。自分で書いていても上手く説明できてないな…と思いますから。図で見ると分かりやすいのですが。そしてその図と、実際のクライアントおよび保護対象リソースサーバ内のコーディングが手を動かしながら学べるのがこの本です。OAuthはシンプルな構造と度々書かれていますが、実際にはいくつものプロトコルを組み合わせて使います。実装の方法も複数あり、OAuthは「これを使え」という決めはしていません（これを利用しろ、という規約は特定の業界で作っていたりしますが）。そのため一度に学ぼうとすると頭が爆発してしまうでしょう(^^;)

この本はOAuthを0から1つずつ順を追って解説してくれているため分かりやすいです（それでも一回読んで理解できるものではありませんが…）、各構成要素の実装方法から脆弱性とその対策（徳丸本で学んだ知識が活きます）、さらに応用である認証機能や第三者に権限を委譲する方法なども紹介しています。発売は5年前と古いため最新の情報ではないかもしれませんが、基礎は変わらないはず。OAuthについて0から学ぶのであればふさわしい本と思います。

この本を読んでOAuthとOpenID Connect(OIDC)の違いについて理解できました。OIDCはOAuthの拡張機能で、OAuthの土台の上に認証機能を追加します。OAuth自体は認証機能を持たず（そこは実装側に任せています）認可に特化したプロトコルです。ここで「認証」と「認可」の違いを説明しますと

認証・・・本人であることを確かめ、証明する
認可・・・リソースに何ができるか(Read/Write/Execute)を許可する

少し違いますね。しかし世の中認証と認可はセットで扱われることが多く、多く普及したOAuthに認証機能を付けたいのは現場の自然なニーズだったのかもしれません、両者が混合してしまうのもやむなしかと。