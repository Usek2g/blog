---
layout: post
title:  "【ブックレビュー】パスキーのすべて"
date:   2025-06-28 10:20:27 +0900
categories: bookreview
img: all-of-passkey.jpg # Add image post (optional)
tags: [security,passkey] # add tag
description: 僕の一推しの技術「パスキー」の本格的な書籍が遂に登場
---

皆さん、パスキーを使っていますか？
このブログでもたびたび話題に上げているパスキー。僕も[GitHubの認証](https://docs.github.com/ja/authentication/authenticating-with-a-passkey/signing-in-with-a-passkey)や[Amazonのログイン](https://www.amazon.co.jp/gp/help/customer/display.html?nodeId=TPphmhSWBgcI9Ak87p)にパスキーを利用しています。
パスキーは一般的な人たち向けのサービスにも普及しています。[例えばニンテンドーアカウントもパスキーに対応](https://support.nintendo.com/jp/nintendo_account/passkey/index.html)しています。[ドコモのdアカウントもログイン後の重要な契約ではパスキーが必須](https://id.smt.docomo.ne.jp/src/utility/passkeys.html)となり、ドコモのセキュリティに対する高い意識を感じます。

パスキーの普及は近年のセキュリティに対するニーズであることはもちろん、そもそもパスキーは"楽ちん"であり、楽ならば普及しない理由はありません。僕はパスキーの存在を知った当時から「必ずこの技術は普及する」と確信し、このブログでも幾度となく（初出は2023年1月）から紹介しているパスキーですが、今年ついにパスキーについて深く語る本が出版されましたので紹介しようと思います。

古代より「合言葉」として使われていたパスワードですが、弱点も多く存在しました。なによりパスワードを利用する「人」が"123456"とか"password"等の弱いパスワードを使っていたり、同じパスワードを使いまわしたり、騙されてパスワードを攻撃者に漏らしてしまったりと、自らセキュリティ事故を起こしてしまうのです。時折「パスワードの定期的な変更はやらなくてよい」というセキュリティ対策の変遷が話題になりますが、これは **「パスワードの定期的な変更は（結局覚えやすいパスワードを使い回ししてしまうためセキュリティが却って弱くなり）やらなくてよい」** という意味で、つまりは人間が惰弱なゆえの対策の変遷なのです。
今や「ID＋パスワードでは安全でもなんでもない」といわれる時代。多要素認証は当たり前となりました。しかし多要素認証にも（ID＋パスワードと比べれば圧倒的に強固ですが）欠点はあります。
それならば「パスワードを辞めてしまおう！」という**パスワードレス**という考えが生まれました。しかしこのパスワードレスも、プライバシーや可用性という点で問題がありました。
これらの問題を一挙解決する優れた技術がパスキーです。しかしパスキーの技術について曖昧な場所も多く、今一度学び直したい、と思った矢先のこの本の出版、渡りに船です。

パスキーの技術の根幹は、セキュリティの分野では多用されている公開鍵暗号方式を利用しています。Webサイトへアクセスするための秘密鍵を認証器に格納し、公開鍵をWebサイト側のサーバに保管します。余談ですが公開鍵暗号方式を考えた人はノーベル賞ものですよね。実際「ディフィー・ヘルマン鍵交換」で名前を残したお二人はコンピュータ界のノーベル賞といわれるチューリング賞を受賞されています。

[コンピューティング分野のノーベル賞ことチューリング賞、公開鍵暗号の研究者に与えられる](https://www.gizmodo.jp/2016/03/Turing_Award_for_public_key_encryption.html)


パスキーは、秘密鍵とそれに対応するWebサイトのドメイン名などを含むメタデータがセットになったもので、スマートフォンのような個人だけが持つデバイスで作成されるものです。鍵を作るデバイス（物理的なデバイスとは限らない）を認証器と呼びます。この認証器は「本人が所有している」ことに加え、スクリーンのロックを解除できるということはそれ自体も認証行為になることから2段階認証を実現します。つまりフィッシング詐欺（遠隔からの不正ログイン）にとても強いことが特徴です。

パスキー自体も有用な技術ですが、これだけですと欠点があります。スマフォが壊れてしまったら、中にある秘密鍵が使えなくなり、すべての認証が通らなくなってしまいます。この弱点を克服するために、Googleパスワードマネージャなどのパスキープロバイダは、複数のウェブサイトやサービスで利用するパスキーを一元的に管理・保存する役割を担います。ただし、これはデバイスに直接保管されている秘密鍵のバックアップや同期を目的としたものであり、認証の主要な処理はデバイス上で行われます。そのうえでWebブラウザやネイティブアプリ上でAPIを利用して認証を実現します。パスキーの普及にはこのパスキープロバイダーの存在が欠かせません。
自分はこの本を読むまでパスキー＝生体認証、だと思っていましたが、生体認証はパスキーを実現する技術の中の1つに過ぎませんでした。大きく分けて「デバイス認証」と「ローカルユーザ認証」があり、

- デバイス認証=所有者認証＋知識認証（パスワードやPIN）、もしくは所有者認証＋生体認証（指紋・顔認証）の2パターン
- ローカルユーザ認証＝スクリーンロックを解除できるという事実（それは実際はデバイス認証と同じように所有者＋知識だったり、所有者＋生体認証だったりする）

と融通が効くのが特徴です。

しかし人はいくらセキュリティが強固でも面倒では使いません。「楽」でないと利用しません。ログインまでの時間が短縮され、セキュリティも強化され、追加コストもかからない。加えて**パスキープロバイダの存在によりデバイス認証の欠点、つまり機種変更した時に認証を設定していたサービスを全部登録し直す、のような面倒くささをデバイス間で同期で解決するようになります**。Googleアカウントのようなインターネット上のログインユーザとして大きなシェアを持っているサービスがパスキープロバイダーとして利用できるのであれば導入の抵抗も少ない。いいとこづくめではありませんか。

とはいえパスキーも銀の弾丸ではなく、スマフォのロックを解除できるPINをソーシャルエンジニアリングで盗み見られたのちにスマフォを強奪されると（生体認証を組み合わせていない場合）ログインされ放題になってしまいます。あくまでパスキーはフィッシング詐欺のリモート攻撃や、パスワード漏洩に対して強い、という基本を留意しておく必要があります。また、**家電量販店の店頭のデモ機など、複数の人間が利用する機器ではパスキーを利用しない、あるいはお店側で無効化しないと、誰かがログインした後別の人がそのパスキーを使ってログインできる可能性がある**点は盲点でした。

この本はパスキーの技術的な説明にとどまらず、パスキーをユーザーに登録・利用してもらうにはどのようなUIを提供するのが良いユーザ体験なのかを先行実装しているYahooや任天堂などの画面を使って例示しています。新たに実装したい場合は真似させてもらうと良いでしょう。
そして具体的な実装方法についても解説。ブラウザでの実装からスマフォでのネイティブアプリでの実装、検証方法。パスキーが使えるようになりました、では終わらず、パスキーの管理や削除、ユーザがパスキーにアクセスできなくなった場合の対処法込みでサービスを作る必要性に言及しているのがさすがです。言われてみれば確かに、**Googleアカウントでログインできなくなったユーザは、Googleパスワードマネージャも使えなくなるので、「パスキー」と「Google連携」でのみログインできるサイトを作った場合は、ユーザはアクセスできなくなってしまいます。**引き続きこれまでのようなID/PWによるログインもできるようにしておかないといけません（メールによる多要素認証の導入もまだまだ必要でしょう）

この本はパスキーを自分の企業に導入しようとするセキュリティ担当者はもちろん、パスキーを自社サービスに実装したいというエンジニアにとってもありがたい本となっています。

