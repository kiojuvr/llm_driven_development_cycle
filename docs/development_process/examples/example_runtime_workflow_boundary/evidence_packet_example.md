# Evidence Packet

記入方針: lane を開く前段として、trigger が concrete かどうかを示す資料として書きます。

## Date

2026-04-24

## Candidate area

post-turn control outcome ownership

## Trigger class

- blocked consumer
- contract drift
- ownership conflict

## Primary evidence

- trace consumer が stop / continue の理由を安定的に読めない
- turn loop が app-local な分岐に依存しており、protocol から次アクションを説明できない
- docs 上では runtime が control を持つように読めるが、live path では app が意味を持っている

## Live paths checked

- turn completion -> post-turn handler -> next action selection
- execution result -> trace assembly -> reviewer-facing trace

## Validation basis

- tests / build commands:
  - `cargo test -p app --lib execution::tests::...`
  - `cargo test -p app --lib`
- diagnostics / self-check commands:
  - `cargo run -p app -- self-check audit list`
- observability strings / metrics:
  - trace 上で stop / continue reason が同粒度で出るか
- config surface checked:
  - current runtime config では post-turn outcome の owner が外から切り替わらないこと

## Concrete consumer

- trace review workflow
- post-turn continuation logic

## Why local patch is insufficient

trace 側だけ直すと loop 側との意味がずれ、loop 側だけ直すと trace の explainability が残る。局所 patch では ownership の曖昧さを温存する。

## Recommended audit question

post-turn outcome は runtime-owned な bounded contract として明示すべきか。
