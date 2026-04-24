# LLM駆動開発サイクル docs テンプレート

## このリポジトリの目的

このリポジトリは、LLM駆動開発における開発運用モデルを docs テンプレートとして整備するための起点です。

ここで扱う中心テーマは、コード生成そのものではなく、LLM が高速に変更案を出せる状況で、どの変更を開き、どの変更を開かないかをどう統治するかです。

従来の開発手法で言えば、次の要素に近いものを含みます。

- Agile
- Design Doc
- Architecture Decision Record
- Spike
- RFC
- Clean Architecture
- DDD
- Release Engineering

ただし、そのままの焼き直しではありません。LLM駆動開発では、課題の重心が「どう書くか」から「何を開くべきか / 何を開かないべきか」へ移るためです。

## 中心となる開発サイクル

このリポジトリで土台にする運用サイクルは、次の流れです。

`probe -> learning log -> friction log -> audit -> bounded lane -> closeout -> steady state`

このサイクルは、LLM駆動開発における変更圧力を統治するためのものです。

特に、次のような価値があります。

- 実験と昇格可能な変更を区別できる
- 変更の影響範囲を bounded lane として限定できる
- closeout によって変更の帰結と未解決事項を明示できる
- steady state を「根拠のある未着手状態」として維持できる

## このリポジトリで先に作るもの

いきなり解説書を書くのではなく、まず LLM に渡せる運用フルセットを先に整備します。

想定している最小構成は次のとおりです。

```text
docs/development_process/
  README.md
  llm_driven_development_cycle.md
  phase_switching_guide.md
  terminology.md
  decision_rules.md
  worker_handoff_protocol.md
  templates/
    probe_log_template.md
    learning_log_template.md
    boundary_friction_log_template.md
    evidence_packet_template.md
    workflow_audit_template.md
    bounded_lane_kickoff_template.md
    closeout_template.md
    parking_statement_template.md
```

## 各文書の役割

### `README.md`

入口となる文書です。何のためのプロセスか、どの文書から読むべきかを示します。

### `llm_driven_development_cycle.md`

中核文書です。`probe` から `steady state` までの全体サイクルを定義します。

### `phase_switching_guide.md`

序盤・中盤・終盤の切り替え基準を定義します。いま必要なのが `probe` なのか、`lane` なのか、`policy/regression` 対応なのかを判定するための文書です。

### `terminology.md`

語彙集です。`bounded lane`、`blocked consumer`、`contract drift`、`steady state`、`parking` などの重要語を定義します。

### `decision_rules.md`

実務上の判断ルールを整理します。何を根拠に lane を開くか、何を根拠に開かないかを明文化します。

### `worker_handoff_protocol.md`

Codex / OpenCode / Qwen / GPT などの LLM worker に作業を渡す形式を定義します。探索、監査、lane 実装を混同させないための protocol です。

### `templates/`

実際に使う雛形群です。思想だけでなく、すぐ運用に使える状態を目指します。

## 重要な概念

このリポジトリでは、特に次の概念を重要視します。

### 変更圧力の統治

LLM は大量の変更案を生成できます。したがって、人間や上位の運用ルールの役割は、変更を生成することよりも、変更を選別し、正当化し、境界づけることになります。

### bounded lane

単なる task ではなく、影響範囲、非目標、closeout 条件を持った変更ラインです。

### steady state

何もしていない状態ではありません。正当化された active lane が存在しない、健全な repository posture を指します。

### probe と lane の区別

序盤では捨てられる探索が必要です。中盤以降は、昇格可能な契約変更だけを lane として扱います。

### blocked consumer

「将来必要そう」ではなく、今その契約がないと困る具体的な利用者や workflow を指します。

### contract drift

局所的には正しく見える変更が、境界や意味論を少しずつ崩していく状態です。LLM駆動開発では特に注意が必要です。

### parking

止まっている状態ではなく、再開条件つきで意図的に閉じている状態です。

## このテンプレートの使い道

この運用は、特定の 1 プロジェクトだけのものではありません。特に次のような開発に対して汎用性があります。

- LLM agent を含む開発
- 複数コンポーネントを持つ中長期プロジェクト
- Rust など型中心のアーキテクチャ開発
- protocol / runtime / orchestration を含むシステム
- 仕様が実装と同時に発見されるプロジェクト
- 複数の LLM worker を使う開発

## 今後の進め方

優先順位は次のとおりです。

1. docs テンプレートとして十分に使える運用文書群を整備する
2. LLM worker にそのまま渡せるフルセットにする
3. その後に、解説書を作る

解説書の作成はこのリポジトリの重要な将来計画ですが、急ぎません。まずは docs を十分に構築し、実運用に耐える形にすることを優先します。

## 元ログ

この README は [chat_log.txt](/home/kioju/GitHub/llm_driven_development_cycle/chat_log.txt) をもとに、起点文書として読みやすい形へ整理したものです。元の会話ログは履歴として残します。
