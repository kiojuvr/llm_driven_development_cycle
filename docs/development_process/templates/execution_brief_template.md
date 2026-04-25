# Execution Brief

記入方針: bounded lane kickoff の後に、実装フェーズで lane を広げないための判断ルール書として書きます。

## Date

## Lane name

## Starting posture

## Non-negotiable design principles

譲れない原則を列挙する。

## Explicit do-not-do list

明示的な禁止事項を書く。

## Ordered tasks

順序付きで書く。各項目に completion criteria を付ける。

## Decision rules for ambiguous situations

迷ったときの判断基準を書く。

例:

- scope 内か判断不能なら新しい audit に戻る
- local patch で honest に閉じられるなら昇格しない
- broad redesign が必要になったらこの brief を破棄して phase 側へ戻る

## Validation commands and checks

テスト、diagnostics、build、observability の確認方法を書く。

## Config / operator surfaces affected

## Rollout dependency

rollout runbook が必要ならここで参照する。

## Completion criteria

## Target posture
