# Bounded Lane Kickoff

記入方針: lane を広げないために、scope と non-goals を先に固定します。

## Date

2026-04-24

## Lane name

Post-Turn Outcome Contract Introduction

## Status

open

## Trigger evidence

`workflow_audit_example.md` で Outcome C。trace consumer と turn loop の双方に blocked consumer が確認された。

## Starting posture

audit 前は runtime workflow boundary に active lane はなく、`current bounded lane = unselected` だった。今回の lane はその steady state を破るだけの concrete trigger が確認されたため開く。

## Entry question

post-turn outcome を runtime-owned contract として最小限導入し、trace と loop の意味を一致させられるか。

## Scope

- post-turn outcome の限定的な contract 追加
- turn loop での next action 判定の整理
- trace surface の reason 表現を対称化

## Non-goals

- generic orchestration API の導入
- delegation policy の再設計
- unrelated trace formatting の変更

## Affected owners

- runtime
- app
- trace surface

## Surfaces affected

- docs: ownership と closeout 記述
- code: post-turn handler / next action selection / trace assembly
- tests: loop action choice と trace reason 表示
- observability: stop / continue reason の対称性

## Expected artifacts

- contract definition
- loop integration
- trace update
- closeout note

## Implementation constraints

- lane 外の control semantics を開かない
- app-local convenience を generic API に昇格させない
- trace wording のみの cosmetic change に逃げない
- shell / flow-control 全体の broad phase に広げない
- 他の closed family を再開しない
- scope 追加が必要なら新しい audit に戻る

## Validation plan

- turn loop が contract を介して次アクションを決める
- trace が stop / continue reason を同粒度で持つ
- docs とコードの ownership 記述が一致する

## Closeout criteria

- post-turn outcome の owner が明示される
- trace と loop の意味が同じ contract を参照する
- reopen condition が書ける

## Reopen conditions

- delegation semantics まで contract 拡張が必要になった場合
- 複数 workflow で再び duplicated semantics が発生した場合

## Target posture after closeout

- current bounded lane = unselected に戻す
- next bounded lane は選ばずに閉じる
- post-closeout watch は不要と想定する
