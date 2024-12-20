---
layout: post
title:  "CISSPに合格しました！"
date:   2024-11-16 10:30:27 +0900
categories: column
img: CISSP-logo-2lines.png # Add image post (optional)
tags: [CISSP] # add tag
description: CISSP受験合格までに何を思い、何をしてきたかを記します
---

もともとこのブログを書き始めたきっかけは、2022年にCISSPの試験を受けたものの不合格だった時の自分の感想を書き留めておきたかったからです。

[CISSP受験の感想](https://usek2g.github.io/blog/impression-of-the-cissp-exam/)

上記の記事内で、当時自分はこう書きました。

>ネット上の合格記には記載されていないこの点をまだ受験したことのない人に知ってほしいです。
>**CISSPの試験では上記の試験対策本やUdemyで身につけられる知識問題はほとんど出ません。**
>企業でセキュリティを担当するものとして、もっと実戦的なことが問われます。「問われる」質問の大半は**最善な対応はどれか**というもの。答えが１つに明快に求められる知識問題ではなく、背景や事情が異なるシチュエーションから、セキュリティの標準に準じたうえで最適な選択肢を選ぶ必要があります。４択から２択くらいには絞れるのですが、ここからは「どっちでも問題ないのでは・・・？」となります。
>CISSPはセキュリティの十分な知識と経験があることを保証するための資格、そのため合格後も企業で最低５年間のセキュリティ業務に従事した実績がないと正式に名乗れません、なのである意味ではこの試験内容は理にかなっていると言えます。試験対策では合格できない、実戦経験を積むべしというのが私の伝えたいこととなります。

＜略＞

>今回試験に不合格となったことは財布的にも時間的にもとても悲しいのですが、CISSPに合格するにはセキュリティの業務を一つずつ着実に実践でこなしていくのが王道だと認識できたことが収穫です。そのため、このブログを立ち上げてセキュリティに対する学びや情報をアウトプットしようと思い立ちました。
毎日のように我々のセキュリティを脅かす事例がアナウンスされ、またセキュリティを守るためのサービスもリリースされます。サイバーセキュリティがこれほど重視された時代はありませんし、今後軽視されることもないでしょう。ブログのタイトル通り、セキュリティの道に終わりはありません。セキュリティエンジニアと胸をはって名乗れるよう、今後もセキュリティの道を歩み続けたいです。

---

上記の約束のとおり、2023年以降もブログ記事を公開して、セキュリティのアウトプットを継続しました。

仕事でもセキュリティ担当として、社内のセキュリティの強化に加え、新規サービス開発プロジェクトでは、これでもかというセキュリティの要望に逃げずに（それは言い過ぎかもですがｗ）立ち向かいました。
 **「ギガンデスとキラーマシーンと戦っているみたいだ」** と何度も仕事中に言ったセキュリティ要求の高さでしたが、その分経験値は溜まりました。

プロジェクトがひと段落した2024年春、改めてCISSPの試験勉強を始めました。
きっかけは今年春、CISSPの試験内容が改定されたことから、「もう一度挑戦しよう」と心に火が付きました。

[CISSP CAT（Computerized Adaptive Testing）試験について](https://www.isc2.org/certifications/cissp/cissp-cat/cissp-cat-japanese)

これまで6時間250問だった問題数が、3時間で100-150問ということになりました。なんで問題数に開きがあるのか、というと、

>100問の試験に合格した受験者は、全ドメインを通じて十分な概念を習得しており、習熟度を証明することができます。100問の試験で合格しなかった受験者は、最低合格点を達成するために必要な習熟度を、十分なドメインを通して示していないことになります。100問を超えた受験者は、いくつかのドメインで熟練している可能性がありますが、追加項目の提示により、最低合格点を達成できるよう、他のドメインでの熟練度を証明し続ける機会を与えられます。

どうやら、100問で「文句なしに合格or文句なしに不合格」が判定され、微妙なラインの人は最大50問のチャンスが与えられる、という構造のようです。

とはいえ、試験勉強のやり方は2年前と大きくは変えませんでした。
2年前の勉強ノートを残していたので（自分は過去取得した資格試験の勉強ノートはほぼ残しています）、再学習して記憶を取り戻し、CISSPを受験する人にとっては有名なサイト[晴耕雨読CISSP 勉強ノート](https://tex2e.github.io/blog/security/cissp-notes)を写経。

これに加えて、単なる試験知識の詰込みでは合格できないことを2年前痛感していたことから、[安全なWebアプリケーションの作り方（徳丸本）](https://usek2g.github.io/blog/how-to-make-safety-web-application/)を読み、自分の理解の薄かった[OAuthについても本で学びました](https://usek2g.github.io/blog/oauth-thorough-introduction/)。
試験合格の最短経路ではなかったかもしれませんが、遠回りこそが結果として最短の道になる、という自分の考えを信じました。

ある程度知識を身に着けたので次は模擬試験。2年前も利用した [CISSP 公式問題集](https://www.amazon.co.jp/CISSP%E5%85%AC%E5%BC%8F%E5%95%8F%E9%A1%8C%E9%9B%86-%E3%83%9E%E3%82%A4%E3%82%AF%E3%83%BB%E3%83%81%E3%83%A3%E3%83%83%E3%83%97%E3%83%AB-ebook/dp/B08C7J6SR5/ref=sr_1_1?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&crid=1IH2WI7ST27O8&keywords=cissp&qid=1669991889&qu=eyJxc2MiOiI0LjEyIiwicXNhIjoiMy41NSIsInFzcCI6IjMuMDMifQ%3D%3D&sprefix=cis%2Caps%2C472&sr=8-1)と、今年発売された[CISSP Official Practice Tests 4th Edition](https://www.amazon.com/Certified-Information-Security-Professional-Official/dp/1394255071)を利用しました。後者はは英語ですが、kindleで買えば翻訳機能があるので問題なく利用できます。

ちなみにUdemyは使いませんでした。2年前利用した講座を最後の仕上げに使おうと思ったのですが、

- 出題内容の正解が公式問題集の回答と異なる
- （これは過去に受験したからこそ分かるのですが）出題される問題の方向性が実際の問題と異なる

上記理由で使いませんでした。kindle unlimitedで配信されているCISSP本の中にも、

- 全部で1000問、などと謳いながら実際には同じ問題が同一模擬試験内で何度も出題される
- 回答が事実と異なる。解説も間違えている

という、厳しい言葉を使うなら"やるだけ時間が無駄"な本も配信されているので、皆さんも気を付けてください。

そういえば、2年前と大きく違うことがありました。**生成AIを利用した学習です**。
調べ物もこれまでのように検索エンジンで調べて、いろんなサイトをめぐって…とやるのではなく、生成AIに聞けばすぐ理路整然と答えてくれます。
**「〇〇について、暗記しやすい覚え方はありますか？」** と聞くとそれも教えてくれるという。パフォーマンスがぜんぜん違います。凄い時代だ…今の学校・塾の学習現場でもこのような事例が起きているのでしょうね。


模擬問題はほぼ70%以上は取れていたのですが、2年前にブログで書いた「実際は模擬問題のような問題は1割程度しか出てこない」というトラウマはちゃんと残っていました。
そして当日。受けている最中に **「やっぱり模擬問題の問題は出ないじゃないか…」**と思いました（2年ぶり2回目）
CISSPの試験は本当に難しく、「そんなことまで聞かれるのか」「どちらでも正しいのでは？」と思わせる問題が多いです。回答するも自信のない問題が多く、心折れそうになりましたが、それでもこの2年の経験と学習を信じて回答し続けました。
今回自分の試験は150問とMAXまで出題され、最後は時間が足らず、ぱっと選んで次の問題、ととにかく最後まで回答するよう頑張りました。
分からないこと、過去勉強していたのに記憶から抜け落ちてしまってたことも多かったので、正直手ごたえはありませんでした。
しかしその場での合否発表では**暫定**合格と書かれた紙をいただいたのでびっくりでした、もちろんうれしいですがあくまで暫定なので、ぬか喜びしないようにしていましたｗ

そして暫定合格の用紙をもらってから数分後（実際に確認したのは夜でしたが）

<img src="{{site.baseurl}}/assets/img/cissp-passed.png" alt="CISSP合格メール">

CISSP 試験合格メールが届きました！


感想として…まず、ギリギリ合格いただいたと思っています。知らないことが多すぎる、ということを痛感させられた試験でした。研鑽が必要です。
研鑽と言えば、CISSPは合格したらそれで終わり、ではなく維持するためにはポイントを貯める必要があります。これについては調べた結果を後日改めて記事にしたいと思います。

このブログのタイトルにもなっていますが、セキュリティの道に終わりはありません。今後もインプット＆アウトプットを続け、CISSPを名乗るにふさわしい実力、経験を身に着けていきたいと思います。