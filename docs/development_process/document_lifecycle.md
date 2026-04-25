# Document Lifecycle

## 目的

この文書は、development-process docs の命名、版管理、superseded 扱い、履歴保持、INDEX 導入基準を定義します。

文書が増えると、内容そのものより「どれが現行か」「どう辿るか」が実運用のボトルネックになります。ここでは探索性と再開性を守る最小ルールを定義します。

## 履歴保持の原則

実運用で作成した運用文書は、原則として削除しません。

履歴を残す理由:

- 当時どの evidence で判断したかを再構成できる
- closeout や steady state がどう成立したかを追跡できる
- 別 worker / 別セッションが途中経過を再利用できる
- historical momentum と fresh trigger を区別しやすくなる

したがって、不要になった文書を消すのではなく、現行ではないことを明記して残します。

## 命名

実運用文書では、必要に応じて日付サフィックスを付けます。

推奨形:

- `<topic>_YYYY_MM_DD.md`
- `<topic>_closeout_YYYY_MM_DD.md`
- `<topic>_audit_YYYY_MM_DD.md`

テンプレートや汎用 docs には日付を付けません。

## predecessor / successor

版が進む文書や closeout family では、必要なら次を明記します。

- predecessor: 直前に読むべき文書
- successor: 現行版または後続判断

これは厳密な必須項目ではありませんが、同名系統が増えたら推奨します。

## superseded 文書

文書が superseded になったら、先頭に短い historical note を置きます。

最低限書くもの:

- この文書は historical note であること
- 現行版へのポインタ
- なぜ superseded になったかの 1 行説明

superseded 文書を削除するのではなく、現行版へ辿れるように残します。

## closeout による凍結

closeout は「変更が完了した」だけでなく、「この読み方を current posture として凍結した」ことを意味します。

したがって:

- closeout 済みの文書群は historical momentum だけで reopen しない
- reopen には fresh trigger か resume-conditions audit が必要

## INDEX 導入基準

文書数が増えたら `INDEX.md` を導入します。

推奨の目安:

- 運用文書が 20 件前後を超えた
- 同一 family の closeout / audit / runbook が複数ある
- 別セッションの worker が docs から再開する頻度が高い

`INDEX.md` には少なくとも次を載せます。

- 時系列順または family ごとの一覧
- 各文書の 1 行説明
- current state を知るために先に読むべき文書

`INDEX.md` は履歴を圧縮して消すためのものではなく、削除しない履歴を辿りやすくするためのものです。

## shared posture の更新点

複数 worker や複数セッションで作業する場合、current posture の更新場所を決めます。

候補:

- current-state snapshot
- latest closeout
- phase kickoff packet
- gate transition runbook

重要なのは、毎回違う場所に current bounded lane を書かないことです。
