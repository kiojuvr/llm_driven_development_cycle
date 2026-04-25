# Anti-Patterns

## 目的

この文書は、LLM駆動開発で繰り返し起こりやすい premature escalation、historical momentum、boundedness の崩壊を防ぐための anti-pattern 集です。

個別ルールは `decision_rules.md` や `phase_switching_guide.md` にも書かれていますが、ここでは worker handoff や review 時に参照しやすいよう 1 か所に集約します。

## 開始時の anti-pattern

- slot があるから lane を開く
- 前回の lane が閉じた勢いで次の lane を選ぶ
- broad phase 名だけで first bounded slice を書かない
- phase 候補を lane と取り違える
- blocked consumer がないのに reusable contract を先に作る

## audit 時の anti-pattern

- evidence より先に設計案を固める
- docs 上の違和感だけで live path を見ない
- diagnostics failure を全部 audit trigger 扱いする
- Outcome A/B を失敗と見なす
- closeout claim と current code/test/observability の照合を省く

## 実装時の anti-pattern

- kickoff だけで実装を始め、execution brief を書かない
- first PR に unrelated cleanup や lifecycle automation を混ぜる
- local convenience を reusable boundary に昇格させる
- 曖昧な scope 追加を audit に戻さず、そのまま吸収する
- broad redesign が見えたときに current lane を広げて対応する

## rollout / closeout 時の anti-pattern

- rollout trigger より先に default 扱いする
- rollback trigger を書かずに candidate を有効化する
- no-code closeout を「何もしないこと」と誤認する
- post-closeout watch が必要なのに closeout だけで終える
- closeout 後に current / next bounded lane を unselected に戻さない

## 文書運用の anti-pattern

- 文書名の時系列情報を省いて探索性を落とす
- superseded 文書を放置して現行版を指さない
- worker ごとに posture の記述を変えて current state を壊す
- INDEX が必要な規模なのに README だけで運用し続ける

## worker 協調の anti-pattern

- 複数 worker が同じ lane を別 posture で進める
- shared posture の更新場所を決めない
- concurrent probe と audit の write scope を分けない
- 別セッションへ引き継ぐときに current bounded lane を省略する

## 実務上の使い方

- lane kickoff の review で 1 回読む
- worker handoff に `Do not` として必要項目を抜き出す
- closeout review で anti-pattern に該当していないか逆照合する
