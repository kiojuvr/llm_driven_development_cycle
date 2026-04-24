# LLM駆動開発サイクル

## 概要

LLM駆動開発では、コードを書く速度よりも、どの変更を開くかを判断する速度と精度が重要になります。

この文書は、変更圧力を統治するための基本サイクルを定義します。

## 基本サイクル

標準サイクルは次のとおりです。

`probe -> learning log -> friction log -> audit -> bounded lane -> closeout -> steady state`

## 各フェーズ

### probe

捨ててもよい探索です。未知の構造、責務、実コードの流れを調べます。

この段階では、設計の昇格や広いリファクタはまだ正当化されていません。

### learning log

probe で得た事実、観察、暫定仮説を記録します。

目的は、印象ではなく evidence を蓄積することです。

### friction log

局所的な不整合、境界摩擦、曖昧な ownership、繰り返しの不便を記録します。

この時点では、まだ lane を開くとは限りません。

### audit

新しい lane を開く根拠があるかを判定する、bounded な調査です。

audit の役割は最終設計を作ることではなく、進めるべきか止めるべきかを判断することです。

### bounded lane

影響範囲、非目標、closeout 条件を持った変更ラインです。

task より狭く、しかし単なる fix よりも明示的な契約を持ちます。

### closeout

何が変わったか、何が変わっていないか、どこが ownership を持つか、何が deferred かを記録します。

### steady state

現在の evidence では新しい lane を開く必要がない状態です。

これは停滞ではなく、正当化された repository posture です。

## このサイクルが必要な理由

- LLM は変更案を大量に生成できる
- 局所的に正しい変更が contract drift を起こしやすい
- reusable な意味や境界が偶発的に昇格しやすい
- 変更の closeout を書かないと、後続 worker が暗黙の前提で拡張してしまう

## 最低限の運用ルール

- mechanics だけの変更は局所対応してよい
- meaning や ownership に触れる変更は audit を先に検討する
- lane は 1 回に 1 本ずつ開く
- lane を開いたら closeout 条件を先に書く
- closeout 後は steady state に戻す
