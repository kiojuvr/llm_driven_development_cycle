# Workflow Audit

記入方針: 最終設計ではなく、進めるべきか止めるべきかを判断する監査として書きます。

## Date

## Purpose

## Current starting assumption

## Audit question

Yes / No または allowed outcome を選べる問いにする。

## Scope

## Primary inputs

## Live paths to inspect

少なくとも 1 つは実コードの流れを書く。

## Surfaces to check

- docs:
- code:
- tests:
- observability:

## Core checks

## Evidence entries

確認した事実を箇条書きで残す。

## Allowed outcomes

- Outcome A: no new lane justified
- Outcome B: pressure exists but continue watching
- Outcome C: concrete trigger found, open one bounded lane

## Non-goals

この audit でやらない設計や実装を書く。

## Completion criteria

- `no new lane justified` の場合でも steady-state posture を書ける
- lane を開く場合は first bounded slice の entry question を 1 つに絞れる

## Final rule

最後に選んだ outcome と、その根拠を 1-3 行で書く。

## Resulting posture

- current bounded lane:
- next bounded lane:
- watch needed?:
