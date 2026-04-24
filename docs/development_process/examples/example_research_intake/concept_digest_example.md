# Concept Digest

## Date

2026-04-24

## Title

Confidence-gated retrieval for agent memory access

## Source

論文メモ。長文コンテキスト下で retrieval を常時有効にするより、confidence が低い局面だけ retrieval を強める方が context pollution を抑えやすいという主張。

## Core claim

- retrieval は常時強くするほどよいわけではない
- confidence や uncertainty に応じて retrieval 強度を変える設計が有効かもしれない
- retrieval policy は memory quality だけでなく control flow にも影響する

## Why it matters

この repo では外部知見を lane の前段で扱う枠組みを整えており、memory 系の概念をすぐ canonical 化しない判断が重要になるため。

## Possible relevance

- cognitive-agent 系 repo では memory retrieval policy の設計制約になりうる
- この repo 自体では、research intake で扱うべき典型例として有用

## Affected areas

- runtime / control flow: retrieval を呼ぶ条件に影響する
- domain model / contracts: memory access policy の契約候補になりうる
- observability / debugging: retrieval 発火理由の説明可能性が必要になる
- docs / process: 外部知見の digest 例として使える

## Classification

Design Constraint

## Immediate action

watch

## Non-action decision

まだ bounded lane は開かない。現 repo には blocked consumer がなく、成功条件も定量化されていないため。

## Revisit trigger

- memory retrieval policy を扱う repo で blocked consumer が出たとき
- retrieval の常時実行が context pollution を起こした evidence が出たとき
- toy probe で confidence gating の有無を比較する価値が生じたとき

## Notes

外部知見の intake では、この段階で実装を始めないこと自体が判断結果になる。
