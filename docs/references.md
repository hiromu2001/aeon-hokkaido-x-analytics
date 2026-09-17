# 先行研究レビューと参考文献

確認日：2026-09-17。16件の研究・方法論資料とX公式資料を整理した焦点化レビュー。体系的レビューではない。書誌・要旨のみの確認と本文確認を区別する。以下の「採用」「限界」は本研究側の判断であり、原著の結論と区別する。

## 研究の位置付け

日本企業Xの基準はR01、食品小売の地域性の基準はR02とする。既に小売の地域性研究があるため、機械学習を加えただけで新規性を主張しない。地域のどの手がかりを測り、どの参加誘因を除き、どの時間幅で反応を比べたのかを再現可能にすることに研究の価値を置く。

| ID | 文献 | 確認範囲 | 本研究に直接使う点 | 適用上の限界 |
|---|---|---|---|---|
| R01 | Tanaka & Huang (2024) | 本文、特に§3〜4・表5/11 | 日本語企業投稿の内容分類、反応別分析 | 単一電機企業、モデル記述の整合性は要注意 |
| R02 | Numan et al. (2026) | 出版社要旨・大学書誌 | 店舗具体性と地域性の区別 | Facebook・複数店舗。詳細推定仕様は未確認 |
| R03 | de Vries et al. (2012) | 大学書誌・要旨 | いいねとコメントを別の指標として扱う | 旧Facebook、投稿後コメントは予測特徴にしない |
| R04 | Pletikosa Cvijikj & Michahelles (2013) | 本文、特に方法節 | 食品/飲料、内容・媒体・投稿時期、過分散 | 現在の日本Xへの係数移植はできない |
| R05 | Lee et al. (2018) | 大学書誌・著者版要旨 | 内容分類と配信選択の問題 | Facebook、著者版と最終版の差は未照合 |
| R06 | Eichinger et al. (2022) | 本文の概念・実験・考察 | 場所・人・過去という理論的整理 | 投稿特徴から受け手の心理を測ったとはいえない |
| R07 | 長尾ほか (2025) | 本文 | 国内の地域・X・日本語感情分析 | 住民等の投稿と企業発信は別の対象 |
| R08 | Ballerini et al. (2023) | 大学書誌・要旨 | スーパーの社会的話題・時期の重要性 | パンデミック期、媒介を因果としない |
| R09 | Coxe et al. (2009) | 著者書誌・論文要旨 | 生の非負整数カウントとGLM | 本研究固有の依存・選択は別途対処 |
| R10 | Kajiwara et al. (2021) | ACL書誌・要旨 | 日本語SNS、書き手と読み手の感情差 | 小売販促文での精度は保証しない |
| R11 | Barbieri et al. (2020) | ACL書誌・要旨 | Twitter分類ベンチマーク | 日本語感情モデルの根拠にはならない |
| R12 | Grootendorst (2022) | arXiv要旨 | 探索的なトピック生成候補 | プレプリント、カテゴリの正解ではない |
| R13 | Lundberg & Lee (2017) | 会議原稿の導入・要旨 | モデル予測の説明 | 因果効果の推定法ではない |
| R14 | Roberts et al. (2017) | 大学書誌・著者版要旨 | 時間・群構造を保つ検証 | 生態学的方法論、7日gapの直接根拠ではない |
| R15 | Fiesler & Proferes (2018) | 出版社要旨 | 公開データ研究の文脈依存性 | 具体的な再配布条件は別途確認 |
| R16 | Borrero (2023) | 出版社本文の対象・方法・結論 | 食品小売Twitterという隣接研究 | 本研究の固定窓・地域性仮説の直接検証ではない |

## R01 — 日本企業Twitter：基準と批判的検討

