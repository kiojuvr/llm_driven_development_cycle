# Research Intake

## 目的

この文書は、外部知見を bounded lane の前段で扱うための intake ルールを定義します。

対象は、論文、記事、会話、他 repo、設計メモ、運用知見など、現在の repo 外から入ってくる概念です。

## なぜ必要か

既存の `audit -> bounded lane -> closeout -> steady state` は、current repo を守るには有効です。

一方で、外部知見は最初から blocked consumer や contract drift の形をしていないことが多く、そのままでは「重要そうだが lane を開く根拠はまだない」という状態を受け止められません。

この入口がないと、外部知見は次の二択に崩れます。

- すぐ実装する
- 捨てる

これは避けます。外部知見の取り込みは、即時実装を意味しません。

## 基本フロー

標準の intake フローは次のとおりです。

`external signal -> research intake -> concept digest -> relevance mapping -> classification -> watch / probe / design constraint / audit / bounded lane / park`

## 基本原則

- 外部知見を、いきなり bounded lane にしない
- 取り込みと実装を同一視しない
- まず relevance と影響面を記録する
- lane に昇格しない判断も有効な成果とみなす
- current repo への concrete な接続がないなら、watch か park を優先する

## まず書くもの

外部知見を見て「これは重要そうだ」と感じたら、最初に `templates/concept_digest_template.md` を使って digest を作ります。

最低限、次を明文化します。

- 何を読んだか
- core claim は何か
- repo のどこに関係しうるか
- 何に分類するか
- 今すぐ何をしないか
- どの trigger が出たら再考するか

## classification

外部知見は、少なくとも次のどれかに分類します。

### Concept Seed

将来重要そうだが、current repo に concrete pressure はまだない概念です。

扱い:

- digest に保存する
- lane は開かない
- watchlist に置くかを判断する

### Probe Candidate

小さい実験で価値を確認できる候補です。

扱い:

- bounded lane ではなく `probe` に接続する
- 成功条件は「学習」または「切り捨て判断」に置く
- canonical 化を急がない

### Design Constraint

今すぐ実装しないが、今後の設計判断を制約する知見です。

扱い:

- digest に明記する
- 必要なら関連 docs の判断ルールに反映する
- lane は開かない

### Audit Trigger

外部知見によって、既存設計の危険や drift 候補が見えたものです。

扱い:

- `audit` に接続する
- 既存 repo への concrete impact を確認する
- まだ実装は始めない

### Lane Candidate

外部知見が、すでに current repo の blocked consumer、contract drift、ownership conflict、duplicated semantics に接続できるものです。

扱い:

- `audit` を経るか、十分に concrete なら bounded lane 候補にする
- kickoff と closeout 条件を先に書く

## 行き先の選び方

### watch

重要だが、まだ trigger が未成熟なら `watchlist` に置きます。

### probe

小さい検証で意味があるなら `probe` に送ります。

### design constraint

今後の判断ルールにだけ影響させたいなら、constraint として残します。

### audit

既存 repo に対する concrete な危険や圧力が見えたら `audit` に送ります。

### bounded lane

current repo と直接つながる concrete trigger があり、closeout 条件まで定義できるときだけ開きます。

### park

重要そうでも、今は扱うべきでないなら再開条件つきで閉じます。

## lane に昇格してよい条件

次の条件が揃うときに限って、外部知見を bounded lane 候補にします。

- current repo の blocked consumer と接続できる
- 既存設計の drift risk や ownership conflict を具体化できる
- 影響範囲が bounded に書ける
- closeout 条件が定義できる
- 「何をまだやらないか」を先に固定できる

## lane に昇格してはいけない条件

- 面白いだけ
- 将来必要そうなだけ
- 実装対象が広すぎる
- 既存構造との接続が曖昧
- 成功条件が「賢くなる」「よさそう」だけ

## watchlist の役割

`parking` は一度閉じるための記録ですが、外部知見には「まだ閉じ切らない熟成棚」が必要です。

その役割を `watchlist` が持ちます。watchlist には、次を残します。

- なぜ今は lane にしないか
- どの trigger が出たら再考するか
- 関係する area や境界はどこか

## 最低限の実務ルール

- 外部知見を見ても、最初の反応を lane にしない
- まず digest を作る
- digest には non-action decision を必ず書く
- watch / probe / audit / lane のどれに送るかを明示する
- 昇格しない判断も進捗として扱う
