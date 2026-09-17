# aeon-hokkaido-x-analytics

イオン北海道株式会社の公式X公開投稿を対象に、**統計分析・自然言語処理（NLP）・機械学習**を用いて、投稿内容とエンゲージメントの関係を分析する個人研究プロジェクトです。

> **Disclaimer**  
> 本リポジトリは個人による研究・学習目的のプロジェクトであり、イオン北海道株式会社およびX Corp.の公式プロジェクトではありません。

## Research goal

単純な「バズった投稿ランキング」ではなく、先行研究に基づいて次を検証します。

- 投稿内容・表現・画像/動画・投稿時刻と反応の関係
- いいね / リポスト / 返信を分けたカウントデータ分析
- 北海道・道産・地域名などの**地域性**と反応の関係
- Sentence Embedding / Topic Modelingによる投稿内容の定量化
- LightGBM / CatBoost等によるエンゲージメント予測
- SHAPによる予測モデルの解釈
- 季節・曜日・時間帯を含む時系列的な変化

## Research design

```text
X API
  ↓
Raw posts（ローカル保存・Git管理外）
  ↓
Cleaning / Feature engineering
  ├─ text length / hashtag / URL / emoji
  ├─ media type
  ├─ CTA / question / promotion
  ├─ local_score
  └─ season / weekday / hour
  ↓
EDA
  ↓
Statistical modeling
  ├─ Poisson regression
  └─ Negative Binomial regression
  ↓
NLP
  ├─ Sentence Embedding
  ├─ Topic Modeling
  └─ sentiment / emotion
  ↓
Machine Learning
  ├─ LightGBM / CatBoost
  └─ SHAP
  ↓
Time-based validation / Sensitivity analysis
  ↓
Report
```

## Key research questions

1. どの投稿カテゴリが likes / reposts / replies と関連するか。
2. 画像・動画・CTA・質問・価格表現・文章長などは反応とどう関連するか。
3. 「北海道」「道産」「札幌」「旭川」「函館」「十勝」「オホーツク」等の地域性は反応と関連するか。
4. 季節・曜日・時間帯によって投稿テーマと反応の関係は変わるか。
5. 投稿前に利用できる情報だけで、将来のエンゲージメントをどこまで予測できるか。

## Planned sample

- Pilot: 約500投稿
- Main analysis: 1,000〜3,200投稿を目安

最初は小規模に取得して分析設計を確認し、必要に応じて拡張します。

## Important methodological rules

- likes / reposts / replies は原則として**別々の目的変数**として扱う。
- カウントデータの過分散を確認し、Poissonを決め打ちせずNegative Binomialも比較する。
- キャンペーン・懸賞投稿を含む分析と除外した分析を両方行う。
- 機械学習ではランダム分割だけでなく**時間順holdout**を用いる。
- SHAPの結果を因果効果として解釈しない。
- 観察データからは原則として「関連」「予測寄与」までを結論とする。

## Repository structure

```text
.
├── README.md
├── docs/
│   ├── research_plan.md
│   └── references.md
├── data/              # raw dataはGit管理しない
├── notebooks/         # future
├── src/               # future
└── outputs/           # future
```

## Literature baseline

日本の企業X分析に近い先行研究として、Tanaka & Huang (2024) がSHARP公式Twitterの500投稿を対象に、画像/動画、リンク、CTA、質問、投稿内容、曜日、文字数等とlikes / retweets / repliesの関係を分析しています。本研究ではこれを主要なベースラインの一つとし、小売・北海道地域性・NLP/MLを追加します。

詳細は [`docs/research_plan.md`](docs/research_plan.md) と [`docs/references.md`](docs/references.md) を参照してください。

## Data / ethics

- 主対象は企業公式アカウントの公開投稿。
- 一般ユーザーの返信本文はPrimary analysisでは原則収集しない。
- API tokenや社内Analyticsなどの非公開情報は絶対にcommitしない。
- X APIのDeveloper Agreement / Policy / display requirementsを実装時に再確認する。
- raw APIレスポンスはGitHubへ公開せず、必要な派生特徴・集約結果を中心に管理する。

## Status

**Planning / Literature review**

実装は未着手。先行研究レビューと研究設計を先に固める。