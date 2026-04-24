# Parking Statement

記入方針: 放置ではなく、再開条件つきで意図的に閉じる文書として書きます。

## Date

2026-04-25

## Area

delegation-aware control family expansion

## Why it is being parked

current lane で必要だったのは post-turn outcome の最小 contract であり、delegation semantics まで広げる concrete trigger はまだない。

## What is explicitly not being done now

- delegation result taxonomy の導入
- generic control graph の設計
- multi-workflow abstraction の作成

## Evidence currently missing

- delegation workflow 側の blocked consumer
- 複数 workflow での duplicated semantics
- 現在の outcome family では表現不能な live path

## Reopen trigger

delegation を伴う current workflow が既存 contract では stop / continue / delegate を正しく区別できないと確認されたとき。

## Safe current posture

post-turn outcome contract は現在の workflow には十分であり、delegation-aware な拡張は parking で妥当である。
