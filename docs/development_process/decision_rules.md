# 判断ルール

## lane を開いてよい条件

次のいずれかが concrete なら、bounded lane を検討します。

- blocked consumer が存在する
- contract drift が live path で確認できる
- ownership conflict が確認できる
- duplicated semantics が複数箇所にある
- improper regression がある
- correctness または explainability への影響がある
- 外部知見が既存 repo の blocked consumer、drift、ownership conflict に接続できる

## lane を開かない条件

次の理由だけでは lane を開きません。

- 設計の見た目がよくなる
- 将来たぶん必要になりそう
- LLM が広い再設計を提案した
- docs 上の違和感はあるが live path の圧力がない
- 局所パッチで正直に閉じられる
- 面白い研究だが current repo への接続が曖昧
- 成功条件が「賢くなりそう」しかない

## audit の allowed outcomes

- `Outcome A`: 新しい lane は不要。局所対応または watch 継続
- `Outcome B`: 圧力はあるが trigger は未成熟。evidence を追加して継続観察
- `Outcome C`: concrete な trigger がある。1 本の bounded lane を開く

## 実務上の短いルール

- meaning に触れるなら、まず audit を考える
- ownership が変わるなら、lane を開く
- reusable contract を追加するなら、lane を開く
- blocked consumer がないなら、parking を優先する
- 外部知見は、digest / watch / probe / audit を経てから lane に昇格させる
- audit の negative result も進捗として扱う
