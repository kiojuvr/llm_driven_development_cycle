# Example Set: Runtime Workflow Boundary

このディレクトリは、`templates/` にある雛形の記入例を 1 セットで示すものです。

題材は、`post-turn control handling` における runtime と app の境界摩擦です。

## 読み順

1. `probe_log_example.md`
2. `learning_log_example.md`
3. `boundary_friction_log_example.md`
4. `evidence_packet_example.md`
5. `workflow_audit_example.md`
6. `bounded_lane_kickoff_example.md`
7. `closeout_example.md`
8. `parking_statement_example.md`

## テンプレート対応

- `templates/probe_log_template.md` -> `probe_log_example.md`
- `templates/learning_log_template.md` -> `learning_log_example.md`
- `templates/boundary_friction_log_template.md` -> `boundary_friction_log_example.md`
- `templates/evidence_packet_template.md` -> `evidence_packet_example.md`
- `templates/workflow_audit_template.md` -> `workflow_audit_example.md`
- `templates/bounded_lane_kickoff_template.md` -> `bounded_lane_kickoff_example.md`
- `templates/closeout_template.md` -> `closeout_example.md`
- `templates/parking_statement_template.md` -> `parking_statement_example.md`

## 例の意図

- probe から lane までどう昇格するかを見せる
- closeout と parking をどう分けるかを見せる
- LLM worker が自走しやすい粒度を示す

この例は仮想ケースですが、`blocked consumer`、`contract drift`、`ownership conflict` の書き分けが分かるようにしてあります。

`closeout` と `parking` の日付を 2026-04-25 にしているのは意図的です。lane を開いた日と閉じた日が同じとは限らないため、終端文書が翌日に書かれるケースを例にしています。
