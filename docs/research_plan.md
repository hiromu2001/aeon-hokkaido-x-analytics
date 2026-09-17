# Research Plan

## 1. Study objective

イオン北海道株式会社の公式X公開投稿を対象に、投稿内容・表現・媒体・投稿条件と、likes / reposts / replies などのエンゲージメントの**関連**を統計分析・NLP・機械学習で検証する。

本研究は観察研究として開始し、因果推論ではなく、まず以下を明確に区別する。

- 記述：どの投稿がどれだけ反応されたか
- 関連：どの特徴と反応が統計的に結びついているか
- 予測：投稿前特徴から将来反応をどこまで予測できるか
- 因果：特徴を変えれば反応が変わるか（本研究単独では原則主張しない）

## 2. Closest baseline study

Tanaka & Huang (2024) は、日本のSHARP公式Twitterの500投稿を対象に、画像/動画、リンク、CTA、質問、brand account personality、informative / entertaining / promotional content、曜日、文字数等をコード化し、likes / retweets / repliesの関係を分析している。

この研究を日本企業X研究の主要ベースラインとする。

本研究ではそこに以下を追加する。

- 小売業特有の販促・価格・商品カテゴリ
- 北海道・道産・地域名を用いたlocality特徴
- Sentence Embedding / Topic Modeling
- Gradient Boosting + SHAP
- 時系列holdout
- キャンペーン投稿除外の感度分析

## 3. Research questions

### RQ1 — Content
どのコンテンツタイプがlikes / reposts / repliesと関連するか。

候補カテゴリ：
- 商品情報
- 価格・セール・特売
- キャンペーン / プレゼント
- 季節・催事
- 店舗・地域イベント
- 北海道・道産・地域性
- 企業活動 / CSR
- 娯楽・雑談的投稿

### RQ2 — Expression
文章長、質問、CTA、絵文字、ハッシュタグ、URL、価格表記、感情表現、くだけた表現などは反応とどう関連するか。

### RQ3 — Media
テキストのみ / 画像 / 動画 / GIFで反応は異なるか。

### RQ4 — Locality
北海道・道産・地域名を含む投稿は反応と関連するか。

### RQ5 — Time
曜日、時間帯、月、季節、年中行事などによって投稿テーマと反応の関係は変わるか。

### RQ6 — Prediction
投稿前に利用可能な特徴だけで将来のエンゲージメントをどこまで予測できるか。

## 4. Data collection

### Pilot
約500投稿。

### Main analysis
1,000〜3,200投稿を目安とする。

### Candidate fields
- post_id
- created_at
- text
- like_count
- repost_count / retweet_count
- reply_count
- quote_count
- media type
- URL / hashtag / mention
- referenced post type

Primary analysisでは原則、公式アカウントが作成した**オリジナル投稿**を対象とする。reply / repostは別分析または除外とする。

## 5. Feature engineering

### Mechanical features
- text_length
- hashtag_count
- mention_count
- emoji_count
- has_url
- has_question
- has_price_expression
- media_type
- weekday
- hour
- month
- season

### Literature-based features
- informative
- entertaining
- promotional
- remunerative
- CTA
- question
- vividness
- interactivity
- humanized tone / brand account personality

### Aeon Hokkaido specific features
- local_score
- store_specific
- price_promotion
- product_category
- seasonal_event
- corporate_CSR

### NLP features
- sentence embedding
- sentiment / emotion
- linguistic style
- topic clusters

主要カテゴリを自動分類する場合、人手コーディングしたサンプルで精度を確認する。人手分類そのものを主分析に用いる場合は、二重コーディングとCohen's kappa等で一致度を確認する。

## 6. Exploratory data analysis

- 投稿数の時系列
- likes / reposts / replies / quotes の分布
- 平均 / 中央値 / 分散
- 外れ値確認
- カテゴリ別分布
- media別分布
- 曜日 / 時間帯別分布
- topicの時間推移
- campaign投稿と通常投稿の比較

## 7. Statistical modeling

エンゲージメントは非負整数かつ右裾が長くなることが予想されるため、OLSを主分析にしない。

