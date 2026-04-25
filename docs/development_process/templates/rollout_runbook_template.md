# Rollout Runbook

記入方針: 実装後に変更をどう candidate / default / watch に進めるかを固定する runbook として書きます。

## Date

## Lane name

## Change surface

- docs:
- code:
- config:
- operator / workflow:

## Candidate state

candidate として何が有効で、何がまだ default でないかを書く。

## Activation method

config、docs、operator 手順など、どう切り替えるかを書く。

## Smoke session

- query / command set:
- expected outputs:
- expected routing / observability:

## Diagnostics / self-check

- baseline commands:
- post-change commands:
- expected pass / fail interpretation:

## Promotion criteria

candidate -> default に上げてよい条件を書く。

## Rollback triggers

事前に固定する。

## Rollback method

## Post-default watch

必要なら `post_closeout_watch_log_template.md` を参照する。

## Closeout handoff

closeout に何を引き継ぐかを書く。
