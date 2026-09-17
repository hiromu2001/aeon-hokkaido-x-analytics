# References

このファイルには、本研究の設計根拠として優先して確認する先行研究・公式資料をまとめる。

## Closest prior study: Japanese corporate Twitter/X

### Tanaka & Huang (2024)
Yusuke Tanaka & Lin Huang. **Enhancing social media engagement in Japan: An empirical study of design and content factors on brand account.** *International Journal of Marketing & Distribution*, 27(1-2), 53–72, 2024.

- DOI: https://doi.org/10.5844/jsmd.27.1-2_53
- J-STAGE: https://www.jstage.jst.go.jp/article/jsmd/27/1-2/27_53/_article/-char/en
- 対象: SHARP公式Twitterの500投稿
- 重要点: design/content要因とlikes / retweets / repliesの関係を分析。日本企業Twitter研究として本研究に最も近いベースライン。

## Brand-post engagement foundations

### de Vries, Gensler & Leeflang (2012)
L. de Vries, S. Gensler, P. S. H. Leeflang. **Popularity of Brand Posts on Brand Fan Pages: An Investigation of the Effects of Social Media Marketing.** *Journal of Interactive Marketing*, 26(2), 83–91, 2012.

- DOI: https://doi.org/10.1016/j.intmar.2012.01.003
- 355 brand posts / 11 international brands
- vividness、interactivity、content等をbrand-post popularityと結びつけて検討した代表的研究。

## NLP for social-media text

### Barbieri et al. (2020) — TweetEval
Francesco Barbieri, Jose Camacho-Collados, Luis Espinosa Anke, Leonardo Neves. **TweetEval: Unified Benchmark and Comparative Evaluation for Tweet Classification.** *Findings of EMNLP 2020*, 1644–1650.

- DOI: https://doi.org/10.18653/v1/2020.findings-emnlp.148
- ACL Anthology: https://aclanthology.org/2020.findings-emnlp.148/
- Twitter固有のsentiment、emotion、irony、stance等の分類benchmark。
- 一般文章向けNLPモデルを無検証でX投稿へ流用しない根拠として重要。

### Grootendorst (2022) — BERTopic
Maarten Grootendorst. **BERTopic: Neural topic modeling with a class-based TF-IDF procedure.** 2022.

- arXiv: https://arxiv.org/abs/2203.05794
- Sentence embeddingsとclusteringを使ったtopic modeling。
- 本研究では探索的topic抽出・特徴生成候補として利用。

## Research ethics

### Fiesler & Proferes (2018)
Casey Fiesler & Nicholas Proferes. **“Participant” Perceptions of Twitter Research Ethics.** *Social Media + Society*, 4(1), 2018.

- DOI: https://doi.org/10.1177/2056305118763366
- 公開Twitterデータであっても、研究利用に対するユーザー認識は文脈依存であり、倫理上の検討が必要であることを示す。
- 本研究では一般ユーザーの返信本文をPrimary analysisから外す方針の根拠の一つ。

## X API / platform documentation

実装時は必ず最新版を再確認する。

- X API Timelines: https://docs.x.com/x-api/posts/timelines/introduction
- Full-Archive Search: https://docs.x.com/x-api/posts/search/quickstart/full-archive-search
- Usage / billing: https://docs.x.com/x-api/fundamentals/post-cap
- Developer terms / policies: https://docs.x.com/developer-terms

## Literature review TODO

実装前に以下の領域を追加レビューする。

- [ ] 小売業・スーパーマーケットのSNSエンゲージメント研究
- [ ] Food / retail brand social-media engagement
- [ ] Negative Binomial regressionを用いたSNSカウントデータ研究
- [ ] 日本語SNS向けsentiment / emotion model
- [ ] corporate-account personality / humanized brand voice
- [ ] social media temporal effects（曜日・時間帯・季節）
- [ ] campaign / sweepstakes投稿のengagement bias
- [ ] multimodal social-media engagement prediction
- [ ] X APIの再配布・保存・表示要件

> 参考文献は、分析実装時に「実際に採用した変数・モデル」と対応付けて更新する。単に文献数を増やすのではなく、各手法の採用根拠を明確にする。