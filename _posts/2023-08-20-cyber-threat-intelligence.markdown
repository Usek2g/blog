---
layout: post
title:  "【ブックレビュー】脅威インテリジェンスの教科書"
date:   2023-08-20 22:20:27 +0900
categories: bookreview
img: cyber-threat-intelligence.jpg
# Add image post (optional)
tags: [security] # add tag
description: サイバー攻撃に対して「インテリジェンス」で立ち向かう
---

この本の前書きに「セキュリティシステムは常勝を義務付けられているのに、攻撃者は一度勝つだけで良い」とあるようにサイバーセキュリティの世界は圧倒的に有利です。防御側の我々は組織内の『あれが危険』『これが足りない』と分かっていても、その工数も予算も捻出することはできません。だからといってそれを言い訳にセキュリティをなおざりにしてはならない・・・そんな状況で注目されているのが「脅威インテリジェンス」です。

- 攻撃する意図がある
- 攻撃できてしまう攻撃対象の状況がある
- 攻撃者自身に攻撃する能力がある

この3つが揃ったときに脅威は現実化します。対してインテリジェンスとは
- 情報収集・加工・分析評価の成果物
- 成果物を作成するプロセス
- それらを行う組織

を指します。

単にデータ（Data）を収集するだけでなく、それを加工して情報（Information）とし、更に分析してインテリジェンス（Interlligence)とします。また脅威インテリジェンスも、対応する期間や組織などにより戦術・運用・戦略と分けられます。現代ではセキュリティは現場の技術者だけが考えればよいのではなく、経営者も検討する必要がある経営課題となっており、戦略が必要となっています。この本はその各分類に分けて、考えることをまとめています。本では様々なセキュリティに関する用語や組織が出てきます。[MITRE ATT&CK（マイターアタック）](https://www.intellilink.co.jp/column/security/2020/060200.aspx) どこかで聞いたことあるな・・・という用語はCISSPで学んだ知識でした。不合格なわけだ（ーー；

伝統的なリスク管理として『コンプライアンス型アプローチ』というセキュリティのAs isをTo beに持っていく方法がありますが、最初に書いたように資産が膨大、人は少ない状況ではすべてを対応するのは不可能です。ましてどんどん新しい脆弱性が生まれ、クラウドサービスなど外部ベンダーが保有するインフラ上で業務する場合、もはや手がつけられない分野も発生し、そこは相手がちゃんとやってくれることを信じるしかありません。
その一方『脅威ベース型アプローチ』は「脅威が何をしたいのか」にフォーカスします。このことで対象を絞り込み、優先度を定めることができます。効率良いセキュリティ対策が可能になります。毎日のようにCVEがアナウンスされていますが、実際に対応しなければならない脆弱性は一部に集中しています、『Criticalだから対応しなくては！』となると現場が疲弊するばかり。とはいっても専門家でも意見が分かれる脆弱性の強弱を判断するのは一般人には至難の業。
僕が思ったのは、この本で紹介されているような『過去数年間の脆弱性TOP10」みたいなレポートが常に発行されれば助かるのですが。年に1回ではどうしてもタイムラグが発生します。そのため近年は機械学習によるデータ分析により、その脆弱性が本当に対応するべきか否か、を示してくれるサービスもあるとのこと。

この本はPart1：理論編、Part2：実践編、Part3：応用編に分かれています。理論編では脅威インテリジェンスを実現するための体系化された様々な手法、フレームワークが紹介されています。

理論編ではセキュリティを実現するための様々なフレームワークや手法、フォーマットが紹介されています。攻撃側有利とされているセキュリティの世界において、防御側もただ手をこまねいているわけではありません。一言に脅威ハンティングと言っても、こんなにいろいろあるのか…。特に学びがあったのは「戦略インテリジェンス」。会社に”サイバーセキュリティ経営ガイドライン”をいつか導入したいと思っている自分なので、ここに書かれていることはとても参考になります。「サイバーセキュリティは経営課題である」（だからセキュリティにお金出して）というからには、技術者もお金のことを知らないといけないです。二つ上の視点でモノを考える必要があります。

実践編ではいざ実際に脅威インテリジェンスを実施する場合に利用する心構えや分析モデル、コミュニティ、テンプレート
が紹介されます。NTTで年収3000万もらうようなピラミッドの頂点の人たち(https://www.nikkei.com/article/DGXZQOUC10BIF0Q3A710C2000000/ )はこれらを活用して活動しているのだろうな、と勝手に妄想してますw

一方でインテリジェンスの失敗は経営に大きな悪影響を及ぼします。情報が少なすぎることは今の時代稀で、逆に情報過多の中取捨選択を誤ったり、嘘情報に騙されたり、バイアスにハマってしまったり、論理的誤謬（ごびゅう：誤りのこと）を犯したり・・・人間は完ぺきではありませんし、第三者による客観的判断や組織内レビューが必要です。大きな会社になるとインテリジェンスの扱いが政治化することがあります。僕もセキュリティにヒトとカネを出してほしいと思っていますが、そのために誇張したり、ウソをついたりすることはけして許されません。

応用編は一般企業がセキュリティ対策で行う領域を超えた話が出てきます。セキュリティニュースをチェックしていると名前を聞いたことがある、攻撃者は誰だ、背景は何か、などのプレスリリースする国際的な機関やセキュリティ企業が用いる手法が紹介されます。おとり捜査やセキュリティ侵害に対する反撃など高度なスキルが必要になりますが、そもそもそれらは法律では認められていないため、一般企業は手を出せない分野です。なのでこの章で紹介されている方法は、知識として知っているに留めるが無難でしょう。
中で紹介されているロシアのなりすましハッカーの「Guccifer2.0」を検索したらスプートニク(https://ja.wikipedia.org/wiki/スプートニク_(通信社) )の日本語サイトが上位に出てきて、背筋が寒くなりましたね。サイバー戦争は本の中の話ではなく現実で起こっていることを再認識。これは分かりやすいですが、巨大組織同士のサイバー空間での攻防は本性でも紹介されているような高度な技術の応酬なのでしょう。
本章で紹介されている「情報の無秩序化（Information Disorder）」はtwitter上でも起きているなぁと感じます。Disinformation Kill Chainモデルがそのまま当てはまっています。解説している良い日本語サイトが見つからないため紹介できない・・・。防御側の施策も公開されていますが、攻撃側のほうが圧倒的に低コストなのが問題です。偽情報に騙されないための世界各国が作成したチェックリストも載っていますが、ツイート見た、チェックリスト印刷、レ点チェック！なんて日常を送っている人はなかなかいないでしょう、指先一つで拡散できちゃいますし。

書いてあることは自分が調査しているセキュリティ体制のもとと被っていますが、素人が様々なWebサイトからフレーズをピックしてまとめたものと、プロが書籍にまとめたものとではわかりやすさが段違いです。この本一冊あればよいと思います😂
しかし一人で受け止めるにはあまりにボリュームが有り、セキュリティを兼業で行っている１サラリーマンではとても咀嚼しきれないでしょう。チームを組むことの必要性を感じます。