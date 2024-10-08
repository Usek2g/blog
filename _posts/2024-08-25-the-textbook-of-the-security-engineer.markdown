---
layout: post
title:  "【ブックレビュー】セキュリティエンジニアの教科書"
date:   2024-08-25 12:20:27 +0900
categories: bookreview
img: textbook-of-the-security-engineer.jpg
 # Add image post (optional)
tags: [security] # add tag
description: 特にインシデント周りの記述が充実している本です
---

2024年の上半期を振り返ると、毎日のように情報漏洩とランサムウェアのニュースが流れて、セキュリティに難があるのがもはや当たり前のような時代になってしまっているな、という感じがあります、そんな状況下で読んだこの本はタイトル通り教科書的かつ初歩的な内容となっていますが、何事も基礎が大切であるということは言うまでもありません。CISSPでも出題される知識も記載されているので、復習がてら読みました。過去の記事にも書いていたかもしれませんが、この本で紹介されているようなリスク分析・評価と対策を1度会社でやったことがあります。その時は今より知識も不足していて、周囲に対しても協力を上手に得ることができず、中途半端な状態で終わりました。そも、各事業部のメンバーにとっては（こんなことやっている時間はないんだけどな…）と思われていたかもしれません。

この本の前半はどのような本でも紹介されているセキュリティの基礎知識なのですが、中盤からは脆弱性対応に使用するフレームワークやテストの方法、後半からはインシデントハンドリングフローへの理解など詳しく図で載っているのがとてもありがたいです。CSIRTに関する記事はネットに散見されるが本は少ない印象があります。また手を付けると終わりのない作業になるため、この本が基本レベルの記載で留まっているのが逆にありがたいです。まずここを抑えればよいと考えれられるので。ただセキュリティインシデントの対応手順を作る必要があることは分かっているので、参考になるサンプル手順書を紹介してほしかったなぁ。

セキュリティオペレーションセンター(SOC)の役割：リアルタイム監視、ログ分析、異常なふるまいの検知、インシデントの検知と暫定対応です。中小企業だとCSIRTが利用するものと定義づけられる、と自分は思っているのですが、（そもそもセキュリティ業務すら兼業）SOCはSOC、CSIRTはSCIRTとちゃんと役割がに分けられていて、必要に応じてアウトソーシングされることが分かりました。むしろ中小企業こそ、全部自分たちでやろうとするのではなく、パブリックSOC/共用SOC（セキュリティ企業が複数の企業をまとめて監視してくれる）を利用するべきと知りました（KADOKAWAのような大きな会社がプライベートクラウドを社内に構築する一方、中小企業がAWSを活用するように）結局一番お金がかかるのは人件費なので。SOCで使われるツール、SIEMやSOARはとても高機能で。現代はAIを活用してインシデント初動対応もやってくれるらしいです。

そしてCSIRT。CSIRTに関連する資料はいろいろなサイトに掲載されていますが、この本は日本CSIRT協議会に加盟している組織のエンジニアが記載した本だけあり、まずはおさえるべきポイント、勘所を列挙しています。CSIRTは各事業部の情報連携の役割が主であり、インシデントマネージャやインシデントハンドラーは本来別の組織が担当するべきなのですが、中小企業だとどうしても兼務になってしまいますよね。

一つ印象に残っているのが、CSIRTに求められる人物像について記載されていた点です。こういう血の通った解説はこれまで読んだことがなかったのでありがたいです。

CSIRTコマンダーに必要な能力
- IT、セキュリティ知識
- 情報を正確にやり取りするためのコミュニケーション能力
    - 聞く
	- 理解する
	- 伝える
- 交渉力
- 論理的思考力
- 精神力（現場では攻撃側ではなく防御側を責めることがある）

知識、技術があることのみならず（むしろそれよりも）社内で様々な関連部署（経営層、法務、広報、各事業部、そしてインシデントマネージャ）との折衝が必要になります。上の箇条書きを見る限り、自分が向いているとは思えない…。人間力が求められます。僕にはとてもできない、という気持ちになる…(- -)
気を取り直して。CSIRTコマンダーになるにめに社内で平時からやれる訓練についても記載されていますので参考になります。あとやっぱり、外部の組織（CSIRT）との交流関係を築くことは重要なのですね。インシデントの流行や予兆、問題発生時の対応については横の情報共有が大きな力を発揮するので。

他にもCSIRTコマンダーの戦略を基に、具体的に技術的な対応を考えるインシデントマネージャと実際に手を動かすインシデントコマンダーなど、企業のインシデント対応ではどのような登場人物が存在するのか、分かりやすく図で記している貴重な本です。ただしセキュリティ対応のベストプラクティスは企業ごとに十人十色。現実的にはここまで細分化できないだろう、という感想です。しかし「これに見立てて」と社内でインシデント体制を構築し、経営層に論理的に説明するのには間違いなく役立つ本です。初歩的な内容でありながら、まだ初歩すらできていない自分達を再認識させられました。