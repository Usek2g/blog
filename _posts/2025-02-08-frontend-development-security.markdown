---
layout: post
title:  "【ブックレビュー】フロントエンド開発のためのセキュリティ入門"
date:   2025-02-08 10:20:27 +0900
categories: bookreview
img: frontend-development-security.png # Add image post (optional)
tags: [programming,security] # add tag
description: フロントエンドのお約束の脆弱性とその対策について手を動かしながら真似べる本
---

これまで僕が書評を書いていたセキュリティ関係の本はインフラだったり、組織に対する内容だったりと、アプリケーションの実装に関連する本は少なかったように思えます。しかしシステム開発のメーンストリームであるアプリケーションのセキュリティ対策を知識として知ることは重要ですし、アプリ開発メンバーの連携協調してプロジェクトを進めるためにも、相手が何を言っているのかを理解することは必須のスキルです。
僕はかつてはソフトウェアエンジニアとしてシステム開発も携わっていたので、アプリに関する知見も多少はあります。それが今の仕事で有利に働いていることは間違いなく、この辺りは抜かりなく研鑽を続けていきたいと考えています。

本書籍はWebセキュリティの必須知識である「CORS」「XSS」「CSRF」などについてフロントエンドにhtml+JavaScript、バックエンドにnode.js+expressを用いて、実際に手を動かしながらブラウザ側とWebサーバ側のセキュリティ対策の実際の方法について学ぶことができます。本書にあるように、セキュリティ対策は自分で組み込むのではなくライブラリの利用が推奨されています。なぜならライブラリは多くのすぐれたエンジニアが安全、堅牢なセキュリティ対策を作り、メンテしてくれているモノなので、個人が実装するより絶対的に安全だからです。しかしライブラリを使う場合も、根幹の部分を知ることは大切です。

XSS対策にサニタイジング、というのはもはや当たり前であり、インフラエンジニアの自分でも当然知っている話でしたが、Webサーバ側でレスポンスヘッダに「「Strict-Transport-Security」や、OORSヘッダ「Access-Control-Allow-Origin」を付与して返すことについては知識を十分に持っておらず、たいへん参考になりました。

プリフライトリクエストについては最近仕事の中でアプリケーション開発者と会話で挙がったこともあり、「もっと早くこの本を読んでいれば」という感想でした。

Gemini:
> 具体的には、以下の条件のいずれかに該当する場合、ブラウザは自動的にプリフライトリクエスト（OPTIONSリクエスト）を送信します。

> リクエストメソッドがGET、HEAD、POST以外の場合（PUT、DELETE、PATCHなど）。
> POSTメソッドであっても、Content-Typeヘッダーがapplication/x-www-form-urlencoded、multipart/form-data、text/plain以外の場合（application/jsonなど）。
> リクエストにカスタムヘッダーが含まれている場合（X-Custom-Header: valueなど）

> プリフライトリクエストの流れ

> ブラウザ: メインリクエスト（この場合はDELETEリクエスト）を送信する前に、OPTIONSリクエスト（プリフライトリクエスト）を送信します。このOPTIONSリクエストには、以下のヘッダーが含まれます。
> Origin: リクエスト元のオリジン（例：http://localhost:3000）。
> Access-Control-Request-Method: メインリクエストで使用するメソッド（この場合はDELETE）。
> Access-Control-Request-Headers（必要に応じて）: メインリクエストで使用するカスタムヘッダー。

> サーバー: OPTIONSリクエストを受け取り、CORSポリシーに基づいてレスポンスを返します。レスポンスには、以下のヘッダーが含まれる可能性があります。
> Access-Control-Allow-Origin: アクセスを許可するオリジン（例：http://localhost:3000または*）。
> Access-Control-Allow-Methods: 許可するHTTPメソッド（例：GET, POST, DELETE）。
> Access-Control-Allow-Headers: 許可するカスタムヘッダー。
> Access-Control-Max-Age: プリフライトリクエストの結果をキャッシュする時間（秒単位）。

> ブラウザ: サーバーからのレスポンスを検証します。
> Access-Control-Allow-Originがリクエスト元のオリジンと一致するか、または*であるかを確認します。
> Access-Control-Allow-Methodsにメインリクエストのメソッドが含まれているかを確認します。
> Access-Control-Allow-Headersにメインリクエストで使用するカスタムヘッダーが含まれているかを確認します。
> 成功の場合: ブラウザはメインリクエスト（DELETEリクエスト）を送信します。
> 失敗の場合: ブラウザはメインリクエストを送信せず、CORSエラーとして処理します

CORSについては「なぜ静的htmlにクロスオリジンである別ドメインのリンク(aタグ)を埋め込んだ場合は拒否されないのか」という初歩的な疑問が今更沸いたのですが、こちらもLLMであるGoogle Geminiと並走しながら学習することで理解することができました。

Gemini:
> これは、imgタグやlinkタグ、scriptタグなど、一部の要素はCORSの制約を受けないためです。これらの要素は、クロスオリジンリソースを埋め込むことが歴史的に許容されてきました。
> 具体的には、以下のリソースはCORSの制約を受けません。
> ・imgタグの画像
> ・videoタグやaudioタグのメディア
> ・linkタグのCSS
> ・scriptタグのJavaScript
> ・frameタグやiframeタグで読み込まれるコンテンツ

僕:
> scriptタグやiframeタグでクロスオリジンのコンテンツをデフォルトで拒否していないのは危険ではないでしょうか？

Gemini:
> scriptタグやiframeタグがデフォルトでクロスオリジンのコンテンツを許可しているのは、歴史的な経緯によるものです。しかし、これはセキュリティ上のリスクを含んでいるため、現代のWebセキュリティではCSP、SRI、SameSite Cookie、sandbox属性などの対策を組み合わせて、これらのリスクを軽減しています。
> 特にCSPは、scriptタグによるXSS攻撃を防ぐための最も効果的な手段の一つであり、現代のWebアプリケーション開発においては必須のセキュリティ対策と言えるでしょう。

> つまり、デフォルトで拒否していないことは確かに危険性を含んでいますが、現代のWeb開発ではこれらの危険性を認識した上で、適切なセキュリティ対策を講じることが重要です

一昔前なら、学生のこのような質問についての回答は、先輩や先生が、必要に応じてネットで調べて回答していたはず。学生が自力で上記知識をまとめるにはかなりの時間を検索に費やさなければいけなかったはずです。それが今や一瞬で比喩などを用いながら腑に落ちる回答を得られるとは…LLM（AIチャット）の凄さを再認識しました。

先日セキュリティとは関係ないのですが、Webアプリ開発に用いられるReact.jsについても勉強しました。その際ＡＩにいろいろとサポートしてもらいました。大学時代、学生につきっきりで大学院生の先輩がTA/SAとして教えてくれたことを思い出しました。今や生徒一人一人にTA/SAがいつでもどこでも付きっきりで対応してくれるのですから、学ぶ気持ちがある人には便利な時代になった一方で、卒論や課題をAIの回答を●写しで提出するなど、「何のために学んでいるのですか」と本末転倒な事態も起きています。