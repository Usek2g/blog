---
layout: post
title:  "ウェビナー「こう出たR6秋セキスぺ解答解説」"
date:   2025-03-18 21:15:27 +0900
categories: diary
img: reiwa6-autumn-security-specialist-exam.jpg # Add image post (optional)
tags: [seminar] # add tag
description: 昨年秋の情報処理安全確保支援士（旧セキスぺ）試験はどんな問題だったのだろう
---

ITエンジニア向け勉強会サービス「CONNPASS」特に転職前はお世話になりました。僕の転職後すぐコロナ禍になり、勉強会というものも出来なくなりましたが、かわりにオンラインによるウェビナーは盛んになりましたね。

久しぶりにCONNPASSのイベントに参加しました。タイトルは

[「こう出たR6秋セキスペ解答解説」 ](https://s-jaws.connpass.com/event/340397/)

主催はJP-RISSA（情報処理安全確保支援士会）。昨年秋の情報処理安全確保支援士試験についてどのような問題が出たのかを解説するとのこと。
僕が合格した当時はセキュリティスペシャリスト試験という名称でした。時が経ち、今はどのような問題が出題されているのか興味があり視聴しました。

まず、午前２の難易度が上がったとのこと。過去問と同じ問題が減り、新規の問題が増えたとのことです。丸暗記で余裕、とはならなくなったのが難易度アップの理由と推測されていました。
ここで「今の時代AIを使えば4択問題を大量に作ることはたやすいのでは」という面白い推測が発表者からありました。たしかに。勉強にAIが活用できるのはさんざん書いてきましたが、出題する側もAIを使うことができますものね。

また、曖昧な質問の仕方や文字数制限がほぼ撤廃されたこと、実際に行うことを書かせる出題など、暗記ではなく考えを述べさせるような出題が多かったことで午後も難化。令和の中でもっとも低い合格率になった原因はここにあるのでは、と推測されていました。

午後の問題は

## 午後問１＝インシデントレスポンス
- ログを読ませる
- クラウド側プロキシサービスを使うには専用のプログラムをクラウンとPCにインストールする必要があるというリアリティ
- DLPという用語を自分が導き出す必要あり

## 午後問２＝ドメイン名変更を機にしたメールサービス導入
ある会社が社名変更にともないドメインの変更が必要になるというストーリー
ついでにメールシステムも刷新し、DMARC対応も進めようという話は業務内容を思い出させます。
社名変更前のドメインは一生持ち続ける覚悟を持つのが一番安全です。しかしそれだとお金がもったいないのでドメイン更新しないと言うケースはよくあります。
キャンペーンサイトのドメインはアクセス数が多いことや多くのサイトにリンクが張られているから検索におけるドメインパワーがあり、他の会社が買い取って利用することがあります。

例えばお名前.comではこのように使われなくなった価値あるドメインをオークション形式で打っています。

https://www.onamae.com/campaign/auction/


この問題は、悪意ある人間が過去企業や官公庁がキャンペーンで一時的にで利用されていたドメインを買い取り、詐欺サイトを作る危険性です。この手のキャンペーンサイトのURLはキャンペーン終了後も公式サイトや個人ブログの記事にリンクが残ります。第三者がこのドメインを取得して自分のサイトにアクセス流入させる行為を[ドメインドロップキャッチ](https://ja.wikipedia.org/wiki/%E3%83%89%E3%83%AD%E3%83%83%E3%83%97%E3%82%AD%E3%83%A3%E3%83%83%E3%83%81)といいます。

対策としては、キャンペーンサイトのために別ドメインを取得せず、既存ドメインのサブドメインやサブディレクトリ配下にキャンペーンサイトを作るのが有効です。サブドメインのほうが管理は楽ですが、インターネット上ではサブディレクトリのほうが検索時のドメインパワーは強いとされます。
が、なんでもAIに聞いて答えを得る時代において、検索サービスの持つドメインパワーというものは低下していきそうな気がしますね。

## 午後問３＝ECサイトのクレジットカードの漏洩
この手口は昨年の某コーヒーショップのインシデントのやり方にそっくりだったと話題になったそうです。試験が単なる知識の発表の場ではなく、実際に起こるリスクがあること、どう対応するかなど実践的であることを再認識ですね。
SQLインジェクション、クロスサイトスクリプティングなどおなじみのセキュリティ対策とセキュアコーディングの知識が問われたとのことです。

## 午後問４＝セキュリティ診断
他3問の技術の話しからは少し外れたISMS的な話しで、自分ならこの問題をまずは選択しますね。

- 個人情報収集しちゃってる
- IDがランダムじゃなくてYYYYMMDD推測可能

などセキュリティ的な問題点と解決策を問われる問題だったとのことです。しかし
「何が問題なのか・何が危険なのか」では不正解で、「どうすればば改善されるか」まで回答して初めて満点がもらえる問題があり、問題文からはぱっと見そこまでは読めないため、ここで原点をくらった人が多かったのではないか、と分析されていました。

---

久しぶりにウェビナーに参加しましたが、とても有意義でした。自分がセキスぺを取得した時どのような問題を解いたかはもう忘れてしまいましたが、午後問題に会社の統合によるドメイン刷新やメールドメイン変更対応におけるセキュリティ問題や、昨年実際に発生したセキュリティインシデントと類似した問題が出題され、単なる知識詰め込みの試験ではなく、実際業務のセキュリティ対応に密接に紐づいた出題がされていることを再認識しました。またDMARCやIdPなど頻出した出題内容は現在重要視されるセキュリティだと考えられ、学びがありました。

だからこそ、情報処理安全確保支援士の資格の価値をもっと高めてくれ、と何度も言っていますが・・・。