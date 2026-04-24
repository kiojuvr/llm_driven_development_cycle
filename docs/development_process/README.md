# development_process

## 目的

このディレクトリは、LLM駆動開発サイクルを実運用できる形で定義するための docs セットです。

中心課題は、LLM が高速に変更案を出せる環境で、変更を無制限に広げず、根拠にもとづいて bounded に進めることです。

このディレクトリが、このリポジトリにおける運用ルールの正本です。

## 運用成熟度

この docs セットは、実証済みの運用コアと、そこから正規化した周辺運用をまとめたものです。

特に `audit -> bounded lane -> closeout -> steady state` は、実際に 1 か月以上の運用で drift 防止に効いていたコア手順です。一方で、`probe`、`learning log`、`friction log` を含む全体サイクルは、その知見を再利用しやすくするために整理したテンプレートであり、今後の運用で調整が入る可能性があります。

また、実運用では `docs/` 直下に生成された多数の文書を `INDEX.md` で時系列に案内し、各文書にワンライン説明を付ける補助運用も行われていました。これはコアサイクルの定義そのものではありませんが、evidence の探索性と再開性を支える補助要因だった可能性があります。

このリポジトリでは、現時点ではそれを必須ルールではなく、観測された有効な周辺実務として扱います。

## 読み順

まず次の順で読むことを想定します。

1. `llm_driven_development_cycle.md`
2. `research_intake.md`
3. `phase_switching_guide.md`
4. `terminology.md`
5. `decision_rules.md`
6. `worker_handoff_protocol.md`

実務では、必要なテンプレートを `templates/` から選んで使います。

## 文書一覧

- `llm_driven_development_cycle.md`: 全体サイクルの定義
- `research_intake.md`: 外部知見を lane の前段で扱う intake ルール
- `phase_switching_guide.md`: 序盤・中盤・終盤の切り替え基準
- `terminology.md`: 重要語彙の定義
- `decision_rules.md`: lane を開く / 開かない判断ルール
- `worker_handoff_protocol.md`: LLM worker への作業依頼形式
- `templates/`: 実務で使うテンプレート
- `examples/`: テンプレートの記入例

## テンプレートと記入例

最初に雛形だけを見るより、対応する記入例を横に置いて読むほうが使いやすいです。

- `templates/probe_log_template.md` -> `examples/example_runtime_workflow_boundary/probe_log_example.md`
- `templates/learning_log_template.md` -> `examples/example_runtime_workflow_boundary/learning_log_example.md`
- `templates/boundary_friction_log_template.md` -> `examples/example_runtime_workflow_boundary/boundary_friction_log_example.md`
- `templates/evidence_packet_template.md` -> `examples/example_runtime_workflow_boundary/evidence_packet_example.md`
- `templates/workflow_audit_template.md` -> `examples/example_runtime_workflow_boundary/workflow_audit_example.md`
- `templates/bounded_lane_kickoff_template.md` -> `examples/example_runtime_workflow_boundary/bounded_lane_kickoff_example.md`
- `templates/closeout_template.md` -> `examples/example_runtime_workflow_boundary/closeout_example.md`
- `templates/parking_statement_template.md` -> `examples/example_runtime_workflow_boundary/parking_statement_example.md`
- `templates/concept_digest_template.md` -> `examples/example_research_intake/concept_digest_example.md`
- `templates/watchlist_template.md` -> `examples/example_research_intake/watchlist_example.md`

## 参照資料との関係

`references/` 配下には、起点となった会話ログや初期メモを置きます。そこに同じ概念の古い表現や別言語版が存在していても、運用判断ではこの `docs/development_process/` 配下を優先します。

## 言語方針

このディレクトリは日本語を正とします。将来英語版を作る場合でも、ここで定義した意味と判断ルールを先に確定させます。

## 運用原則

- 速く作ることより、何を開くかを正しく決めることを優先する
- 探索と昇格可能な変更を混同しない
- reusable な意味や契約を変える場合は、bounded lane を開く
- lane は必ず closeout まで含めて扱う
- justified な lane がない状態を steady state とみなす
