# Worker Handoff Protocol

## 目的

LLM worker に対して、探索、監査、lane 実装を混同させずに作業を依頼するための形式を定義します。

## 基本方針

- vague な改善依頼をしない
- task type を先頭で明示する
- 最初に読む文書を指定する
- non-goals を明記する
- lane を勝手に広げないよう制約を書く

## 推奨フォーマット

```markdown
You are operating under `docs/development_process/`.

Task type:
- <research intake | concept digest | probe | audit | bounded lane implementation | closeout>

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

### bounded lane implementation

- scope と non-goals を固定する
- affected owners を意識させる
- closeout 条件を最初から持たせる

### closeout

- 何が fixed され、何が deferred かを区別する
- reopen condition を明記する
- future work の願望を書かせない

## 悪い依頼の例

> Improve the runtime architecture.

## 良い依頼の例

> Execute the workflow audit for post-turn control handling. Inspect at least one live call chain, record evidence entries, and select exactly one allowed outcome. Do not redesign the control plane.
