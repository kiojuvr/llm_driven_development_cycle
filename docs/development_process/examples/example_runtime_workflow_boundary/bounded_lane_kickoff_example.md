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

## Expected artifacts

- contract definition
- loop integration
- trace update
- closeout note

## Implementation constraints

- lane 外の control semantics を開かない
- app-local convenience を generic API に昇格させない
- trace wording のみの cosmetic change に逃げない

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
