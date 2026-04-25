# Closeout

記入方針: 進捗報告ではなく、何が確定し、何が deferred のままかを明示する終端文書として書きます。

## Date

2026-04-25

## Lane name

Post-Turn Outcome Contract Introduction

## Status

closed

## What changed

- post-turn outcome を runtime-owned contract として明示した
- turn loop は app-local 条件分岐ではなく contract を参照して次アクションを決めるようになった
- trace surface で stop / continue reason を同じ粒度で扱うようにした

## What did not change

- delegation semantics 全体は変更していない
- generic workflow engine は導入していない
- trace の表現スタイル全体は見直していない

## Final ownership

post-turn outcome の意味論は runtime が持つ。app はその contract を消費する側に留まる。trace は runtime-owned outcome を説明面で露出する。

## Fixed assumptions

- next action の意味は app-local convenience ではなく reusable contract として扱う
- trace explainability は loop semantics から独立して定義しない

## Deferred assumptions

- delegation を含む広い control family を 1 つの contract に統合するかは未確定
- 複数 workflow 間で同じ outcome family を再利用するかは未確定

## Validation

- turn loop の live path で contract 経由の next action selection を確認
- trace review で stop / continue reason が対称に読めることを確認
- docs と code comments の ownership 記述を一致させた
- tests と trace 出力の双方で observability surface を確認した
- docs / code / tests / observability の claim が揃っていることを確認した

## Reopen conditions

- 新しい workflow が current outcome family では表現できない理由を要求した場合
- app が再び独自の next action semantics を持ち始めた場合

## Post-closeout watch

不要。今回の lane は focused contract 導入であり、追加の watch を要する未固定な drift 面を残していない。

## Resulting steady state

current repository では post-turn outcome ownership に関する active lane は存在しない。次に動くのは、新しい blocked consumer が現れた場合のみ。

## Lane posture

- current bounded lane: `unselected`
- next bounded lane: `unselected`
