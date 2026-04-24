# Probe Log

記入方針: 観察と推測を分けて書き、まだ設計昇格を正当化しないことを明示します。

## Date

2026-04-24

## Area

post-turn control handling

## Purpose

turn 実行後に「継続」「停止」「委譲」の判断がどこで行われているかを把握したい。
特に、app-local な分岐が runtime の意味論に昇格していないかを確認する。

## Starting assumption

現時点では app 側に局所分岐があるが、まだ reusable contract とまでは言えない可能性がある。

## Files / surfaces inspected

- `app` の post-turn handler
- `runtime_protocol` の result type
- turn loop の call chain
- trace 出力の assembling path

## Observations

- post-turn 後の next action 判定が app 側の条件分岐で行われている
- `runtime_protocol` には継続可否を直接表す型がない
- trace では「なぜ止まったか」と「なぜ継続したか」が対称に残っていない

## Confirmed facts

- live path 上で next action 判定は少なくとも 1 箇所 app-local に存在する
- protocol type だけでは post-turn outcome の区別が足りない
- trace consumer は stop / continue の理由を同じ粒度で読めない

## Open questions

- blocked consumer が既に存在するか
- runtime ownership に昇格すべき意味論か
- 局所 patch で閉じられる範囲か

## What this does not justify yet

- 新しい runtime control plane の設計
- generic orchestration API の追加
- 全 workflow の再設計

## Suggested next step

probe 結果を learning log にまとめ、trace consumer と turn loop の friction を切り分ける。
