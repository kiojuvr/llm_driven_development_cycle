# LLM駆動開発サイクル

## 概要

LLM駆動開発では、コードを書く速度よりも、どの変更を開くかを判断する速度と精度が重要になります。

この文書は、変更圧力を統治するための基本サイクルを定義します。

## 基本サイクル

標準サイクルは次のとおりです。

`probe -> learning log -> friction log -> audit -> bounded lane -> closeout -> steady state`

外部の論文、記事、他 repo、会話ログなどから新しい概念が入る場合は、いきなり `lane` に入れず、`research_intake.md` で定義する intake 経路を先に通します。

`external signal -> research intake -> concept digest -> relevance mapping -> classification -> watch / probe / design constraint / audit / bounded lane / park`

必要に応じて、このサイクルの周辺に派生ドキュメントを置いてよいです。たとえば `phase kickoff packet` は、broad phase 候補を整理する pre-lane packet であり、lane そのものではありません。
また、audit 後の開始条件を確認する `gate transition runbook`、lane が開いた後に scope 拡張を防ぐ `execution brief`、実装後の candidate / default / watch を扱う `rollout runbook` を置いてよいです。

## 各フェーズ

### probe

捨ててもよい探索です。未知の構造、責務、実コードの流れを調べます。

この段階では、設計の昇格や広いリファクタはまだ正当化されていません。

次へ進む条件: 複数回の probe にまたがって参照したい事実が出た、または他の worker に引き継ぐ価値がある観察が出たら `learning log` に進みます。

### learning log

probe で得た事実、観察、暫定仮説を記録します。

目的は、印象ではなく evidence を蓄積することです。

次へ進む条件: 同じ摩擦や違和感が境界の問題として見え始めたら `friction log` に進みます。

### friction log

局所的な不整合、境界摩擦、曖昧な ownership、繰り返しの不便を記録します。

この時点では、まだ lane を開くとは限りません。

次へ進む条件: blocked consumer、contract drift、ownership conflict などの trigger 候補が具体化したら `audit` に進みます。

### audit

新しい lane を開く根拠があるかを判定する、bounded な調査です。

audit の役割は最終設計を作ることではなく、進めるべきか止めるべきかを判断することです。

audit では、docs / code / tests / observability のどこに live な圧力があるかを分けて見ます。見た目の違和感だけでなく、観測面の drift や closeout claim との不整合があるかを確認します。

Outcome C が出ても、必要ならすぐ lane を開かず `gate transition` で readiness と owner を確認します。

次へ進む条件: `Outcome C` に相当する concrete な trigger が確認できた場合のみ `bounded lane` に進みます。

### bounded lane

影響範囲、非目標、closeout 条件を持った変更ラインです。

task より狭く、しかし単なる fix よりも明示的な契約を持ちます。

lane は「次にやるべき広いテーマ」ではなく、1 つの entry question に答える bounded first slice として開きます。steady state からの再開時も、過去の勢いだけで lane を開かず、現在の pressure に結びついた最小 slice を選びます。

必要なら、kickoff の直後に `execution brief` を置きます。これは kickoff を置き換えるものではなく、実装フェーズで worker が lane を広げないための判断ルール書です。

次へ進む条件: scope 内の変更と validation が揃ったら `closeout` に進みます。

### closeout

何が変わったか、何が変わっていないか、どこが ownership を持つか、何が deferred かを記録します。

closeout は必ずしもコード変更を意味しません。audit や bounded review の結果として「現状は honest な bounded defer である」と判断できた場合は、no-code closeout として閉じてよいです。

必要なら closeout 後に watch を付けます。これは lane を開いたままにすることではなく、closeout 済みの境界について regression や drift の再発を観測する短い補助運用です。

変更を段階的に有効化する必要がある場合は、closeout 前後で `rollout runbook` を使います。標準の考え方は `candidate -> default -> post-closeout watch` です。

次へ進む条件: reopen condition と resulting posture が明記できたら `steady state` に戻ります。

### steady state

現在の evidence では新しい lane を開く必要がない状態です。

これは停滞ではなく、正当化された repository posture です。

steady state では、必要に応じて少なくとも次を固定します。

- current bounded lane = unselected
- next bounded lane = unselected

「次に開きそうな領域」が頭にあっても、それは activation evidence ではありません。新しい blocked consumer、ownership gap、contract absence、observability drift が出るまでは、再開しないのが正しい posture です。

必要なら、steady state を保ったまま派生ドキュメントを作ってよいです。たとえば `phase kickoff packet`、`resume conditions audit`、`reentry preconditions` は、lane を開く前の posture 固定に使えます。

次に動く条件: 新しい evidence や blocked consumer があれば再び開始します。再入口は、構造理解が不足していれば `probe`、既存の friction log に trigger 候補が揃っていれば `audit` を選びます。

## このサイクルが必要な理由

- LLM は変更案を大量に生成できる
- 局所的に正しい変更が contract drift を起こしやすい
- reusable な意味や境界が偶発的に昇格しやすい
- 変更の closeout を書かないと、後続 worker が暗黙の前提で拡張してしまう
- 外部知見は、実装するか捨てるかの二択にすると探索能力を失う
- observability や trace の surface はコードより遅れて drift しやすく、live path の説明責任を壊しやすい
- steady state に戻したあとも、勢いだけで次 lane を選ぶと boundedness が崩れる
- 実装中に execution brief がないと、LLM worker が lane の内部で再設計を始めやすい
- rollout と rollback を固定しないと、default reading が曖昧なまま closeout されやすい
- anti-pattern が分散したままだと、別 worker や別セッションで同じ誤りが再発しやすい
- 文書ライフサイクル規則がないと、どれが現行 posture か失われやすい

## 最低限の運用ルール

- mechanics だけの変更は局所対応してよい
- meaning や ownership に触れる変更は audit を先に検討する
- 外部知見の取り込みは、即時実装を意味しない
- lane は 1 回に 1 本ずつ開く
- lane は「広いテーマ」ではなく、1 つの bounded first slice として開く
- lane を開いたら closeout 条件を先に書く
- 複数 worker や長い継続がある lane は gate transition で入口を固定する
- 実装フェーズで迷いやすい lane は execution brief を追加する
- candidate / default の読み分けがある変更は rollout runbook を追加する
- closeout は no-code defer でもよいが、ownership と reopen condition は省略しない
- docs / code / tests / observability のどこが trigger かを区別する
- diagnostics / self-check failure は friction / audit trigger になりうる
- steady state では `current bounded lane = unselected` を明示できる状態にする
- superseded 文書や current posture の更新点を放置しない
- closeout 後は steady state に戻す
