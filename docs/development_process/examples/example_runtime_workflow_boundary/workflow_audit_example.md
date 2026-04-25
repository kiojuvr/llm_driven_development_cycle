# Workflow Audit

記入方針: 最終設計ではなく、進めるべきか止めるべきかを判断する監査として書きます。

## Date

2026-04-24

## Purpose

post-turn outcome ownership を bounded lane として開く必要があるか判断する。

## Current starting assumption

app-local な分岐で当面は動いているが、trace と loop の双方で pressure がある可能性が高い。

## Audit question

post-turn outcome を runtime-owned contract として限定的に導入しないと、current workflow が clean に進まないか。

## Scope

- live path の確認
- blocked consumer の確定
- allowed outcome の選択

## Primary inputs

- `probe_log_example.md`
- `learning_log_example.md`
- `boundary_friction_log_example.md`
- `evidence_packet_example.md`

## Live paths to inspect

- turn completion -> post-turn handler -> next action selection
- execution result -> trace assembly

## Surfaces to check

- docs: ownership と closeout claim の整合
- code: post-turn handler と trace assembly の責務分離
- tests: next action selection と trace reason の期待値
- observability: stop / continue reason の trace 表示粒度

## Core checks

- trace consumer は本当に困っているか
- loop 側で duplicated semantics が存在するか
- 局所修正で honest に閉じられるか

## Evidence entries

- trace review では stop / continue reason の非対称がレビュー負荷を上げている
- loop 側は app-local 分岐を保持しており、protocol だけ読んでも次アクションが確定しない
- trace 側だけの補修では ownership conflict が残る

## Allowed outcomes

- Outcome A: no new lane justified
- Outcome B: pressure exists but continue watching
- Outcome C: concrete trigger found, open one bounded lane

## Non-goals

- generic workflow engine の設計
- delegation semantics 全体の刷新
- runtime 全面リファクタ

## Completion criteria

- blocked consumer の有無を明記する
- allowed outcome を 1 つ選ぶ
- 選んだ outcome の根拠を live path ベースで書く
- steady-state 維持か bounded lane 開始かを posture として明記する
- lane を開くなら first bounded slice の問いを 1 つに限定する

## Final rule

Outcome C を選ぶ。trace consumer と turn loop の両方が current workflow 上の blocked consumer であり、ownership conflict を局所 patch だけで閉じるのは不誠実である。bounded lane は post-turn outcome contract の導入に限定する。

## Resulting posture

- current bounded lane: `Post-Turn Outcome Contract Introduction`
- next bounded lane: `unselected`
- watch needed?: no
