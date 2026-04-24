# development_process

## 目的

このディレクトリは、LLM駆動開発サイクルを実運用できる形で定義するための docs セットです。

中心課題は、LLM が高速に変更案を出せる環境で、変更を無制限に広げず、根拠にもとづいて bounded に進めることです。

## 読み順

まず次の順で読むことを想定します。

1. `llm_driven_development_cycle.md`
2. `phase_switching_guide.md`
3. `terminology.md`
4. `decision_rules.md`
5. `worker_handoff_protocol.md`

実務では、必要なテンプレートを `templates/` から選んで使います。

## 文書一覧

- `llm_driven_development_cycle.md`: 全体サイクルの定義
- `phase_switching_guide.md`: 序盤・中盤・終盤の切り替え基準
- `terminology.md`: 重要語彙の定義
- `decision_rules.md`: lane を開く / 開かない判断ルール
- `worker_handoff_protocol.md`: LLM worker への作業依頼形式
- `templates/`: 実務で使うテンプレート

## 運用原則

- 速く作ることより、何を開くかを正しく決めることを優先する
- 探索と昇格可能な変更を混同しない
- reusable な意味や契約を変える場合は、bounded lane を開く
- lane は必ず closeout まで含めて扱う
- justified な lane がない状態を steady state とみなす
