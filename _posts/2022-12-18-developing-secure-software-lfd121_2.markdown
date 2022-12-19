---
layout: post
title:  "Linux Foundationの「セキュアソフトウェア開発」を受講しました（2）"
date:   2022-12-18 20:50:27 +0900
categories: online-training
img: lfd121-jp.png # Add image post (optional)
tags: [security] # add tag
description: Linux Foundationの「セキュアソフトウェア開発」を受講しました
---

[Linux Foundation「セキュア ソフトウェア開発」無料オンラインコースを開始](https://www.linuxfoundation.jp/press-release/2022/12/free-openssf-developing-secure-software-training-course-now-available-in-japanese/)
第2部の内容についての所感です。

# 「第2部：実装」
バリデーション


符号なし型とかUnicodeとか、知識があいまいな部分について再認識ができました。

- 負の数が許されない場合は符号なし型を使用する
- 浮動小数点データを受け取らなければならない場合（なるべくそうしないようにします）、適切な型に格納し、その多くの特殊ケース（NaN、無限大、負の0、アンダーフロー、オーバーフローなど）に注意する

> 歴史的には、すべての文字を識別するには16ビットで十分だと考えられていましたが、これは間違いで、1996年に変更されました（現在はどの文字も21ビットで符号化するようになっています）。この間違いの結果、一部のプログラミング言語は、16ビット長しかない「文字」型（Javaのcharなど）を持っています。16ビットのデータ型は、それ自体では21ビットの任意の文字を格納できないため、16ビットの「文字」を持つプログラミング言語やAPIでは、「文字」が実際の文字の半分しかないことがあります。

