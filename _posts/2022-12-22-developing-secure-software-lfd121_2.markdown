---
layout: post
title:  "Linux Foundationの「セキュアソフトウェア開発」を受講しました（２）"
date:   2022-12-22 20:50:27 +0900
categories: online-training
img: lfd121-jp.png # Add image post (optional)
tags: [security] # add tag
description: Linux Foundationの「セキュアソフトウェア開発」を受講しました
---

[Linux Foundation「セキュア ソフトウェア開発」無料オンラインコースを開始](https://www.linuxfoundation.jp/press-release/2022/12/free-openssf-developing-secure-software-training-course-now-available-in-japanese/)
第2部の内容についての所感です。
自分用のメモが含まれているため、理解度テストの結果が含まれています。ネタバレを防ぐため、受講する人は先に受講してからこの記事を読んでほしいです。

# 「第2部：実装」
バリデーションがメインの内容です。
バリデーションと一言に行っても、単に数値やテキストを超え、テキストエンコーディングやデシアライゼーション、外部参照、環境変数の利用など考えることが多いです。csvファイル自体に書かれているのは単純な文字列でも、Excelで開いた場合に「=」が使われていると関数とみなして実行するなど、言われてみると「そういえばそうだ」という話も多く掲載されています。

また、バリデーションや値チェックなど不正な入力値をチェックできても、人間が意図せず作りこんだプログラムのバグまではチェックできません。
CVE-2014-1266、通称「goto fail; goto fail;」脆弱性(https://appllio.com/20140223-4899-apple-ios-bug-ssl-goto-fail)など、ぞっとする話ですが同時にやりかねない話だと思います。

知らないことが多かったです。

> 歴史的には、すべての文字を識別するには16ビットで十分だと考えられていましたが、これは間違いで、1996年に変更されました（現在はどの文字も21ビットで符号化するようになっています）。この間違いの結果、一部のプログラミング言語は、16ビット長しかない「文字」型（Javaのcharなど）を持っています。16ビットのデータ型は、それ自体では21ビットの任意の文字を格納できないため、16ビットの「文字」を持つプログラミング言語やAPIでは、「文字」が実際の文字の半分しかないことがあります。

理解度テストの7.4、**許可リストにするには^...$が必要**って「そうなの？」という感想でした。
`^`が文頭を、`$`が文末を意味するのは知っているのですが、`[a-z]+` で1文字以上の小文字英字を意味しないの？
`^[a-z]+$`でないとダメなのかな？だとすると、正規表現を使う場合`^`が文頭を、`$`が文末の意味をあらわすのは知っていましたが、これは必須なのでしょうか？（章最期のナレッジテストでもそれに従ったら正解になったので、そういうものなのかもしれない）

脆弱な正規表現というものも初めて知りました。下手なマッチングを書いたせいで処理に時間がかかり、結果自分からDoSを自分のシステムにしかけるというものです。正規表現は自分も十分理解しているとは言えないため怖いところです。setuid/setgidが絡むプログラムは極力書きたくないという感想も持ちました。とはいえ触らぬ神に祟りなしの姿勢はエンジニアとして正しいのか・・・。
APIの使用回数制限ややネットワーク帯域の帯域制限など、単純ながら攻撃者に攻撃を躊躇させる（あるいはプログラムの予期せぬバグに対する防波堤になる）対策があることも頭の片隅に入れておきたいです。


デシアライゼーションについてはこちらのページが参考になりました。

[実践！安全ではないデシリアライゼーションの攻撃手法](https://yamory.io/blog/about-insecure-deserialization/)


yamoryさんはXXE（XML External Entity: XML 外部エンティティ参照, XML 外部実体）についても解説してくれています。

[油断ならない脆弱性　XXE への対策](https://yamory.io/blog/what-is-xxe/)


バリデーションの章を〆るナレッジチェック（テスト）はかなり難度が高いです。でも7.2の問題は納得がいかない…日本語だとAとCは同じ意味に聞こえるんですよね。原文（英語）だと違う意味ととらえられるのでしょうか。他にも第2部は解説の日本語が腑に落ちない箇所が散見しました。

> (メモリーセーフでない)CやC++で書かれた大規模なプログラムには、書き換えが困難なものがたくさんありますし、もちろん、人々がそれらの言語を選択する理由もあります。オペレーティングシステムのカーネルはほとんどがCで書かれていますが、これはパフォーマンスが重要であり、Cがこの作業のために特別に設計されたからです。同様に、メモリー安全性を無効にできる言語にも、そのメカニズムが存在する理由があるのです。

安易にCやC++をディスってはいけません。しかしCやC++においてメモリ解放が重要なのは承知ですが、解放された後のメモリを再利用することはリスクがあると学びました。

[MEM30-C. 解放済みメモリにアクセスしない](https://www.jpcert.or.jp/sc-rules/c-mem30-c.html)
[メモリの解放](https://www.comp.sd.tmu.ac.jp/spacelab/c_lec2/node118.html)

しかしメモリ容量には限度があります。メモリを使いきってしまった、ということにはならないのでしょうか？（頓珍漢な疑問？）

[CやC++における未定義の動作](https://programming-place.net/ppp/contents/glossary/ma/undefined_behavior.html)

[HTTPヘッダーがセキュア化をチェックできるサイト](https://securityheaders.com/)

hrefのリダイレクトなんて初めて知りました。以下のように書くとリダイレクトされます。
`<a h‌ref="ht‌‌tps://bank.example.com/redirect?url=ht‌‌tps://attacker.example.net">Click here to log in</a>`
404に飛ばすために使われたりするそうですが、明らかに脆弱性を仕込める仕様ですよね。リダイレクトを使ったセキュリティリスクは「オープンリダイレクト」と呼ばれます。言うまでもなくオープンリダイレクトの脅威からWebサイトを守る最善の方法は、リダイレクトを完全に回避することです。これは使わなくてよい仕様と思います。

> HTMLコンストラクト`<a href=... target=...>`は、クリックすると新しい「ターゲット」を作成するハイパーリンクを作成します。 targetのデフォルト値は_selfです。targetを設定する場合、一般的なものはtarget="_blank"で、新しいタブにターゲットを作成します多くの人が気づいていないのは、targetの値をデフォルトの_self以外にすると、場合によっては脆弱性が生じる可能性があるということです

「どういうこと？」と思ったあなた、カリキュラムを受講しましょう(笑)
ネタバレになりますが基本的に自分がリンクを貼って、貼った先のページが安全であれば問題ありません（貼った先のページが改ざんされたらその限りではないかもしれませんが…）

自分用メモ
- セキュアな入力検証チェックは「なにがNGか」ではなく「なにのみがOKか」で設定を行う
- 電子メールだけを用いたパスワードのリセットは、攻撃者によるものの可能性があるため、強力な認証メカニズムではない。
- ほとんどのUnix系システムにおいて、ファイル名は\0（終端記号）やスラッシュを含まない任意のバイト列とすることができる。Unixのファイル名は文字列ではなく、単なるバイト列なので、ファイル名は必ずしも正規の文字列である必要はない。スペース（またはスペースだけ）、制御文字（改行、タブ、エスケープなどを含む）、UTF-8の適正でないバイト、または、先頭の「-」（コマンドオプションの目印）を含むファイル名などの多くの問題のあるファイル名を作成することができる

NGなプリペアードステートメント
```
String QueryString = "select * from authors where lastname = '" + search_lastname + "';";
PreparedStatement pstmt = connection.prepareStatement(QueryString);
ResultSet results = pstmt.execute( ); // Probably insecure, don’t do this!
```

OKなプリペアードステートメント
```
String QueryString = "select * from authors where lastname = ?";
PreparedStatement pstmt = connection.prepareStatement(QueryString);
pstmt.setString(1, search_lastname);
ResultSet results = pstmt.execute( );
```

>「?」を値のプレースホルダーとして正しく使用する代わりに（その後適切にエスケープされます）、このコードはデータをクエリーに直接連結しています。このデータが適切にエスケープされていない限り（そして、ほぼ間違いなくされていません）、このコードは、このデータが攻撃者によって制御される場合、すぐに深刻な脆弱性につながる可能性があります。

→JavaにおけるprepareStatementの使い方を覚える

- 送信される出力の文字エンコーディングを明示します。受信側のプログラムに文字コードを推測させないようにしましょう。受信側のプログラム（通常はWebブラウザー）が推測しなければならない場合、攻撃者はあなたのシステムを騙して間違った推測をさせ、最終的には攻撃につながるようなものを送るかもしれません。HTMLを送信する場合、通常は受信者にそれがUTF-8であることを伝えるべきです。これを行う最良の方法は、HTTPのcharsetオプションで、多くの場合、単純な設定オプションで行うことができます。何らかの理由でそれを制御できない場合は、HTMLの`<head>`にその情報を含めます。例えば、`<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`とします。
- 非常に穏やかなハードニング対策は、クッキーにHttpOnly属性を設定することです。そうすれば、悪意のあるスクリプトが実行されたとしても、クッキーの値を見ることはできません。これは権限を制限することになるので、できる限りこの制限を設定すべきですが、これはとても穏やかなハードニング対策であり、他の対策も適用している場合にのみ有効です。
- おそらく最も重要なCSPの機能は、どのスクリプトの実行を許可するかをCSPが制御できることです。デフォルトでは、Webブラウザーは送られてきたすべてのスクリプトを実行します。ここに、多くの攻撃を防ぐ簡単なCSPがあります。このCSPは、リソース（特にスクリプトとスタイル）はソースサイト（'self'）からのみであり、スクリプトとスタイルに対するinlineまたはevalsは（特に許可されていないため）許可されないと述べています。`Content-Security-Policy: default-src 'self';` インラインスクリプトやスタイルを使用しないことは、広く良い習慣とされていますが、それ以上に、セキュリティを劇的に向上させることができます。インライン スクリプトとスタイルを無視すると、HTML Webページを狙うXSS攻撃で、信頼できないスクリプトやスタイルが簡単に使えなくなるからです。
- CookieのHttpOnlyフラグ：クッキーは、JavaScriptプログラムから見えなくなります
- ユーザーがログインに成功するたびに、必ず新しいセッションIDを取得するようにしてください（これは通常、クッキーの中の値として戻されます）。特に、ログインを受け取る側は、決してセッションの値を再利用してはいけません。
- CSRF対策として使われているのは、SameSiteクッキーと呼ばれるものです。歴史的には、表示された主なページが別のサーバーのものであっても、ユーザーがそのサーバーに一致するクッキーを持つときは、すべてのクッキーがそのサーバーに送信されました。例えば、サイトBBのWebページがサイトCCのイメージへの参照を含むかもしれません。WebブラウザーがCCからイメージをダウンロードすると、関連するすべてのクッキーを送信することになります。しかし、これは実際にはあまり意味がありません。多くの場合、相互作用が関係のないサーバによって引き起こされた場合、クッキーは送信されるべきではないのです。そこで最近のブラウザーは、クッキーにオプションでSameSiteの設定をしています。この設定がLaxまたはStrictの場合、異なるサーバーの攻撃者によって引き起こされたリクエストは、（セッションのような）クッキーを送信させることはありません。ですから、セッションクッキーにSameSiteの設定がLaxまたはStrictである限り、一般にCSRF攻撃は機能しません。さらに良いことに、最近のブラウザーはSameSite=Laxをデフォルトにするよう取り組んでいます。自分でSameSiteをLaxかStrictに設定するのが一番ですが、それでも安全なデフォルトは良いことです。