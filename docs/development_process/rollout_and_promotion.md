# Rollout And Promotion

## 目的

この文書は、bounded lane の成果をどう段階的に有効化し、どう rollback し、どの時点で closeout と steady state に戻すかを定義します。

LLM駆動開発では、実装完了だけでは変更が固定されたとは言えません。candidate として入った変更が、default に昇格してよいか、post-closeout watch で regression がないかを別に確認する必要があります。

## 基本原則

- rollout は closeout の代替ではない
- closeout は rollout の代替でもない
- 変更を有効化する前に rollback trigger を先に書く
- smoke session や diagnostics を evidence として残す
- candidate のまま放置しない
- default 昇格後も必要なら短い watch を行う

## 基本ステージ

標準の段階は次のとおりです。

`candidate -> default -> post-closeout watch`

必要がない場合は一部を省略してよいですが、省略理由は runbook に書きます。

## candidate

変更は存在するが、まだ default ではない段階です。

この段階で固定するもの:

- どの config / docs / operator surface が candidate か
- smoke session の query set や確認手順
- diagnostics / self-check の再実行手順
- rollback trigger

## default

通常の読み方、通常の config、通常の docs として扱ってよい段階です。

default に上げてよい条件:

- candidate 段階の smoke session が通っている
- diagnostics / tests / observability に improper regression がない
- config-driven feature flag がある場合、default reading が明確
- rollback trigger が依然として有効

## post-closeout watch

default 昇格または no-code closeout の直後に、短期間の regression / drift を見る補助観測です。

これは lane 継続ではありません。steady state を保ったまま、観測だけを残します。

## diagnostics との接続

diagnostics や self-check は audit と rollout の両方で evidence source になります。

少なくとも次を区別して書きます。

- baseline としての diagnostic pass / fail
- candidate 適用後の再実行結果
- post-closeout watch での再確認結果
- 失敗した場合に friction log / audit へ戻す条件

diagnostic failure が次を満たすなら、watch や local patch ではなく audit trigger として扱います。

- live path の correctness に影響する
- explainability / observability を壊す
- closeout claim と矛盾する
- rollback trigger を満たす

## closeout との関係

closeout では、少なくとも次を明示します。

- rollout が不要か、必要か
- candidate / default のどこで閉じるか
- post-closeout watch が必要か
- config / operator reading の実務上の読み方
- rollback trigger

## no-code closeout の場合

コード変更がなくても rollout 的な読み分けが必要なことがあります。

たとえば:

- 現在の reduced compatibility surface を intentional と固定する
- docs 上の canonical reading と実装上の bounded compatibility reading を分ける
- 将来の worker が「不足」と誤認して広げないようにする

この場合も、何を default reading とし、何が reopen trigger かを closeout に書きます。