Tanaka, Y., & Huang, L. (2024). **Enhancing social media engagement in Japan: An empirical study of design and content factors on brand account.** *International Journal of Marketing & Distribution, 27*(1–2), 53–72. [DOI](https://doi.org/10.5844/jsmd.27.1-2_53) / [本文](https://www.jstage.jst.go.jp/article/jsmd/27/1-2/27_53/_pdf)

SHARPの2021年5〜8月の500投稿を分析。元データは担当者提供のDashboard由来であり、公開APIだけの本研究とは取得条件が違う。本文§3.1では報酬型投稿がなく該当仮説を撤回しているため、懸賞効果の実証根拠にはできない。

§3.4はPoissonと記す一方、目的変数の対数変換、表11のF値/R²、対数化後の欠測除外が記される。これだけで実際の推定処理を断定できないが、通常の生カウントPoisson GLMとして再現するには確認が必要。本研究は内容変数を参考にし、ゼロを保持するNB2/Poissonを明示する。動画7件・質問9件という希少性にも注意し、当該方向を普遍的仮説にしない。

## R02 — 最も近い食品小売・地域性研究

Numan, N. N., Wielheesen, T. J. P., Sloot, L. M., Bijmolt, T. H. A., & van Nierop, E. (2026). **Hooking Customers with Facebook: An Empirical Analysis of Grocery Stores’ Online Engagement.** *Journal of Interactive Marketing, 61*(1), 60–78. オンライン先行公開2025-04-17、巻号2026-02。[DOI/出版社](https://doi.org/10.1177/10949968251337700) / [大学書誌](https://research.rug.nl/en/publications/hooking-customers-with-facebook-an-empirical-analysis-of-grocery-/)

135店舗・2,700投稿。要旨では店舗固有の内容や店舗による発信と反応の関係を報告する。したがって「地域性を初めて扱う」という主張は避ける。単一アカウントの本研究では発信主体の違いを識別できないため、内容の具体性を分けて測る。出版社PDFリンクは要旨ページに転送されたため、詳細な回帰式・効果量・統制変数を確認済みとはしない。

## R03 — 投稿人気の基礎

De Vries, L., Gensler, S., & Leeflang, P. S. H. (2012). **Popularity of Brand Posts on Brand Fan Pages: An Investigation of the Effects of Social Media Marketing.** *Journal of Interactive Marketing, 26*(2), 83–91. [DOI](https://doi.org/10.1016/j.intmar.2012.01.003) / [大学書誌・要旨](https://research.rug.nl/en/publications/popularity-of-brand-posts-on-brand-fan-pages-an-investigation-of-/)

11ブランド・355投稿で、いいねとコメントには異なる関連要因があることを報告。反応の単純合算を主指標にしない根拠にする。投稿後に生じたコメント内容を投稿前の予測特徴に入れない。

## R04 — 食品・飲料とカウントデータ

Pletikosa Cvijikj, I., & Michahelles, F. (2013). **Online engagement factors on Facebook brand pages.** *Social Network Analysis and Mining, 3*, 843–861. [DOI](https://doi.org/10.1007/s13278-013-0098-8) / [著者所属機関の本文](https://cocoa.ethz.ch/downloads/2013/07/1253_10.1007_s13278-013-0098-8.pdf)

食品・飲料の100ブランドページ、2か月を対象とし、内容・媒体・投稿時期を扱う。方法節で過分散に対する負の二項推定を説明する。販促、娯楽、情報、報酬を区別する設計の参考。ただし過去のFacebookの反応過程や定義を現在のXへそのまま移さない。

## R05 — 内容と配信の選択

Lee, D., Hosanagar, K., & Nair, H. S. (2018). **Advertising Content and Consumer Engagement on Social Media: Evidence from Facebook.** *Management Science, 64*(11), 5105–5131. [DOI](https://doi.org/10.1287/mnsc.2017.2902) / [大学書誌](https://www.gsb.stanford.edu/faculty-research/publications/advertising-content-consumer-engagement-social-media-evidence) / [著者版](https://repository.upenn.edu/bitstreams/84f143d8-fa82-47db-a77c-35c051d73f5a/download)

大規模な投稿内容のコード化と配信アルゴリズムの選択問題を扱う。価格情報と感情・人格的な表現を一つの排他的カテゴリに潰さない参考とする。単一アカウントの公開反応だけで露出選択を解決できるわけではない。著者版の標本情報を最終版の確定値として転記しない。

## R06 — 地域性の理論的な補助線

Eichinger, I., Schreier, M., & van Osselaer, S. M. J. (2022). **Connecting to Place, People, and Past: How Products Make Us Feel Grounded.** *Journal of Marketing, 86*(4). [DOI/本文](https://doi.org/10.1177/00222429211027469)

場所・人・過去との結びつきからgroundednessを整理する。地域情報を地名の数に還元しない理論的参考。ただし消費者心理に関する研究であり、本研究の投稿ラベルは心理尺度ではない。心理メカニズムを検証するなら読者調査または実験が別途必要。

## R07 — 国内の地域・日本語SNS研究

長尾雅信・南雲航・八木敏昭 (2025). **機械学習を用いたセンス・オブ・プレイスの解析―地域間ブランドとしての燕三条にかかるSNSデータをもとにした感情分析―.** *マーケティングレビュー, 6*(1), 1–8. [DOI](https://doi.org/10.7222/marketingreview.2025.001) / [本文](https://www.jstage.jst.go.jp/article/marketingreview/6/1/6_2025.001/_html/-char/ja)

燕三条についてのSNS投稿を日本語感情モデルで分析する国内事例。地域に関する発信と感情を扱う点で参考になるが、一般利用者の地域言及と企業公式投稿の分類では対象が異なる。原著のモデル評価値をイオン北海道データの精度として使わない。

## R08 — スーパーと社会的話題

Ballerini, J., Alam, G. M., Zvarikova, K., & Santoro, G. (2023). **How emotions from content social relevance mediate social media engagement: evidence from European supermarkets during the COVID-19 pandemic.** *British Food Journal, 125*(5), 1698–1715. [DOI](https://doi.org/10.1108/BFJ-06-2021-0695) / [大学書誌・要旨](https://iris.unito.it/handle/2318/1871918)

欧州20スーパー、8か国、2020年3〜6月の2,524投稿。社会的話題と反応を扱う。災害・地域行事・社会状況を時点文脈として記録する動機となる。観察的な媒介分析から心理的因果機序を断定する方法は採用しない。

## R09 — カウント回帰

Coxe, S., West, S. G., & Aiken, L. S. (2009). **The Analysis of Count Data: A Gentle Introduction to Poisson Regression and Its Alternatives.** *Journal of Personality Assessment, 91*(2), 121–136. [DOI](https://doi.org/10.1080/00223890802634175) / [著者書誌](https://stefanycoxe.github.io/research.html) / [論文要旨](https://pubmed.ncbi.nlm.nih.gov/19205933/)

カウントに適した回帰モデルの方法論資料。主分析で生カウントとlog-linkを使う理由を明記し、ゼロ件を対数変換で落とさない。時系列依存と観測窓は別途設計する。

## R10 — 日本語感情分析

Kajiwara, T., Chu, C., Takemura, N., Nakashima, Y., & Nagahara, H. (2021). **WRIME: A New Dataset for Emotional Intensity Estimation with Subjective and Objective Annotations.** *NAACL-HLT*, 2095–2104. [DOI/ACL](https://aclanthology.org/2021.naacl-main.169/)

原論文は17,000件の日本語SNS投稿に書き手と読み手の感情強度を付与する。後続のデータ拡張と区別する。企業の宣伝口調を担当者の内面感情と解釈せず、モデル・データ版を固定して対象領域で評価する。

## R11 — TweetEvalの適用範囲

Barbieri, F., Camacho-Collados, J., Espinosa Anke, L., & Neves, L. (2020). **TweetEval: Unified Benchmark and Comparative Evaluation for Tweet Classification.** *Findings of EMNLP*, 1644–1650. [DOI/ACL](https://aclanthology.org/2020.findings-emnlp.148/)

Twitter分類を共通条件で評価するベンチマーク。日本語企業投稿での妥当性を直接保証する資料ではない。元の計画から残すが、感情モデル採用の直接根拠は日本語データと対象領域での評価に置く。

## R12 — 探索的トピック

Grootendorst, M. (2022). **BERTopic: Neural topic modeling with a class-based TF-IDF procedure.** arXivプレプリント. [本文ページ](https://arxiv.org/abs/2203.05794)

埋め込みとクラスタリングに基づくトピック抽出の候補。探索用途に限定し、seedや標本を変えた安定性・人手解釈を報告する。教師なしでもtestを含めたfitは将来予測評価への漏洩になり得る。

## R13 — 予測説明

Lundberg, S. M., & Lee, S.-I. (2017). **A Unified Approach to Interpreting Model Predictions.** *Advances in Neural Information Processing Systems, 30*. [会議原稿](https://papers.nips.cc/paper/2017/file/8a20a8621978632d76c43dfd28b67767-Paper.pdf)

SHAPの方法論。特徴寄与は対象モデル・背景分布に依存し、関連特徴間での割当てにも注意が必要。本研究では予測性能の確認後に解釈し、施策効果として示さない。

## R14 — 構造を保つ検証

Roberts, D. R., et al. (2017). **Cross-validation strategies for data with temporal, spatial, hierarchical, or phylogenetic structure.** *Ecography, 40*(8), 913–929. [DOI](https://doi.org/10.1111/ecog.02881) / [大学書誌](https://epub.uni-regensburg.de/39299/) / [著者版](https://www.wsl.ch/lud/biodiversity_events/papers/Roberts_et_al-2017-Ecography.pdf)

依存構造を無視する検証の問題を扱う。時間順・企画群の分割を採用する方法論上の参考。7日＋取得遅延というgapは本研究のラベル取得条件から導くもので、この論文がX向けに指定した値ではない。

## R15 — 研究倫理

Fiesler, C., & Proferes, N. (2018). **“Participant” Perceptions of Twitter Research Ethics.** *Social Media + Society, 4*(1). [DOI/出版社](https://doi.org/10.1177/2056305118763366)

公開投稿の研究利用について、利用者の認識や文脈を考える根拠。企業発信を対象とし、一般利用者の返信本文を主分析から外す。法的・契約上の可否をこの論文だけから判定しない。

## R16 — 食品小売Twitterという隣接領域

Borrero, J. D. (2023). **Analysis of tweets from food retailers operating in Spain and the UK: How user-generated content on Twitter can help agrifood cooperatives build better relationships with their customers.** *REVESCO. Revista de Estudios Cooperativos, 143*, e85557. [DOI](https://doi.org/10.5209/reve.85557) / [出版社本文](https://revesco.es/txt/REVESCO%20Juan%20Diego%20BORRERO%20SANCHEZ.htm)

食品小売Twitterの内容・関係性の分析という隣接研究。食品小売Xの研究が存在しないとは書けない。原著に記載される当時のAPI取得上限を、現在の収集可能範囲や必要標本数として流用しない。

## R17 — 公式API資料（2026-09-17確認）

- [Metrics](https://docs.x.com/x-api/fundamentals/metrics)：public_metricsにimpression_countが記載される。取得可否・欠測は実応答で確認する。クリック等の非公開値とは区別する。
- [Timelines](https://docs.x.com/x-api/posts/timelines/introduction) / [Search](https://docs.x.com/x-api/posts/search/introduction)：対象期間と取得経路を分ける。
- [X API](https://docs.x.com/x-api/introduction)：現在の利用・料金体系の入口。費用の見積りと実課金は未実施。
- [Policies and agreements](https://docs.x.com/developer-terms)：規約入口のみ確認。全条項の適合性確認・公開承認が完了した意味ではない。

公開可否や料金を固定値で記載せず、収集直前に権限・再配布・保存/削除要件を再確認して記録する。

## 未確認・次の調査

R02の本文・補足で地域性の厳密な定義と推定仕様を確認する必要がある。懸賞参加条件と反応種別の本研究独自の分類は、既存尺度として検証済みではない。短文・画像内日本語の多モーダル予測は今回の中核から外し、データ量と測定精度を確保してから別途レビューする。検索の範囲と除外理由は[literature_search.md](literature_search.md)に記録する。
