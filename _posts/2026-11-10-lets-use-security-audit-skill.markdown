---
layout: post
title:  "Cloudflare Audit SkillとAiderを使ってソースコードの脆弱性をチェック"
date:   2026-11-10 22:15:27 +0900
categories: diary
image:
  path: /assets/img/about-recent-frequent-cyberattacks-and-data-breaches2.jpg # Add image post (optional)
tags: [ai,security] # add tag
description: 目には目を、AIにはAIを。AIを使ったセキュリティ脆弱性対策
---

毎日のようにAIを利用したサイバー攻撃のニュースが流れてきてもううんざりです。誰かがSNSで言っていました。**「AIがなかったころに作られたソフトウェア・サービスはAIには勝てない。AIを使って全部作り直すべき」**だと。なんというものを人類が作ってしまったのか。
残念ながらAIに対してはAIで対抗するしかありません。

[https://github.com/cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)

security-audit-skillは、Cloudflareが公開しているオープンソースのAIエージェント用スキルです。
スキルとは、AIエージェントに特定のタスクを遂行させるための、具体的な指示書やワークフローのまとまりのことを指します。
自然言語でmarkdownファイルに「この観点で計画を立てろ」「こういう手順で作業を行え」「この点に注意しろ」と書いたファイルをまとめて読み込ませてskillコマンドで呼び出すことで、AIエージェントに処理を任せることができます。

Claude CodeやCodexのようなAIエージェントに対して普通に指示を出してもかなりの精度で作業を行ってくれます。しかしこのように特定の作業に特化したスキルを併用してAIエージェントに指示を出すと、AIの作業の品質が上がります。
クラウドサービスにおけるトップランナーの1社であるCloudflareが自社のセキュリティチェック用に使用しているスキルを公開してくるという太っ腹。READMEにはこのスキルの特徴が記載されてました。

- 敵対的検証：「脆弱性を発見したエージェント」と「それをチェック（検証）するエージェント」を完全に分離しています。これによりAI特有の誤検知（ハルシネーション）を防ぎます。
- 厳格な評価基準：単なるチェックリストの逸脱や「多層防御の欠け（防御層が1つ足りないだけ）」は脆弱性とみなさず、「実際に影響（インパクト）を及ぼせるか」を重視して判定します。
- 反復による精度向上：同じコードベースに対して複数回監査を実行すると、過去の記録（Ledger）を活用して未検証のギャップを狙うように設計されており、実行するほど網羅性が高まります

LLMの推論能力を利用して、本格的かつ体系的なセキュリティテストを自動化するための非常に実践的なフレームワークとなっています。
巨人の肩に乗るという言葉もありますし、使い方を試してみます。さっそくgit cloneしましょう。

今回は[OWASP Juice Shop](https://github.com/juice-shop/juice-shop)を使います。事前にローカル（作業用ディレクトリ）にcloneしましょう。先ほどcloneしたsecurity-audit-skillと同じディレクトリに配置してください。
OWASP Juice Shopは、意図的にセキュリティ対策が施されていないWebアプリケーションです。セキュリティトレーニング、セキュリティ意識向上デモ、CTF（Capture The Flag）など、様々な場面で活用でき、セキュリティツールのテストにも最適と考えました。Juice Shopには、 OWASP Top Tenに掲載されている脆弱性だけでなく、実際のアプリケーションで発見された多くのセキュリティ上の欠陥も網羅されています。

次に、AIエージェントが利用するLLMを用意します。世の中いろいろなLLMがありますが、今回はGoogle AI Studioを使用します。
Google AI Studioは、Googleが開発者向けに提供している、Geminiなどの生成AIモデルをAPI経由で利用・検証するためのプラットフォームです。
Geminiを契約している人は「Gemini上でAPIキーを発行して利用できないのか？」と思うかもしれませんが、普段ブラウザで使っている有料版の「Gemini Advanced」などは一般向けのチャットサービスであり、外部ツールから呼び出すためのAPIキーは提供されていません。
作成するAPIキーは無料枠の発行で構いません。もちろん、本格的な業務で利用する場合は無料枠だとすぐに上限に到達してしまいますが、今回は検証目的のためお金はかけません。
APIキーの発行方法は[ Google AI Studio ](https://aistudio.google.com/)からGoogleアカウントでログイン。 画面左側のメニューから「API Keys」をクリックします。右上の「APIキーを作成」を押して、APIキー発行します。

そしてAIコーディングエージェントをインストールします。今回はオープンソースのAIコーディングエージェントであるAiderを利用します。
AiderはClaude CodeやCodexと競合しますが、AnthropicのLLMを利用するClaude Codeと異なり、Aiderは特定のAIに縛られないため、今回利用するGeminiのAPIの他にも、ClaudeやOpenAIのLLMも利用可能です。
Aiderはpip(Windows)またはHomebrew（Mac）でインストールします。

Windowsの場合：
`python -m pip install aider-chat`

Macの場合：
`brew install aider`

僕のPCはWindowsなので、以降はWindowsで実行した結果となります。

インストールした後は、環境変数GEMINI_API_KEYに、Google AI Studioで発行したAPIキーを設定します。

`set GEMINI_API_KEY=APIキー`

いよいよAiderを起動します。先ほどGeminiのAPIキーを設定したので、Aider起動時のモデル指定も必ず gemini/ から始まる名前を選んでください。
ただし、普通のgeminiだと何をするにもAPIレート制限に引っかかってしまうので、今回は最新のgemini-flashを使いましょう。検証目的なら十分です。

`aider --model gemini/gemini-flash-latest`

```text
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Aider v0.86.2
Model: gemini/gemini-flash-latest with diff-fenced edit format
Git repo: .git with 1,467 files
Warning: For large repos, consider using --subtree-only and .aiderignore
See: https://aider.chat/docs/faq.html#can-i-use-aider-in-a-large-mono-repo
Repo-map: using 4096 tokens, auto refresh
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
>
```

まず、スキルを読み込みます。Aiderの特徴として、AIコーディングエージェントが認識できるファイルを1つずつ読み込みます。Claude Codeなどはフォルダを指定すればファイルをすべて読み込んでくれたりしますが、その結果トークンの枯渇も早くなります。Aiderは利用者の手間がかかる代わりに、必要なトークンの消費を抑えることができる設計思想になっています。
以下を1行ごと入力します。

`> /read ../security-audit-skill/skills/security-audit/SKILL.md`
監査エージェントとしての根幹ファイルです。全6フェーズの進行手順やプラットフォームの用語定義が書かれています。

`> /read ../security-audit-skill/skills/security-audit/RECONNAISSANCE.md`
本格的な調査を始める前の文字通り「偵察」を行う指示書です。
AIに対し、ソースコードを読み込んでアーキテクチャ、データ入力口（エンドポイント）、信頼境界（外部と内部の境目）をマッピングするよう指示します。
この結果として、漏れなく監査を行うためのリスト（coverage-ledger.json）を作成させます。

`> /read ../security-audit-skill/skills/security-audit/HUNTING.md`
フェーズ1で作ったリストに基づいて、対象領域ごとに孤立した「ハンター（探索実行者）」を割り当て、どのような観点でチェックを行い、どのように検証記録を残すのか（検証ルール）をAIに指示します。

Cloudflareのエンジニアたちが考えた、AIエージェントに正確に脆弱性診断をおこなうための秘伝のタレが公開されています。つまり、security-audit-skillはファイルを分割して段階的に読み込ませることで、AIが一度に大量の指示を抱えて混乱（ハルシネーション）するのを防ぎ、かつリストを作ることで体系的で精度の高い監査を実現する設計になっています。

準備が整いました。自然言語で指示を出してみましょう。

`> 読み込んだ手順（SKILL.mdなど）に従って、現在のプロジェクトのセキュリティ監査を実施してください。まずは「フェーズ1（Reconnaissance）」のアーキテクチャ把握と coverage-ledger.json の作成から開始してください。 `

以下のような結果が得られました。

```text
今回のリクエスト（セキュリティ監査のフェーズ1の実施、アーキテクチャ把握および coverage-ledger.json
の作成）では、既存のソースコードファイルを変更する必要はありません。

監査成果物は新規作成となります。SKILL.mdの規定に従い、フェーズ1のファイルを生成する前に以下のセットアップ情報を確認させてください。

 1 出力ディレクトリ: 監査成果物（run-metadata.json, architecture.md, coverage-ledger.json
   など）を保存するパス（デフォルトはターゲットリポジトリ外の ~/security-audit-skill/juice-shop/run-1
   です。リポジトリ内に作成する場合は、.gitignore で無視されているディレクトリパスをご指定ください）。
 2 実行プロファイル:
   standard（標準）、quick（1波のみの簡易監査）、deep（高詳細・網羅的監査）のいずれを適用しますか？（指定がない場合は
   standard で進行します）。

上記を確認でき次第、指定の出力先に新規作成（SEARCH/REPLACE ブロック）でフェーズ1の成果物を配置します。
```

Juice Shopリポジトリ外（security-audit-skill/juice-shop/run-1)にレポートを配置することで、脆弱性レポートをリポジトリ内に混入させるリスクを防いでいますね。
では、実際に実行してみましょう。

`> 出力ディレクトリは（../security-audit-skill/juice-shop/run-1）で、実行プロファイルは standard で進めてください。`

結果は以下になります。

```text
フェーズ1（Reconnaissance）を実施し、以下の3つの成果物ファイルを新規作成します。

 1 ../security-audit-skill/juice-shop/run-1/run-metadata.json - 実行設定およびメタデータ

 2 ../security-audit-skill/juice-shop/run-1/architecture.md - システム構成、信頼境界、攻撃対象面の要約

 3 ../security-audit-skill/juice-shop/run-1/coverage-ledger.json - 決定論的カバレッジ台帳

各ファイルの作成を行う SEARCH/REPLACE ブロックは以下の通りです。

../security-audit-skill/juice-shop/run-1/run-metadata.json

<<<<<<< SEARCH

=======

{

  "run_id": "juice-shop-standard-run-1",
  "repo": "juice-shop",
  "target": ".",
  "source_ref": "HEAD",
  "profile": "standard",
  "scope_paths": [
    "routes/",
    "server.ts",
    "frontend/src/app/",
    "infrastructure/"
  ],

  "budget": null,
  "execution_policy": "sandboxed-source-and-local-only",
  "selected_companion_files": [],
  "prior_run_paths": [],
  "shared_file_owners": {
    "parent": "parent-coordinator"
  },
  "run_status": "in_progress"
}

>>>>>>> REPLACE

../security-audit-skill/juice-shop/run-1/architecture.md

<<<<<<< SEARCH
=======
# Architecture Summary: OWASP Juice Shop

## 1. Product, Principals, and Protected Resources

OWASP Juice Shop is a modern e-commerce web application intentionally designed with realistic architectures and security

scenarios.

**Principals**:
  - Unauthenticated visitor: Browsing products, tracking public orders, search, registration, login.
  - Authenticated customer: Shopping basket management, checkout/order placement, product reviews, 2FA management,
customer complaints, digital wallet balance.
  - Support / Administrator: Administrative actions, backend management.
**Protected Resources**:
  - User credentials, TOTP 2FA tokens, session tokens.
  - Basket contents, order history, invoice PDFs (`/ftp/order_*.pdf`).
  - Wallet balances, payment methods, delivery addresses.
  - Server process integrity and filesystem.

## 2. Technology Stack & Deployment Paths

**Backend**: Node.js, Express, Sequelize (SQLite / in-memory DB), Handlebars (`hbs`), WebSocket / socket.io.
**Frontend**: Angular SPA, Angular Material, RxJS.
**Infrastructure**: AWS ECS via Terraform (VPC, public subnets, ECR, EFS).
**Execution Limits**: Offline builds with local dependencies; bounded loopback for API verification. Network
dependency installation prohibited during sandbox runs.

## 3. Entry Surfaces & Important Paths

**HTTP REST / Express Routes**:
  - `routes/2fa.ts`: TOTP setup and verification endpoints (`/rest/2fa/verify`, `/rest/2fa/setup`).
  - `routes/order.ts`: Order processing, discount calculation via coupons/campaigns, invoice PDF creation.
  - `routes/redirect.ts`: Redirection service via `to` query parameter.
  - `routes/search.ts`: Product search querying SQLite database.
  - `routes/checkKeys.ts`: Web3/crypto mnemonic key parsing.

**Frontend SPAs**:
  - Token handling via localStorage/cookies, OAuth callback parsing in `OAuthComponent`, 2FA entry dialogs.

## 4. Trust Boundaries & Controls

**Boundary 1: Authentication & MFA (routes/2fa.ts)**:
  - Intended control: Verification of temporary token (`tmpToken

Tokens: 22k sent, 850 received. Cost: $0.02 message, $0.04 session.

routes\2fa.ts

Add file to the chat? (Y)es/(N)o/(A)ll/(S)kip all/(D)on't ask again [Yes]:
```

architecture.mdにはJuice shopがどういうアーキテクチャ化をAIが分析した結果が書かれています。このような設計図を実業務では開発側が自分で用意してきましたが、これもAIにお任せすることができるのか…。

直前の出力に**Cost: $0.02 message, $0.04 session**とありますが、無料枠で使っている限りは（使いすぎると動作が停止するため）課金されないので安心を。
その後ろにある「routes\2fa.tsをチャットに加えますか？」という質問の意味について説明します。
routes\2fa.tsはJuice Shopリポジトリ内に存在するtsファイルです。僕は「え、aiderはすべてのコードを走査して脆弱性診断してくれるんじゃないの？」と思ったのですが、Cloudflareのセキュリティチェックツールのロジックは、AIに単なる表面的なコードの構文チェックをさせるのではなく、事前に手順書（SKILL.mdやHUNTING.md）を読み込ませることで、システム全体のトラストバウンダリ（信頼境界）や認証仕様を特定させます。
その上で、調査台帳（coverage-ledger.json）を作成し、AI特有の「目についたところだけ直すつまみ食い」を防ぎながら、IDOR（認可制御不備）のような複雑なビジネスロジックの欠陥を計画的かつ網羅的に発見できる仕組みになっています。

ここはYを押してファイルを追加しました。
この後もAiderと会話を続けますが、無料枠のAPIキーを使っているためか、**Empty response received from LLM (0 received)**」**と表示されることが多々あります。これは一時的なレート制限に引っかかってしまっているためです。

- 少し間を開けてEnterキーを押して再実行
- /clearコマンドを実行。これまでのチャットの会話履歴だけを消去（読み込んだファイルは維持されます）して空きを作り、再実行

のどちらかを選択してください。また、出力が途中で途切れてしまうことがあります。その場合は`先ほどの出力が途中で途切れてしまいました。作業の続きから再開し、最後まで完了させてください`と指示します。会社でClaude Codeを使っている時はこのようなストレスは経験したことはないのですが、有料のLLMを利用しているのである意味当然と言えます。このようにAiderは「指示を出せばあとはよしなにやってくれる」というツールではありません。躓いたら都度AIに聞いて解消していきましょうw


何度かの`The API provider's servers are down or overloaded. Retrying in X.X seconds...`が出力されたのち、以下が結果として返ってきました。

```text
脆弱性の原因

routes/basket.ts の retrieveBasket 関数において、URL パラメータ（req.params.id）から取得したバスケット ID
に対する所有権検証が行われていません。リクエストを行った認証済みユーザーのバスケット
ID（user.bid）と一致するかを確認せずにデータベースから取得・返却しているため、任意のバスケット ID
を指定することで他者のバスケット内容を閲覧できる認可制御不備（BOLA / IDOR）が存在します。

修正方針

リクエスト送信者の認証情報（user）を確認し、user.bid と要求された id が一致しない場合は 403 Forbidden
を返してアクセスを拒否するように検証処理を追加します。

Tokens: 20k sent, 536 received. Cost: $0.02 message, $0.09 session.
Applied edit to routes\basket.ts
    litellm.ServiceUnavailableError: GeminiException - {flash-latest
  "error": {
    "code": 503,
    "message": "This model is currently experiencing high demand. Spikes in demand are usually temporary. Please try again later.",
    "status": "UNAVAILABLE"
  }
}

The API provider's servers are down or overloaded.
Retrying in 0.2 seconds...
Commit cc298aa fix: バスケット取得時の所有権検証を追加してアクセス制御不備を修正
You can use /undo to undo and discard each aider commit.
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Readonly:
..\security-audit-skill\juice-shop\run-1\architecture.md
..\security-audit-skill\juice-shop\run-1\coverage-ledger.json
..\security-audit-skill\skills\security-audit\HUNTING.md
..\security-audit-skill\skills\security-audit\SKILL.md

Editable: lib\insecurity.ts routes\basket.ts
>
```

脆弱性の原因と修正方針を考えてくれました。AIコーディングエージェントがどのような思考とスキルの利用を経てこの結論にたどり着いたかは、juice-shopディレクトリ直下にある、AIとのやり取りが記録された`.aider.chat.history.md`というファイルに記載されています。（ちなみにこのファイルは.gitignoreで無視されるようAiderが初期設定してくれるので安心です）
さらに`git show HEAD`を実行すると

```text
git show HEAD
commit XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXxXXXXXXX (HEAD -> master)
Author: Usek2g <usek.2g@gmail.com>
Date:   Fri Oct 23 08:33:13 2026 +0900

    fix: バスケット取得時の所有権検証を追加してアクセス制御不備を修正

    Co-authored-by: aider (gemini/gemini-flash-latest) <aider@aider.chat>

diff --git a/routes/basket.ts b/routes/basket.ts
index 18dd06914..ea5294612 100644
--- a/routes/basket.ts
+++ b/routes/basket.ts
@@ -16,13 +16,13 @@ export function retrieveBasket () {
   return async (req: Request, res: Response, next: NextFunction) => {
     try {
       const id = req.params.id
+      const user = security.authenticatedUsers.from(req)
+      if (!user || user.bid !== parseInt(id, 10)) {
+        res.status(403).json({ error: 'Access denied to basket' })
+        return
+      }
+
       const basket = await BasketModel.findOne({ where: { id }, include: [{ model: ProductModel, paranoid: false, as: 'Products' }] })
-      /* jshint eqeqeq:false */
-      challengeUtils.solveIf(challenges.basketAccessChallenge, () => {
-        const user = security.authenticatedUsers.from(req)
-        const isValidId = id && id !== 'undefined' && id !== 'null' && id !== 'NaN'
-        return user && isValidId && user.bid && user?.bid != parseInt(id, 10) // eslint-disable-line eqeqeq
-      })
       if (((basket?.Products) != null) && basket.Products.length > 0) {
         for (let i = 0; i < basket.Products.length; i++) {
           basket.Products[i].name = req.__(basket.Products[i].name)
```

と、どのように修正したかもばっちり記録されています、あとはこれをリモートにpushするだけです。

もちろん業務でClaude Codeなどを使っている人はもっと簡単に利用できます。公式にあるように`npx skills add`でインストールするのはもちろん、「同じディレクトリにあるsecurity-audit-skill内のスキルファイルを利用して脆弱性を診断して」くらいの粗い指示でも、結果を返してくれると思います（これは社内環境で検証しないとな…）

いかがでしたでしょうか？既にAIエージェントを使用して自動でコードを作成、修正した人にとっては半分以上は知っている話だったかもしれません。しかし今後AIによりコーディングのスピードはさらに加速していくでしょう。同時にセキュリティは担保されていないといけません。Cloudflare謹製のセキュリティ監査用エージェントスキルを併用することで、より安全なコードを生成することができます。活用しない手はありません。

ただし、これは自戒を込めて忘れないようここに記していますが、攻撃者もAIを使い、防御側もAIを使うのであれば互角です。防御側は攻撃側を上回らなければなりません。その差は結局人間の差が出ると思います。AIは人間の力をブーストする存在。僕たち自体がセキュリティに日々関心を持ち、スキルを磨いていくことの重要性は変わらないでしょう。