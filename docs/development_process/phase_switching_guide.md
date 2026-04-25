# フェーズ切り替えガイド

## 目的

この文書は、いま必要なのが probe なのか、audit なのか、bounded lane なのかを判定する基準をまとめたものです。

外部の論文、記事、会話、他 repo 由来の概念を扱う場合は、まず `research_intake.md` を通し、そこから `probe`、`audit`、`bounded lane` に接続するかを決めます。

## 序盤

序盤は、構造理解と live path の把握を優先します。

この段階で主に行うもの:

- probe
- learning log
- friction log

序盤の特徴:

- ownership がまだ見えていない
- 用語が安定していない
- 問題が「不快感」なのか「実害」なのか分離できていない

序盤で避けること:

- 広い再設計
- reusable contract の導入
- aesthetic なリファクタ

## 中盤

中盤は、観察から判断へ移る段階です。

この段階で主に行うもの:

- workflow audit
- evidence packet
- bounded lane kickoff

中盤へ移る目安:

- 同じ摩擦が複数回観察されている
- blocked consumer が具体化している
- docs / code / tests の contract drift が見えている
- observability / trace / health signal の drift が live path 説明を壊している
- ownership conflict が live path で確認できる

## 終盤

終盤は、bounded lane を閉じて steady state に戻す段階です。

この段階で主に行うもの:

- 実装の収束
- closeout
- parking
- reopen condition の明記

終盤で確認すること:

- 変更範囲が lane の境界を超えていないか
- ownership が明文化されているか
- deferred 項目が future work ではなく parking として扱われているか
- no-code closeout でも reopen condition と current posture が書かれているか
- post-closeout watch が必要なら、lane 継続ではなく補助観測として分離されているか

## steady state からの再開

steady state に戻ったあと、次の lane は自動では選ばれません。

再開前に少なくとも次を確認します。

- `current bounded lane = unselected` を正直に言えるか
- 前回 closeout の claim がまだ有効か
- 新しい trigger は historical momentum ではなく current repository pressure に基づくか
- 開くとしても broad phase ではなく first bounded slice に落ちているか

## 簡易判定

次の問いで判定します。

### まだ構造理解が不足しているか

不足しているなら `probe` に留まります。

### 具体的な blocked consumer があるか

あるなら `audit` または `bounded lane` を検討します。

### その pressure は docs / code / tests / observability のどこに出ているか

場所を分けて言えないなら、まだ `probe` または `audit` の材料整理が足りません。

### 外部知見を直接実装したくなっていないか

なっているなら、まず `research intake` で digest、分類、再考 trigger を書きます。

### 問題は reusable な意味や ownership に触れているか

触れているなら `audit` を先に行います。

### 単なる局所修正で正直に閉じられるか

閉じられるなら lane を開かずに対応します。

### 前回 closeout 済みの領域を、勢いだけで再開しようとしていないか

そうなら、lane ではなく steady state を維持します。再開には fresh trigger が必要です。
