# FAMI/JINQIAN research note — supporting data

「株式トークンは、オンチェーンの需要ショックを現物市場へ伝えるのか」の図表・検証台帳です。各データは取得時点のスナップショットであり、現在のAPI・取引画面の表示と一致しない場合があります。

## 本文のどこで使うか

| 本文の節 | 図表・主張 | このフォルダの資料 |
| --- | --- | --- |
| `FAMI/JINQIANは、裁定による価格伝播の事例だったのか` | 表1：FAMIの公式性・供給・経済的接続の確認 | `data/fami_economic_connection_ledger.csv` |
| `FAMIの供給比率は、公式群から桁違いに外れる` | 図1：FAMIと公式企業株式トークン176件の供給量比 | `data/official_token_supply_snapshot.csv`、`data/underlying_market_data_snapshot.csv`、`data/official_token_market_data_joined.csv`、`data/official_corporate_equity_universe.csv`、`figures/figure_01_supply_ratio.png` |
| `オンチェーンの買いは、現物株の買いに直結していない` | 図2：最多FAMI/USDGプールの実効約定価格・1分VWAPとFarmmi現物株の比較 | `data/fami_usdg_pool_swap_ranking.csv`、`data/fami_usdg_dominant_pool_effective_prices.csv`、`data/fami_usdg_cash_market_1m.csv`、`data/fami_yahoo_1m_gap_audit_summary.json`、`figures/figure_02_execution_price_and_equity_price.png` |
| `公式株式トークンの周辺にあるミームコインのペア市場は、無視できるほど小さくない` | 図3・表3：候補ペアの探索、活動規模、確認標本 | `data/official_equity_candidate_pair_audit.csv`、`data/official_equity_candidate_positive_liquidity_pools.csv`、`data/candidate_pair_activity_clusters.csv`、`data/candidate_pair_cluster_summary.csv`、`data/candidate_pair_cluster_samples.csv`、`figures/figure_03_candidate_pair_activity_clusters.png` |
| 同上 | 図4：候補ペアがRobinhood Chain上の基軸資産ペアの活動域と重なる範囲 | `data/base_asset_positive_liquidity_pools.csv`、`data/candidate_pair_base_asset_density_bands.csv`、`figures/figure_04_base_pair_density_bands.png` |

## 構成

### 図表

| ファイル | 内容 |
| --- | --- |
| `figures/figure_01_supply_ratio.png` | FAMIと公式RHJ企業株式トークンの総供給量比 |
| `figures/figure_02_execution_price_and_equity_price.png` | FAMI/USDG実効約定価格とFarmmi現物株の1分足 |
| `figures/figure_03_candidate_pair_activity_clusters.png` | 公式株式トークンの候補ペアにおける流動性・出来高の探索的分類 |
| `figures/figure_04_base_pair_density_bands.png` | 候補ペアとUSDG・ETH・WETHを含む基軸資産ペアの活動域比較 |

### 図1：公式トークンの供給量と対応株式

| ファイル | 内容 |
| --- | --- |
| `data/official_token_supply_snapshot.csv` | 現行RHJ公式コントラクト194件の生のERC-20 `totalSupply()` |
| `data/underlying_market_data_snapshot.csv` | 対応銘柄のYahoo Finance市場データ取得値 |
| `data/official_token_market_data_joined.csv` | 上記二つを結合した全件台帳 |
| `data/official_corporate_equity_universe.csv` | `quoteType == EQUITY` の企業株式176件。図1の公式比較群 |

### 図2：FAMI/USDGとFarmmi現物株

| ファイル | 内容 |
| --- | --- |
| `data/fami_usdg_pool_swap_ranking.csv` | 初期化ログでFAMI/USDGと確認した40プールの同一窓Swap件数順位 |
| `data/fami_usdg_dominant_pool_effective_prices.csv` | 最多Swapプールの全116,147件。実効約定価格とSwap後表示価格を別列で保存 |
| `data/fami_usdg_cash_market_1m.csv` | 図2に用いたオンチェーン分次値とFarmmi現物株1分足の結合データ |
| `data/fami_yahoo_1m_gap_audit_summary.json` | Yahooの1分足にある6分のOHLCV空値に関する監査結果 |
| `data/fami_economic_connection_ledger.csv` | FAMIの公式性、供給、経済的接続の確認項目台帳 |

### 図3・表3：公式株式トークンと候補ペア

| ファイル | 内容 |
| --- | --- |
| `data/official_equity_candidate_pair_audit.csv` | 企業株式トークン176件のAPI応答・相手分類・探索対象判定 |
| `data/official_equity_candidate_positive_liquidity_pools.csv` | 除外規則後に残った正の流動性を持つ候補プールの台帳 |
| `data/candidate_pair_activity_clusters.csv` | 24時間出来高が正の991件に対するK-means分類の全行 |
| `data/candidate_pair_cluster_summary.csv` | Kの比較、クラスタの件数・代表的な活動規模 |
| `data/candidate_pair_cluster_samples.csv` | 各クラスタから本文・表3で確認した1標本 |

### 図4：基軸資産ペアとの比較

| ファイル | 内容 |
| --- | --- |
| `data/base_asset_positive_liquidity_pools.csv` | USDG・ネイティブETH・WETHを含む基軸資産ペアの正の流動性プール |
| `data/candidate_pair_base_asset_density_bands.csv` | 図3と同じ991件について、基軸資産ペアの50%・90%密度帯への所属を判定した台帳 |

## 読む際の注意

- DEX Screenerのデータは直接トークン・ペアAPIが返した範囲の時点表示であり、チェーン全体の全プール、市場シェア、実行可能な板の深さ、純買い需要を意味しません。
- 図3のK-meansは、流動性USDと24時間出来高USDの対数値を用いる探索的な活動規模の分類です。ミームコイン分類や市場品質の判定ではありません。K=2〜6を比較し、silhouette scoreが最大のK=6を採用しました。
- 図2のオンチェーン価格は、最多Swapプールの実効約定価格を1分VWAPに集計したものです。個別の因果効果を推定するものではなく、流通した「機械的・一対一の価格転写」という説明を検証するために用いました。
- FAMIと公式群の供給量比は、生のERC-20 `totalSupply()` とYahoo Finance取得時点の `shares outstanding` の比較です。現物株の保有、裏付け、償還、経済的エクスポージャーを示すものではありません。

中間生成物、旧版図、個別APIの生レスポンスは、公開データセットを読みやすく保つため含めていません。各最終台帳には照会対象・アドレス・取得時刻・確認URLを保持しています。
