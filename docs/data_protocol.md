# データ収集・品質仕様 v1

未実装の収集仕様。APIへの課金・実データの取得はまだ行っていない。

## 収集前の確認

企業公式サイトから対象Xアカウントを照合し、usernameだけでなく不変のuser_idと根拠URL・確認日を記録する。アカウント名はこの設計段階で推測入力しない。

[R17の公式資料](references.md)をもとに取得経路、権限、料金、取得できる期間、pagination、削除対応、公開条件を確認する。実アカウントのAPI応答でpublic_metrics、media、referenced_tweets、編集情報の可用性を検証。APIの一般仕様を、本人の契約で取得できる保証としない。

## 保存単位

投稿テーブルとスナップショットテーブルを分ける。更新取得で前回の値を上書きしない。時刻はタイムゾーン付きUTC、曜日・投稿時刻特徴はAsia/Tokyoへ変換。整数IDは文字列で保持する。

| テーブル | 最低限のフィールド | 注意 |
|---|---|---|
| posts | post_id, author_id, created_at, first_seen_at, reference_type | 自己返信もreply扱い。APIの参照型で分類 |
| posts_private | text, media references, edit history | 公開リポジトリに置かない |
| snapshots | post_id, collected_at, like_count, repost_count, reply_count, quote_count | 一意キーはpost_id＋collected_at |
| snapshots | impression_count, metric_source, fetch_status, missing_reason | 未提供を0にしない。public/organic/promotedを混ぜない |
| annotation | post_id, codebook_version, coder_id, labels, source_modality | 人手原値と合議値を分離 |
| accounts | author_id, followers_count, observed_at | 投稿以前に観測された履歴だけを予測に利用 |
| manifest | run_id, endpoint, query, started_at, ended_at, page_count, errors | tokenを記録しない。pagination未完了を明記 |

取れない投稿も予定取得台帳に残し、成功行だけから取得率を計算しない。投稿の発見段階で落ちたものは総数不明となり得るため、観測可能な取得成功率と全投稿の網羅率を区別する。

## 固定窓ラベルの作成

- elapsed_hours = (collected_at - created_at)の時間差。
- 主窓は168 <= elapsed_hours <= 174。この範囲の最初の成功スナップショットを選び、選択時刻を保存。
- その窓にない投稿の7日ラベルは欠測。近い時点の代入、24時間値からの外挿、現在値の流用はしない。
- 24〜30時間、720〜726時間は別テーブル/ラベル列。繰返し観測を独立投稿として数えない。
- 取得失敗、削除、権限制限、値未提供を区別。反応数減少も起こり得るため、単調増加を強制補正しない。

## 重複・編集・投稿種別

同一IDのAPI重複だけを統合し、同文でも別IDなら直ちに削除しない。近重複はtemplate_groupとして検証漏洩の確認に使う。編集履歴の複数IDは同じ投稿系列に束ね、最初の公開時刻と使用した版を明記する。版ごとの反応定義が確認できなければ主分析から除外し件数を報告する。

主分析はoriginal。reply/repost/quote/mixedは別に保持する。引用の追加評価では元投稿由来の反応・話題性を限界として記す。

## 実装時に失敗させる検証

- ID・authorの不整合、タイムゾーンなし、収集時刻が投稿より前。
- 負数・小数の反応数、不明値を0として取り込んだ列。
- 同じ投稿に複数の主窓ラベル、許容窓外の採用。
- 主分析集合にreply/repost/quoteまたは未判定の懸賞ラベルが混入。
- 訓練ラベルの取得完了が検証の予測時刻より後。

報告項目：取得期間、投稿発見経路、日/月別件数、成功率、欠測理由、除外理由、各窓の実経過時間、地域性/懸賞/媒体別の欠測率。失敗した期間を黙って落とさない。

## 公開と再現性

raw、本文、画像、非公開Analytics、認証情報、個人の識別情報は公開しない。投稿ID・派生特徴・埋め込みも再識別/再配布を確認する。原データを共有できなくても、取得仕様、合成テストデータ、処理コード、集約表、環境固定ファイル、seed、コミットIDで追試可能性を高める。

公開用ファイルは許可リストで選ぶ。.gitignoreだけを安全性の根拠にしない。削除・利用停止要求と契約上の保持条件に対応できる台帳をローカルで維持する。
