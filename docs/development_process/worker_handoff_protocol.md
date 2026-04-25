# Worker Handoff Protocol

## 目的

LLM worker に対して、探索、監査、lane 実装を混同させずに作業を依頼するための形式を定義します。

## 基本方針

- vague な改善依頼をしない
- task type を先頭で明示する
- 最初に読む文書を指定する
- non-goals を明記する
- lane を勝手に広げないよう制約を書く
- 開始 posture と終了 posture を書く
- code だけでなく observability / docs / tests の確認対象を指定する

## 推奨フォーマット

```markdown
You are operating under `docs/development_process/`.

Task type:
- <research intake | concept digest | probe | audit | gate transition | bounded lane implementation | execution brief | rollout runbook | closeout>

Read:
- <required docs>
- <required template>

Task:
- <what to do>

Do not:
- <explicit non-goals>

Expected output:
- <artifact names>

Validation:
- <tests or checks>
- <diagnostics / self-check / observability checks if relevant>

Starting posture:
- <current bounded lane = ... / steady state claim / prior closeout claim>

Target posture:
- <Outcome A/B/C or closeout / steady state / post-closeout watch>
```

## task type ごとの注意

### research intake

- 外部知見を lane と混同させない
- source の要点、relevance、non-action decision を先に書かせる
- 行き先を watch / probe / design constraint / audit / lane / park から選ばせる

### concept digest

- source の要約よりも repo への relevance mapping を重視する
- classification を 1 つ明示させる
- revisit trigger を必ず書かせる

### probe

- 目的は理解であり、設計昇格ではない
- live path の確認を優先する
- 提案より観察を重視する

### audit

- allowed outcome を 1 つ選ばせる
- evidence を伴わない設計拡張を禁止する
- lane を開く場合でも 1 本に限定する
- docs / code / tests / observability のどこを見たか書かせる
- no new lane justified の場合でも steady-state posture を明記させる

### gate transition

- Outcome C をそのまま実装開始と混同させない
- readiness、owner、shared posture update point を書かせる
- pass / hold の二択に絞らせる
- hold の場合の next action を明記させる

### bounded lane implementation

- scope と non-goals を固定する
- affected owners を意識させる
- closeout 条件を最初から持たせる
- first bounded slice を超える phase 設計に拡張させない
- observability drift を伴う lane なら確認面を明示させる

### execution brief

- 実装順序を固定する
- 曖昧時の判断ルールを書かせる
- explicit do-not-do を持たせる
- config / operator / rollout dependency があるか先に切らせる

### rollout runbook

- candidate / default / watch を混同させない
- rollback trigger を先に書かせる
- smoke session と diagnostics の再実行手順を固定させる
- closeout と watch に何を引き継ぐか書かせる

### closeout

- 何が fixed され、何が deferred かを区別する
- reopen condition を明記する
- future work の願望を書かせない
- no-code closeout も許容する
- steady-state posture と、必要なら post-closeout watch を書かせる
- no-code closeout では intentional reading と bounded compatibility reading を混同させない

## 悪い依頼の例

> Improve the runtime architecture.

## 良い依頼の例

> Execute the workflow audit for post-turn control handling. Inspect at least one live call chain, record evidence entries, and select exactly one allowed outcome. Do not redesign the control plane.

## セッション間 posture 共有

複数 worker や別セッションへ引き継ぐ場合は、毎回少なくとも次を共有します。

- current bounded lane
- next bounded lane
- latest controlling doc
- shared posture update point
- write scope

同時並行で複数 worker を使う場合の原則:

- probe と audit は並行してよいが、write scope は分ける
- current bounded lane を変える文書は 1 つの更新点に寄せる
- 同じ lane を別 posture で進めない
