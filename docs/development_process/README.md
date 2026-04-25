# development_process

## 目的

このディレクトリは、LLM駆動開発サイクルを実運用できる形で定義するための docs セットです。

中心課題は、LLM が高速に変更案を出せる環境で、変更を無制限に広げず、根拠にもとづいて bounded に進めることです。

このディレクトリが、このリポジトリにおける運用ルールの正本です。

## 運用成熟度

この docs セットは、実証済みの運用コアと、そこから正規化した周辺運用をまとめたものです。

特に `audit -> bounded lane -> closeout -> steady state` は、実際に 1 か月以上の運用で drift 防止に効いていたコア手順です。一方で、`probe`、`learning log`、`friction log` を含む全体サイクルは、その知見を再利用しやすくするために整理したテンプレートであり、今後の運用で調整が入る可能性があります。

また、実運用では作成した文書を原則として削除せず、`docs/` 直下に継続的に蓄積していました。それらを `INDEX.md` で時系列に案内し、各文書にワンライン説明を付ける運用も行っていました。

これはコアサイクルの外側にある補助運用ですが、evidence の探索性、作業再開性、判断履歴の保存にとって実務上かなり重要でした。

このリポジトリでは、まずコアサイクルを正本として定義しつつ、履歴を消さずに残すことと、必要な規模になったら `INDEX.md` を導入することを推奨します。

## 読み順

まず次の順で読むことを想定します。

1. `llm_driven_development_cycle.md`
2. `research_intake.md`
3. `phase_switching_guide.md`
4. `terminology.md`
5. `decision_rules.md`
6. `worker_handoff_protocol.md`
7. `rollout_and_promotion.md`
8. `anti_patterns.md`
9. `document_lifecycle.md`
10. `gate_transition.md`

実務では、必要なテンプレートを `templates/` から選んで使います。

## 文書一覧

- `llm_driven_development_cycle.md`: 全体サイクルの定義
- `research_intake.md`: 外部知見を lane の前段で扱う intake ルール
- `phase_switching_guide.md`: 序盤・中盤・終盤の切り替え基準
- `terminology.md`: 重要語彙の定義
- `decision_rules.md`: lane を開く / 開かない判断ルール
- `worker_handoff_protocol.md`: LLM worker への作業依頼形式
- `rollout_and_promotion.md`: candidate / default / watch と rollback を含む段階的有効化ルール
- `anti_patterns.md`: momentum や premature escalation を防ぐ anti-pattern 集
- `document_lifecycle.md`: 命名、版管理、superseded 扱い、INDEX の導入基準
- `gate_transition.md`: audit Outcome C から bounded lane 開始までの事前条件確認
- `templates/`: 実務で使うテンプレート
- `examples/`: テンプレートの記入例

## 派生ドキュメント

実運用では、本体サイクルだけでは受け止めにくい判断を補うために、派生ドキュメントが必要になることがあります。

これは本体フェーズの追加ではありません。主はあくまで

`probe -> learning log -> friction log -> audit -> bounded lane -> closeout -> steady state`

であり、派生ドキュメントはその前後や周辺で posture を固定する補助文書です。

特に有用なのは次の種類です。

- `phase kickoff packet`: 新しい phase 候補を検討する pre-lane packet。phase 自体を開く文書ではなく、first bounded slice を開いてよいかを整理する
- `gate transition runbook`: audit 後に lane を開いてよいか、誰が開くか、何が揃っているかを確認する文書
- `execution brief`: bounded lane の実装フェーズで、譲れない設計原則、禁止事項、順序付きタスク、曖昧時の判断ルールを固定する文書
- `rollout runbook`: 変更を candidate -> default -> post-closeout watch の順に段階的に有効化し、rollback trigger を先に固定する文書
- `resume conditions audit`: closeout 済みの領域を再開してよいかを確認する監査
- `reentry preconditions`: 再開に必要な条件を固定する文書
- `post-closeout watch log`: closeout 後の短い regression / drift 観測を残すログ
- `current state / ownership snapshot`: 現在 posture と ownership を圧縮して再開性を上げる文書

これらはすべて任意です。次のようなときに使います。

- steady state のまま、次の大きな pressure 候補だけを整理したい
- lane はまだ開かないが、再開条件や first slice 候補を固定したい
- audit は終わったが、lane を開く readiness と ownership を確認したい
- lane は開いたが、実装中に scope 拡張を防ぐ判断ルールが必要
- 実装後に、どの順で有効化し、何を見て rollback するかを固定したい
- 前回 closeout の惰性で broad phase を開く誤りを避けたい
- closeout claim がまだ有効かを bounded に確認したい

重要なのは、派生ドキュメントが lane の代替にならないことです。実際に開くのは常に 1 本の bounded lane であり、broad phase や将来像そのものではありません。

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
- `templates/phase_kickoff_packet_template.md` -> `examples/example_phase_kickoff_packet/phase_kickoff_packet_example.md`
- `templates/gate_transition_runbook_template.md`: audit Outcome C 後の開始条件確認 runbook
- `templates/execution_brief_template.md`: bounded lane 実装中の判断ルール書
- `templates/rollout_runbook_template.md`: candidate / default / watch / rollback の段階的有効化 runbook
- `templates/post_closeout_watch_log_template.md`: closeout 後の短期 regression / drift 観測ログ
- `templates/closeout_template.md` -> `examples/example_no_code_closeout/closeout_example.md`
- `templates/workflow_audit_template.md` -> `examples/example_audit_outcome_a/workflow_audit_example.md`
- `templates/workflow_audit_template.md` -> `examples/example_audit_outcome_b/workflow_audit_example.md`
- `templates/post_closeout_watch_log_template.md` -> `examples/example_post_closeout_watch_reopen/post_closeout_watch_log_example.md`

## 参照資料との関係

`references/` 配下には、起点となった会話ログや初期メモを置きます。そこに同じ概念の古い表現や別言語版が存在していても、運用判断ではこの `docs/development_process/` 配下を優先します。

## 言語方針

このディレクトリは日本語を正とします。将来英語版を作る場合でも、ここで定義した意味と判断ルールを先に確定させます。

## 文書運用メモ

文書数が少ない段階では `README.md` だけでも運用できますが、文書が増えたら `INDEX.md` を導入します。目安として、運用文書が 20 件前後を超えたら、時系列インデックスとワンライン説明を推奨します。詳細は `document_lifecycle.md` を参照します。

実運用では、作成済みの運用文書は原則として削除しません。履歴はノイズではなく、なぜ今の posture に至ったかを再構成するための作業資産です。

## 運用原則

- 速く作ることより、何を開くかを正しく決めることを優先する
- 探索と昇格可能な変更を混同しない
- reusable な意味や契約を変える場合は、bounded lane を開く
- lane は必ず closeout まで含めて扱う
- justified な lane がない状態を steady state とみなす
