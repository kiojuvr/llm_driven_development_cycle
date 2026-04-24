# Learning Log

記入方針: 学習結果を後続 worker が再利用できるように、confirmed と tentative を分けて書きます。

## Date

2026-04-24

## Topic

post-turn control outcome の ownership

## Source probes

- `probe_log_example.md`

## Confirmed learnings

- current live path では app が post-turn outcome を局所的に解釈している
- `runtime_protocol` は execution result を持つが、次アクションの意味は十分に持っていない
- trace は control decision の説明能力が弱い

## Tentative hypotheses

- post-turn outcome は runtime ownership に寄せたほうが drift を減らせる可能性がある
- ただし、すぐに generic contract を作るのは過剰かもしれない

## Boundary implications

- app と runtime の ownership boundary が曖昧
- trace surface は correctness より explainability の圧力として現れている

## Unknowns

- 具体的に困っている blocked consumer が 1 つか複数か
- 現状の摩擦が duplicated semantics まで進んでいるか

## Next probe if needed

trace consumer と post-turn handler の双方で、同じ意味が二重に解釈されていないか確認する。