候補：
- Poisson regression
- Negative Binomial regression
- zero-inflated / hurdle model（ゼロ過剰が明確な場合）

過分散を診断してモデル選択を行う。

例：

```text
log(E[likes_i])
  = β0
  + β1 image
  + β2 video
  + β3 CTA
  + β4 entertaining
  + β5 promotion
  + β6 local_score
  + controls
```

Control候補：
- 曜日・時刻
- 月 / 季節
- 文字数
- 長期トレンド
- 投稿時点フォロワー数（履歴が入手できる場合）

係数は必要に応じて `IRR = exp(β)` で解釈する。

## 8. Sensitivity analysis

キャンペーンや懸賞投稿は反応を大きく押し上げる可能性があるため、最低でも以下を比較する。

1. 全投稿
2. キャンペーン・懸賞除外

加えて、極端なバズ投稿を除外したrobustness checkも検討する。

## 9. NLP

### Embedding
投稿本文をsentence embeddingに変換し、意味的な近さを数値化する。

### Topic modeling
BERTopic等を用いて投稿テーマを探索的に抽出する。

Topicは「真のカテゴリ」とみなさず、探索と特徴生成に用いる。

### Sentiment / emotion
Twitter/X特有の短文や絵文字・くだけた表現に対応したモデルを優先し、一般文章向けモデルを無検証で使用しない。

## 10. Machine learning

目的は説明ではなく、**未来投稿のエンゲージメント予測性能**を測ること。

候補：
- GLM / Elastic Net baseline
- LightGBM
- CatBoost
- text embedding + gradient boosting
- 将来的に画像特徴を加えたmultimodal model

### Validation
ランダムsplitだけではなく、時間順holdoutを基本とする。

例：
- train: 古い70%
- validation: 次の15%
- test: 最新15%

### Metrics
- MAE
- RMSE（必要に応じlog1p target）
- Poisson deviance
- Spearman rank correlation

### Interpretation
SHAPは「モデルが予測に使った特徴」の説明に用いる。SHAP値を因果効果として解釈しない。

## 11. Internal analytics extension

公開データだけでは、投稿ごとのimpressionsやlink clicksが得られない場合がある。

社内Analyticsを利用できる場合は以下へ拡張できる。

- impressions
- engagements
- engagement rate
- link clicks
- CTR
- video views

impressionsを利用できれば、単純なlikes件数だけより露出量を考慮した分析が可能になる。

ただし非公開データはpublic GitHubへ一切配置しない。

## 12. Causal interpretation

観察データのみから、たとえば

`動画投稿にしたからエンゲージメントが増えた`

とは原則結論しない。

投稿テーマ、販促規模、季節、担当者判断、広告配信、フォロワー構成などが交絡し得るため、結論は基本的に

- 「〜と関連した」
- 「〜が予測に寄与した」

までとする。

将来、投稿形式をランダム化できるA/Bテストや自然実験が可能なら因果分析へ拡張する。

## 13. Ethics and data governance

- 企業公式アカウントの公開投稿を主対象とする。
- 一般ユーザーの返信本文はPrimary analysisでは原則収集しない。
- raw API responseはGitHubへ公開しない。
- API token・cookie・社内Analytics・非公開数値をcommitしない。
- X Developer Agreement / Policy / display requirementsを実装時点で再確認する。
- 公開投稿であっても、研究利用に対するユーザー認識や文脈依存の倫理問題があるため、一般ユーザーコンテンツを追加分析する場合は別途検討する。

## 14. Roadmap

- [ ] Phase 0: X API・料金・規約確認
- [ ] Phase 1: 500投稿のpilot collection
- [ ] Phase 2: EDA
- [ ] Phase 3: coding scheme確定
- [ ] Phase 4: 人手分類の一致度確認
- [ ] Phase 5: Poisson / Negative Binomial比較
- [ ] Phase 6: likes / reposts / replies別に分析
- [ ] Phase 7: Embedding / Topic / sentiment追加
- [ ] Phase 8: LightGBM / CatBoost + time split
- [ ] Phase 9: SHAP・感度分析
- [ ] Phase 10: 社内Analyticsが使える場合はCTR等へ拡張
- [ ] Phase 11: 最終レポート / dashboard
