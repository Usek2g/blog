---
layout: post
title:  "2025年1,2月の気になるインターネット記事をピックアップ"
date:   2025-03-08 10:15:27 +0900
categories: diary
img: interesting-internet-articles_202502.jpeg # Add image post (optional)
tags: [article] # add tag
description: 2025年1,2月の気になった記事を読んでみる
---

１月は行ってしまう、2月は逃げてしまう、そして3月は去ってしまう、とは昔からよく言っているものですが、本当に早いですね、ブログ記事も前のめりで更新していきます。
世界が激動していて、ニュースを見るたびにうんざりなのですが、それでもLife goes onです。


[警察庁、中国の関与が疑われる日本国内へのサイバー攻撃に注意喚起。侵入手口など解説、CLI版VSCodeが悪用される例も](https://www.publickey1.jp/blog/25/clivscode.html)
中国の関与が疑われる組織的なサイバー攻撃が日本に対して行われているという警視庁のアナウンス。その攻撃キャンペーンは3つに分類されるということです。特に気になるトピックが”VS Codeを悪用した手口”であり、PDFが警視庁より公開されているので展開します。

[VS Codeを悪用した手口及び痕跡・検知策](https://www.npa.go.jp/bureau/cyber/pdf/20250108_vscode.pdf)

Microsoft Dev Tunnelsは、開発者がローカルで実行しているWebサービスをインターネット経由で安全に共有できるようにするサービス。開発トンネル機能は本来、ソフトウェア開発者等が遠隔地からコンピュータに接続し、リモートでソフトウェアの開発を行ったり、コマンドでコンピュータを操作するために使用されます。

ローカルで開発する際、ローカルで開発環境を作ることに手間取ることは良くあることです。標的メール攻撃によりVSCodeのCLI版を標的PCにインストールしてVSCode Serverを背後で起動させ、Dev Tunnels機能で遠隔からPCを制御。やり方としてはシンプルですが、国家レベルでやっているという警告です。

[ランサムウェア対策の基礎知識 - 感染経路、対策、発覚後の対応](https://news.mynavi.jp/techplus/article/security_ransomware02-pPbsjdDk/)
徳丸先生のランサムウェアに対する解説記事。特別新しいことは書かれてはいないのですが、眼と耳の痛い記述がありますので自戒のためにも残しておきます。

>バックアップは「3-2-1ルール」にのっとった実施が推奨される。これは、3つのバックアップをとり、2つの異なるメディア（手法）で保存し、1つは別の場所に保管するという考え方だ。徳丸氏は、「別の場所」に関して、ネットワークから隔離されたオフラインバックアップで保存をする、変更・削除ができないイミュータブルなバックアップ方式を使うといった手法を示した。

>最後に、忘れがちなのが、訓練である。ランサムウェア攻撃や大規模災害を想定した復旧訓練を行うことを、同氏は強く薦めた。実際に訓練をしてみると、設定の問題でバックアップが足りていなかったり、とれていると思っていたデータがとれていなかったりという問題も洗い出せる。バックアップするだけでなく、データをきちんと戻せるところまでを確認することが大事なのだ。

この二つを世の中の会社がどこまで実施しているのかは知りたいです。クラウドファーストな現代において、Google WorkSpaceやMicrosoft Offie365のデータのバックアップを外部に保存している会社はどこまであるのでしょう。「天下のGoogleやMicrosoft自体がちゃんと二重三重にバックアップをしているのだろう」という神話に縋り付きたくなりますが、**万万が一クラウドベンダーがデータを吹っ飛ばしても、彼らは責任を取ってくれません。**（規約にも書いてあります）また、「データのバックアップを取っているが、実際に復元できたのは全体の3割の会社」という調査結果もあります。復元を訓練で行うのは気が乗らないのは分かるのですが、絶対にやらないといけないタスク。自分もやらないと・・・。

[英国主導のセキュリティ連合「ICCSW」に日本も加盟、サイバーセキュリティ人材育成を目的に](https://internet.watch.impress.co.jp/docs/news/1660070.html)

> 内閣サイバーセキュリティセンター（NISC）は1月31日、英国科学・イノベーション・技術省（DSIT）が策定した文書「サイバーセキュリティ人材に関する国際的な連合」（ICCSW：International Coalition on Cyber Security Workforces）に日本も参画したことを発表した

セキュリティリスクに対して世界全体で対応する必要がある昨今、ICCSWには英国、日本のほか、カナダ、ドバイ、ガーナ、シンガポールが参加するとのことです。CISSPも国際的な資格ですが、このような組織に加わることで統一された用語、方針を基に活動することができるようになり、セキュリティ対応も捗ることが想定できます。


[「AIで言語の壁なくなり、日本へのサイバー攻撃容易に」　米セキュリティー大手の担当者](https://www.sankei.com/article/20250222-H76J32DLRRLPRMM53HGVO3NBLM/)
インターネットで話題になった記事です。フィッシングメール詐欺、スピアフィッシングなど、言葉巧みに騙そうとしてくる攻撃は、かつて日本は"日本語"という世界シェアで言うとマイナーな言語が使われていたためターゲットとして狙われにくく、また送られてきたとしても日本語としてたどたどしく、不審なメールと見抜くのは比較的容易でした。しかしAIの進化と普及により、僕たち日本人ですらAIを使って日本語文章を矯正してもらっているのですから、攻撃者だって使います。今や日本語として違和感のない攻撃メールが職場メールや個人メールに送り届けられてきます。従業員に「気を付けて」と啓発するにも限度があり、DMARCなど技術的な対策が必要でしょうね。


[イギリス政府がAppleに「全ユーザーのデータを取得できるバックドア」を設けるように求めていたことが報じられる](https://gigazine.net/news/20250210-uk-demands-apple-break-encryption-backdoor/)
セキュリティラジオ[セキュリティのアレ](https://www.tsujileaks.com/)で視聴者からの反響も多かったニュース自分もそれで知ったのですが）

Appleすら復号できない暗号化。セキュリティ・プライバシーの重要性が高まる時代なので善良な市民にとってはありがたい機能なのですが、犯罪者もそれを使います。当局としては歯がゆい、なのでバックドアを作ってデータを見れるようにしろ、とAppleに指示したとのこと。

この話には続きがあり

[Appleが「高度なデータ保護」機能をイギリスで提供終了へ](https://gigazine.net/news/20250222-apple-pulls-icloud-advanced-protection-feature-in-uk/)

言うまでもなく、このような要求に従うと、あらゆる国の捜査機関が「じゃあ俺も俺も」と言ってくることは目に見えている話。特にプライバシーを重視する企業であることをウリ・価値としているAppleとしては受け入れられる話では無かったでしょう。

[Appleがイギリスの「バックドア作成命令」について裁判所へ異議申し立てアップルストア](https://gigazine.net/news/20250305-apple-legal-challenge-to-uk-back-door/)

> イギリスでは2016年に捜査権限法が施行され、法執行機関が証拠を収集する際に企業へ協力を強制することが認められました。

アメリカでは愛国者法（パトリオット法）という、政府やFBIは、アメリカ国内に存在するコンピュータやサーバ内のデータを、裁判所の命令なしで調査することができるという法律もあります。日本では似たような法律として、通信傍受法（犯罪捜査のための通信傍受に関する法律）が裁判所の令状を必要としますが、通信傍受を可能とする法律があります。「自由とセキュリティ」についての課題は尽きません。