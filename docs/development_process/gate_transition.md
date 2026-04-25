# Gate Transition

## 目的

この文書は、audit Outcome C から bounded lane 開始までの間に、何が揃っていれば lane を開いてよいかを定義します。

audit が positive でも、常にその場で lane を開いてよいわけではありません。特に複数 worker や長いセッション継続がある場合、readiness、owner、開始手順を固定しないと lane の入口が曖昧になります。

## いつ使うか

次のいずれかに当てはまるなら gate transition を推奨します。

- audit Outcome C が出た
- 複数 worker が lane 開始に関わる
- 実装前に docs / operator / rollout の準備を確認したい
- kickoff を書く前に owner と readiness を固定したい

## gate で確認するもの

- trigger evidence はまだ有効か
- first bounded slice は 1 問に絞れているか
- affected owner は明示されているか
- kickoff, execution brief, rollout dependency の要否が見えているか
- 同時に複数 lane を開いていないか
- current bounded lane / next bounded lane の更新先が明確か

## readiness の見方

最低限、次の 3 面を見ます。

- docs readiness
- operator readiness
- implementation readiness

すべて満点である必要はありませんが、どこが未準備かを明記せずに lane を開くべきではありません。

## decision worksheet

gate では少なくとも次を決めます。

- gate owner
- lane owner
- kickoff を書く日付または条件
- pass / hold の判定
- hold の場合の次アクション

## Do Not Do

- gate を broad planning meeting にしない
- new evidence なしに phase を開かない
- owner 不在のまま kickoff しない
- Outcome C を理由に複数 lane を同時開始しない

## completion gate

lane を開いてよいのは、少なくとも次が yes のときです。

- concrete trigger is still live
- first bounded slice is named
- kickoff writer is known
- shared posture update point is known
- anti-pattern に該当していない
