# Phase Kickoff Packet

## Date

2026-04-25

## Candidate phase

Shell / Flow-Control Boundary Clarification

## Purpose

semantic-core family を再開せずに、次の pressure 候補が shell / flow-control 側にあるかを整理する。

この packet では phase 開始そのものではなく、phase 検討が正当か、正当なら first bounded slice をどう切るかを固定する。

## Current posture

- current bounded lane: `unselected`
- next bounded lane: `unselected`
- related steady-state claims:
  - `minimum_loop` は steady state にある
  - `world_model` は resume conditions が未充足のまま steady state にある

## Why this phase is being considered

current repository では semantic core 自体よりも、その外側で既存の bounded module をどう選択し、どう接続し、どう handoff するかの圧力が今後先に顕在化しやすい。

ただし、これは product pressure の予測を含む作業仮説であり、まだ activation evidence ではない。

## What this packet does not authorize

- broad shell implementation の開始
- `minimum_loop` や `world_model` の再開
- 複数 lane の同時開始
- semantic-core redesign の混入

## Activation question

current repository は、semantic-core の既存 steady-state claims を保ったままでも、shell / flow-control の reusable boundary を first bounded slice として開く必要がある段階に入っているか。

## Candidate pressure

- blocked path:
  - 現時点では concrete blocked path は未確定
  - 将来の session handoff や routing pressure は予感されるが、まだ live path で具体化していない
- ownership gap:
  - orchestration と app-local wiring の境界は今後問題化しうるが、現在ただちに owner 不在とは言えない
- contract absence:
  - shell-level handoff contract は未明示だが、現行 workflow が即座に破綻しているわけではない
- observability / explainability drift:
  - control-loop decisions の説明面は将来 pressure になりうるが、現時点で improper regression は確認されていない

## Related inputs

- prior closeout:
  - `minimum_loop` 系 closeout 群
  - `world_model` 系 closeout 群
- prior audit:
  - `next lane discovery` で `no new lane justified`
  - `world_model resume conditions audit` で `resume not justified`
- current-state docs:
  - semantic-core steady-state docs
  - current ownership / boundary notes
- inspected code / tests / traces:
  - runtime orchestration call path の概要
  - trace / health / operator-facing control まわりの現状メモ

## Activation conditions

- `minimum_loop` と `world_model` の steady-state claims がまだ有効である
- shell / flow-control 側に concrete blocked path か ownership gap が現れている
- 問題が app-local wiring cleanup では honest に閉じられない
- outer-shell contract を reusable boundary として定義する必要がある
- first bounded slice を 1 問に絞って書ける

## Non-activation conditions

- broad phase 名だけが先に立ち、first bounded slice が書けない
- blocked consumer が具体化していない
- app-local patch で honest に閉じられる
- semantic-core の fresh trigger のほうが優先される

## Candidate entry signals

- 複数 call site が同じ flow decision semantics を必要とし始める
- session / operator handoff が暗黙 state では扱えなくなる
- control-loop transition の observability が live troubleshooting を妨げ始める
- app-local orchestration が複数箇所で互いに異なる前提を持ち始める

## Proposed first bounded slice

- entry question:
  - turn completion 後の next-action decision を outer-shell contract として最小限固定する必要があるか
- in-scope files / modules:
  - runtime orchestration entrypoint
  - post-turn routing / handoff boundary
  - related trace / observability surface
- out-of-scope areas:
  - semantic-core redesign
  - full session state machine
  - delegation policy 全体
- affected owners:
  - app runtime
  - shell / orchestration boundary
  - observability surface
- expected artifacts:
  - workflow audit
  - bounded lane kickoff
  - narrow contract note or closeout
- closeout criteria:
  - local wiring cleanup で十分か reusable boundary が必要かを明確化できる
  - owner が曖昧なまま広い shell work に逃げない

## If not activated

steady state を維持する。必要なら watch に留め、concrete coordination pressure が live path で観測されるまで lane は開かない。

## Final rule

現時点では phase 自体の activation はまだ正当化されない。shell / flow-control は plausible な次候補だが、current repository pressure はまだ first bounded slice を開く threshold に達していない。

## Resulting posture

- current bounded lane: `unselected`
- next bounded lane: `unselected`
- next action: steady state を維持し、coordination pressure が concrete になった時点で workflow audit から再開する
