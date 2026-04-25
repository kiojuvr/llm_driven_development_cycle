# 用語集

## probe

捨てられる前提の探索。理解のための行為であり、契約変更そのものではありません。

## learning log

probe から得た観察結果を残すログ。印象ではなく、確認した事実と仮説を分けて記録します。

## friction log

局所的な摩擦や不整合を蓄積するログ。すぐに lane を開く根拠ではなく、audit 候補の材料です。

## research intake

外部の論文、記事、会話、他 repo 由来の知見を、いきなり実装 lane に入れずに受け止める前段プロセスです。

## concept digest

外部知見の core claim、relevance、分類、次の扱い方を要約した記録です。

## watchlist

まだ lane を開かないが、忘れず再考したい概念や trigger を置く熟成棚です。

`parking` との違いは、watchlist が lane 未開始の概念を熟成させる棚であるのに対し、parking は一度扱った事項を再開条件つきで閉じる記録である点です。

## audit

新しい lane を開くだけの concrete な trigger があるかを判断する bounded な調査です。

## evidence packet

audit の判断材料をまとめた証拠束です。blocked consumer、contract drift、ownership conflict などを明示します。

可能なら tests / diagnostics / observability の再現手順も含めます。

## bounded lane

影響範囲、非目標、validation、closeout 条件を持つ変更ラインです。単なる task よりも境界が明確です。

特に再開時は、広い phase 名ではなく、1 つの entry question に答える first bounded slice として表現します。

## blocked consumer

今その契約や変更がないと困る具体的な利用者、workflow、live path のことです。

## contract drift

局所的には正しそうな変更の積み重ねで、意味や境界が少しずつ崩れることです。

## ownership conflict

複数レイヤが同じ意味や責務を持っているように見える状態です。

## closeout

lane を閉じるための記録です。変更内容、非変更内容、ownership、deferred、reopen 条件を残します。

コード変更がない場合でも、bounded defer を固定する closeout は有効です。

## gate transition

audit Outcome C の後に、lane を開いてよい readiness、owner、shared posture update point を確認するプロセスです。

## execution brief

bounded lane の実装フェーズで、譲れない原則、禁止事項、順序付きタスク、曖昧時の判断ルールを固定する文書です。

## rollout runbook

変更を candidate / default / post-closeout watch のどこでどう有効化するか、rollback trigger をどう扱うかを固定する文書です。

## diagnostics / self-check evidence

diagnostics や self-check を evidence source として扱うときの結果です。audit trigger、rollout 判定、post-closeout watch の根拠になりえます。

## superseded document

現行版ではなくなった historical note 文書です。削除するのではなく、current document へのポインタを残します。

## shared posture update point

current bounded lane / next bounded lane / latest controlling doc を更新する正本の場所です。複数 worker で別々の場所を更新しないための固定点です。

## steady state

現在の evidence では新たな lane を開くべきではない、正当化された安定状態です。

必要に応じて `current bounded lane = unselected` や `next bounded lane = unselected` を明示し、lane 不在が判断済みの posture であることを示します。

## post-closeout watch

closeout 後に短期間の regression / drift 観測を行う補助運用です。lane を開いたままにすることではなく、steady state を維持しながら観測点だけを残すものです。

## parking

放置ではなく、再開条件を持って意図的に閉じることです。
