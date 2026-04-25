# Bounded Lane Kickoff

記入方針: lane を広げないために、scope と non-goals を先に固定します。

## Date

## Lane name

## Status

## Trigger evidence

どの audit / evidence packet から来た lane かを書く。

## Starting posture

前段の steady state / prior closeout claim を短く書く。

## Entry question

lane が答えるべき問いを 1 つに絞る。

## Scope

含める変更範囲を具体的に書く。

## Non-goals

今回やらないことを明示する。

## Affected owners

## Surfaces affected

- docs:
- code:
- tests:
- observability:

## Expected artifacts

## Implementation constraints

- broad phase に拡張しない
- lane 以外の closed family を reopen しない
- scope 追加が必要なら新しい audit に戻る

## Validation plan

## Closeout criteria

満たせば lane を閉じられる条件を書く。

## Reopen conditions

## Target posture after closeout

- current bounded lane = unselected に戻せるか
- next bounded lane は選ばずに閉じるか
- post-closeout watch が必要か
