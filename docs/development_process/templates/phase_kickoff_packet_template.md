# Phase Kickoff Packet

記入方針: broad phase をそのまま開くための文書ではなく、phase 候補を pre-lane として評価し、first bounded slice を切り出せるかを見る packet として書きます。

## Date

## Candidate phase

phase 名を書く。まだ active lane ではない。

## Purpose

この packet で何を固定したいかを書く。

## Current posture

- current bounded lane:
- next bounded lane:
- related steady-state claims:

## Why this phase is being considered

historical momentum ではなく、current repository pressure に基づいて書く。

## What this packet does not authorize

- broad implementation の開始
- 複数 lane の同時開始
- closed family の自動 reopen

## Activation question

この phase を検討してよいかを Yes / No で判定できる問いにする。

## Candidate pressure

- blocked path:
- ownership gap:
- contract absence:
- observability / explainability drift:

## Related inputs

- prior closeout:
- prior audit:
- current-state docs:
- inspected code / tests / traces:

## Activation conditions

phase 検討を進める条件を書く。少なくとも次を含める。

- core steady-state claims がまだ有効
- pressure が concrete に言える
- 局所 cleanup では honest に閉じられない
- reusable outer boundary が本当に必要
- first bounded slice に落とせる

## Non-activation conditions

phase をまだ開いてはいけない条件を書く。

- broad phase 名しかなく first slice が書けない
- concrete trigger がない
- current issue が app-local patch で閉じられる
- semantic-core の pressure が優先される

## Candidate entry signals

phase を正当化しうる signal を列挙する。

## Proposed first bounded slice

- entry question:
- in-scope files / modules:
- out-of-scope areas:
- affected owners:
- expected artifacts:
- closeout criteria:

## If not activated

watch / park / steady state 維持のどれにするかを書く。

## Final rule

この packet の結論を 1-3 行で書く。

## Resulting posture

- current bounded lane:
- next bounded lane:
- next action:
