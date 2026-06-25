# FXコンパス (hajimete-fx.com) サイトアーキテクチャ設計 v1

作成: 2026-06-25
目的: 月間100万円のアフィリエイト収益を達成するためのサイト構造・コンテンツ戦略・技術基盤の全体設計。

---

## 0. 前提と制約

| 項目 | 内容 |
|---|---|
| 現状 | 35ページの静的FXサイト。Cloudflare Pages無料枠。ゼロトラフィック・ゼロ収益 |
| 技術 | 静的HTML + vanilla JS + CSS。publish.pyでビルド。外部依存ゼロ |
| 法規制 | 海外FXブローカーの口座紹介は不可（金商法リスク）。売買助言なし。PR表記必須 |
| 収益源 | 国内FX口座(DMM FX/FXTF等)、VPS(ConoHa/XServer)、TradingView、DMM CFD |
| 目標 | 月間100万円 = 国内FX口座 x 30件(単価2万円=60万) + VPS x 5件(単価5万円=25万) + TradingView(継続30%=15万) |
| ドメイン | hajimete-fx.com（FX初心者を直撃する最高のドメイン名。これ自体が資産） |

---

## 1. 収益逆算モデル（100万円/月への道筋）

### 1-1. 案件別の必要成約数

| 案件 | 単価(円) | 必要件数/月 | 月間売上(円) | 必要クリック数(CVR仮定2%) | 必要PV(CTR仮定5%) |
|---|---|---|---|---|---|
| DMM FX 口座開設 | 20,000 | 20 | 400,000 | 1,000 | 20,000 |
| FXTF 口座開設 | 10,000 | 10 | 100,000 | 500 | 10,000 |
| ConoHa VPS | 50,000 | 3 | 150,000 | 150 | 3,000 |
| XServer VPS | 30,000 | 2 | 60,000 | 100 | 2,000 |
| TradingView | 継続30% | - | 150,000 | 500 | 10,000 |
| DMM CFD | 14,200 | 5 | 71,000 | 250 | 5,000 |
| その他(お名前/BIGLOBE) | 5,000 | 10 | 50,000 | 500 | 10,000 |
| **合計** | | | **1,031,000** | **3,000** | **60,000** |

仮定: アフィリリンクCTR 5%, CVR 2%はFX金融系の一般的な数値。実測で校正する。
結論: **月間6万PVで100万円が射程に入る。** 200ページ x 平均300PV/月 = 60,000PV。

### 1-2. PV獲得戦略の内訳

| チャネル | 月間PV目標 | 手段 |
|---|---|---|
| 検索流入(Google) | 45,000 (75%) | ピラー+クラスター構造でトピカルオーソリティ |
| AI検索(Google AI Overview/Perplexity) | 6,000 (10%) | 構造化データ+SpeakableSpecification+明確なFAQ |
| SNS(X/YouTube概要欄) | 6,000 (10%) | 計算ツール共有・比較表画像のバイラル |
| ダイレクト/リファラル | 3,000 (5%) | ブックマーク+note二次利用からの流入 |

---

## 2. ピラーページ+クラスター構造（5本柱）

### 設計原則

- 各ピラーは3,000-5,000語の包括的記事
- 各クラスターは1,500-2,500語の具体的記事
- ピラー -> クラスターは必ず双方向リンク
- クラスター間も関連があれば相互リンク（同一クラスター内を優先）
- 全ページを3クリック以内にホームから到達可能にする

### 2-1. ピラー1: FX口座比較（収益の主柱 = 全体の50%）

**ピラーページ**: `/guide/fx-kouza-hikaku.html`
**対象KW**: 「FX口座 比較」「FX おすすめ」「FX 口座開設」
**CTA先**: DMM FX, FXTF, GMOクリック
**想定PV**: 月間15,000（ピラー3,000 + クラスター合計12,000）

クラスター記事:

| # | ファイル | 対象KW | 検索意図 | 主CTA | 状態 |
|---|---|---|---|---|---|
| 1-1 | kouza-ranking.html | FX口座 ランキング 2026 | 比較して選びたい | DMM FX | 既存(改修) |
| 1-2 | spread-hikaku.html | FX スプレッド 比較 | コスト比較 | FXTF | 既存(改修) |
| 1-3 | swap-hikaku.html | FX スワップポイント 比較 | 長期保有で選びたい | DMM FX | 既存(改修) |
| 1-4 | ikura-kara.html | FX いくらから始められる | 最低資金を知りたい | DMM FX(1万通貨) | 既存(改修) |
| 1-5 | demo-trade.html | FX デモトレード おすすめ | 無料で試したい | DMM FX/GMO | 既存(改修) |
| 1-6 | fx-app-hikaku.html | FX アプリ 比較 | スマホで取引したい | DMM FX | 既存(改修) |
| 1-7 | kokunai-kouza.html | 国内FX口座 選び方 | 安全な口座が欲しい | DMM FX/FXTF | 既存(改修) |
| 1-8 | NEW: fx-kouza-kaisestu-tejun.html | FX 口座開設 手順 | 実際の手順を知りたい | DMM FX | 新規 |
| 1-9 | NEW: fx-kouza-campaign.html | FX 口座開設 キャンペーン | お得に始めたい | DMM FX | 新規 |
| 1-10 | NEW: fx-kouza-shinsa.html | FX 口座開設 審査 | 審査が不安 | DMM FX | 新規 |
| 1-11 | NEW: dmm-fx-kuchikomi.html | DMM FX 評判 口コミ | 特定業者の評判を知りたい | DMM FX | 新規 |
| 1-12 | NEW: fxtf-kuchikomi.html | FXTF 評判 口コミ | 特定業者の評判を知りたい | FXTF | 新規 |
| 1-13 | NEW: gmo-click-kuchikomi.html | GMOクリック証券 評判 | 特定業者の評判を知りたい | - | 新規 |
| 1-14 | NEW: sbi-fx-trade.html | SBI FXトレード 評判 | 1通貨から始めたい | - | 新規 |
| 1-15 | NEW: fx-kouza-fukusu.html | FX 口座 複数 | 複数口座のメリット | DMM FX+FXTF | 新規 |
| 1-16 | NEW: fx-hikaku-vs-dmmfx-gmo.html | DMM FX GMOクリック 比較 | 2社で迷っている | DMM FX | 新規(pSEO) |
| 1-17 | NEW: fx-hikaku-vs-dmmfx-fxtf.html | DMM FX FXTF 比較 | 2社で迷っている | FXTF | 新規(pSEO) |
| 1-18 | NEW: fx-hikaku-vs-dmmfx-sbi.html | DMM FX SBI FXトレード 比較 | 2社で迷っている | DMM FX | 新規(pSEO) |

### 2-2. ピラー2: FX自動売買/EA/VPS（高単価の収益柱 = 全体の25%）

**ピラーページ**: `/guide/fx-jidou-baibai.html`
**対象KW**: 「FX 自動売買」「EA 始め方」「FX VPS」
**CTA先**: ConoHa VPS, XServer VPS, お名前.com
**想定PV**: 月間12,000（ピラー2,500 + クラスター合計9,500）

クラスター記事:

| # | ファイル | 対象KW | 検索意図 | 主CTA | 状態 |
|---|---|---|---|---|---|
| 2-1 | vps.html | FX VPS おすすめ | VPSを選びたい | ConoHa | 既存(改修) |
| 2-2 | fx-vps-hikaku.html | FX VPS 比較 | VPSを比較したい | ConoHa/XServer | 既存(改修) |
| 2-3 | vps-setup.html | VPS 設定 MT4 | 設定手順を知りたい | ConoHa | 既存(改修) |
| 2-4 | ea-hajimekata.html | EA 始め方 初心者 | EAを始めたい | ConoHa | 既存(改修) |
| 2-5 | mac-mt5.html | Mac MT5 使い方 | MacでMT5を使いたい | ConoHa | 既存(改修) |
| 2-6 | mac-vps.html | Mac VPS FX | MacでVPS使いたい | ConoHa | 既存(改修) |
| 2-7 | NEW: ea-osusume.html | EA おすすめ 無料 | 使えるEAを探している | ConoHa | 新規 |
| 2-8 | NEW: mt4-mt5-chigai.html | MT4 MT5 違い | プラットフォーム選び | ConoHa | 新規 |
| 2-9 | NEW: fx-jidou-baibai-kiken.html | FX 自動売買 リスク 危険 | リスクを知りたい | - (信頼構築) | 新規 |
| 2-10 | NEW: conoha-vps-fx-setup.html | ConoHa VPS FX 設定 | 具体的な設定手順 | ConoHa | 新規 |
| 2-11 | NEW: xserver-vps-fx-setup.html | XServer VPS FX 設定 | 具体的な設定手順 | XServer | 新規 |
| 2-12 | NEW: vps-hikaku-conoha-xserver.html | ConoHa XServer 比較 | 2社で迷っている | ConoHa | 新規(pSEO) |
| 2-13 | NEW: ea-backtest-yarikata.html | EA バックテスト やり方 | 検証方法を知りたい | ConoHa | 新規 |
| 2-14 | NEW: fx-jidou-baibai-zeikin.html | FX 自動売買 税金 確定申告 | 税金が不安 | - (信頼構築) | 新規 |

### 2-3. ピラー3: FXチャート分析/テクニカル（TradingView収益 = 継続報酬の柱）

**ピラーページ**: `/guide/fx-chart-bunseki.html`
**対象KW**: 「FX チャート 見方」「テクニカル分析 初心者」
**CTA先**: TradingView
**想定PV**: 月間12,000（ピラー2,000 + クラスター合計10,000）

クラスター記事:

| # | ファイル | 対象KW | 検索意図 | 主CTA | 状態 |
|---|---|---|---|---|---|
| 3-1 | chart-yomikata.html | FX チャート 読み方 | チャートを読みたい | TradingView | 既存(改修) |
| 3-2 | tradingview.html | TradingView 使い方 | ツールを使いこなしたい | TradingView | 既存(改修) |
| 3-3 | tradingview-plan.html | TradingView 料金 プラン | プランを比較したい | TradingView | 既存(改修) |
| 3-4 | NEW: fx-indicator-osusume.html | FX インジケーター おすすめ | 効果的な指標を知りたい | TradingView | 新規 |
| 3-5 | NEW: fx-idou-heikinsen.html | FX 移動平均線 使い方 | 基本テクニカルを学びたい | TradingView | 新規 |
| 3-6 | NEW: fx-rousoku-ashi.html | ローソク足 パターン 一覧 | パターンを覚えたい | TradingView | 新規 |
| 3-7 | NEW: fx-bollinger-band.html | ボリンジャーバンド FX 使い方 | 具体的な手法 | TradingView | 新規 |
| 3-8 | NEW: fx-rsi-macd.html | RSI MACD 使い方 FX | オシレーター系を学びたい | TradingView | 新規 |
| 3-9 | NEW: fx-support-resistance.html | サポートライン レジスタンスライン | 水平線を引きたい | TradingView | 新規 |
| 3-10 | NEW: fx-trend-line.html | FX トレンドライン 引き方 | トレンド判断をしたい | TradingView | 新規 |
| 3-11 | NEW: tradingview-vs-mt4.html | TradingView MT4 比較 | ツール選びで迷っている | TradingView | 新規(pSEO) |
| 3-12 | NEW: fx-multi-timeframe.html | FX マルチタイムフレーム 分析 | 上位足と下位足の見方 | TradingView | 新規 |

### 2-4. ピラー4: FX初心者ロードマップ（全案件への導線ハブ）

**ピラーページ**: `/guide/fx-hajimekata.html`（既存を大幅改修）
**対象KW**: 「FX 始め方」「FX 初心者 何から」
**CTA先**: DMM FX（最初の口座として）
**想定PV**: 月間12,000（ピラー5,000 + クラスター合計7,000）

クラスター記事:

| # | ファイル | 対象KW | 検索意図 | 主CTA | 状態 |
|---|---|---|---|---|---|
| 4-1 | order-types.html | FX 注文方法 種類 | 注文の仕方を知りたい | DMM FX | 既存(改修) |
| 4-2 | leverage-guide.html | FX レバレッジ とは 計算 | リスクを理解したい | DMM FX | 既存(改修) |
| 4-3 | currency-pairs.html | FX 通貨ペア おすすめ 初心者 | 何を取引すべきか | DMM FX | 既存(改修) |
| 4-4 | NEW: fx-lot-keisan.html | FX ロット 計算 | 適切なサイズを知りたい | DMM FX | 新規 |
| 4-5 | NEW: fx-pips-toha.html | FX pips とは 計算 | 基本用語を理解したい | - | 新規 |
| 4-6 | NEW: fx-spread-toha.html | FX スプレッド とは | コスト構造を理解したい | FXTF | 新規 |
| 4-7 | NEW: fx-risk-kanri.html | FX リスク管理 資金管理 | 損失を抑えたい | - (信頼構築) | 新規 |
| 4-8 | NEW: fx-torihiki-jikan.html | FX 取引時間 何時まで | 取引可能時間を知りたい | DMM FX | 新規 |
| 4-9 | NEW: fx-yogo-shu.html | FX 用語集 初心者 | 用語がわからない | - (SEO集客) | 新規 |
| 4-10 | NEW: fx-shippai-rei.html | FX 失敗 初心者 | 同じ失敗を避けたい | - (信頼構築) | 新規 |
| 4-11 | NEW: fx-benkyou-hou.html | FX 勉強 方法 本 | 学習ロードマップが欲しい | TradingView | 新規 |
| 4-12 | NEW: fx-shisan-unyou.html | FX 資産運用 始め方 | 投資として考えたい | DMM FX | 新規 |

### 2-5. ピラー5: FX副業/税金/確定申告（信頼性構築 + 長期流入）

**ピラーページ**: `/guide/fx-fukugyou.html`（既存を大幅改修）
**対象KW**: 「FX 副業」「FX 税金」「FX 確定申告」
**CTA先**: なし（信頼構築が主目的。文末にDMM FX/TradingViewを自然導線）
**想定PV**: 月間9,000（ピラー3,000 + クラスター合計6,000）

クラスター記事:

| # | ファイル | 対象KW | 検索意図 | 主CTA | 状態 |
|---|---|---|---|---|---|
| 5-1 | kakutei-shinkoku.html | FX 確定申告 やり方 | 申告手順を知りたい | - | 既存(改修) |
| 5-2 | NEW: fx-zeikin-keisan.html | FX 税金 計算 シミュレーション | 税額を知りたい | - (計算ツール) | 新規 |
| 5-3 | NEW: fx-fukugyou-kaishain.html | FX 副業 会社員 バレない | 会社に知られたくない | DMM FX | 新規 |
| 5-4 | NEW: fx-sonshitsu-kurikoshi.html | FX 損失 繰越控除 | 損を活かしたい | - | 新規 |
| 5-5 | NEW: fx-kehi-keihi.html | FX 経費 何が落ちる | 節税したい | - | 新規 |
| 5-6 | NEW: fx-kaigyo-todoke.html | FX 開業届 個人事業主 | 本格的に始めたい | - | 新規 |
| 5-7 | NEW: fx-my-number.html | FX マイナンバー なぜ必要 | 不安を解消したい | DMM FX | 新規 |
| 5-8 | NEW: fx-nenmatsu-chosei.html | FX 年末 損益調整 | 節税テクニック | - | 新規 |

### 2-6. 独立ページ（ピラーに属さない）

| # | ファイル | 用途 | 状態 |
|---|---|---|---|
| S-1 | index.html | トップページ（全ピラーへのハブ） | 既存(改修) |
| S-2 | about.html | 運営者情報・E-E-A-T | 既存(維持) |
| S-3 | legal/disclaimer.html | 免責事項 | 既存(維持) |
| S-4 | legal/pr-policy.html | 広告掲載ポリシー | 既存(維持) |
| S-5 | tools/calculator.html | リスク管理計算ツール | 既存(維持) |
| S-6 | tools/tracker.html | 進捗トラッキング | 既存(維持) |
| S-7 | gold-cfd.html | ゴールドCFD | 既存(維持) |
| S-8 | guide/koushin-log.html | 更新ログ | 既存(維持) |

### 2-7. プロップファーム関連（既存資産。縮小して維持）

プロップは法規制グレー領域のため、SEOの主力にはしない。ただし既存ページは資産として維持し、FTMO等のアフィリ導線として機能させる。

| # | ファイル | 状態 |
|---|---|---|
| P-1 | guide/ftmo.html | 既存(維持) |
| P-2 | guide/erabikata.html | 既存(維持) |
| P-3 | guide/challenge-rules.html | 既存(維持) |
| P-4 | guide/shikin-kanri.html | 既存(維持) |
| P-5 | guide/shikin-kessai-hou.html | 既存(維持) |
| P-6 | guide/prop-no-risk.html | 既存(維持) |
| P-7 | guide/prop-yougo.html | 既存(維持) |

### 2-8. 削除するページ

なし。既存35ページは全て維持するが、検索意図に合わせてtitle/descriptionを全面書き直す。

---

## 3. プログラマティックSEO用ページ

### 3-1. ブローカー比較ページ（XX vs YY）

対象ブローカー: DMM FX / FXTF / GMOクリック証券 / SBI FXトレード / 外為どっとコム / みんなのFX / LIGHT FX / 松井証券FX
組み合わせ: 8C2 = 28ページ（ただし初期は主要6組み合わせのみ生成）

**テンプレート**: `/guide/fx-hikaku-vs-{A}-{B}.html`

生成データ（JSON）:
```
brokers.json:
{
  "dmmfx": {
    "name": "DMM FX",
    "spread_usdjpy": "0.2銭",
    "min_unit": "10,000通貨",
    "pairs": 21,
    "swap_usdjpy": "要公式確認",
    "tools": "独自アプリ/PC",
    "demo": true,
    "affiliate_key": "dmmfx",
    "strengths": ["スプレッド最狭水準", "LINEでのサポート", "取引ツールの使いやすさ"],
    "weaknesses": ["最小取引単位が1万通貨"]
  },
  ...
}
```

### 3-2. 通貨ペア個別ページ

対象: 主要10通貨ペア
**テンプレート**: `/guide/currency/{pair}.html`

| 通貨ペア | ファイル | 対象KW |
|---|---|---|
| USD/JPY | usdjpy.html | ドル円 特徴 FX |
| EUR/JPY | eurjpy.html | ユーロ円 特徴 |
| GBP/JPY | gbpjpy.html | ポンド円 特徴 |
| AUD/JPY | audjpy.html | 豪ドル円 特徴 |
| EUR/USD | eurusd.html | ユーロドル 特徴 |
| GBP/USD | gbpusd.html | ポンドドル 特徴 |
| NZD/JPY | nzdjpy.html | NZドル円 |
| CAD/JPY | cadjpy.html | カナダドル円 |
| CHF/JPY | chfjpy.html | スイスフラン円 |
| TRY/JPY | tryjpy.html | トルコリラ円 スワップ |

### 3-3. 計算ツールページ

**テンプレート**: `/tools/{tool-name}.html`

| ツール | ファイル | 対象KW | CTA |
|---|---|---|---|
| ロット計算機 | lot-calculator.html | FX ロット 計算機 | DMM FX |
| 利益損失計算機 | profit-calculator.html | FX 利益 計算 | DMM FX |
| スワップ計算機 | swap-calculator.html | FX スワップ 計算 | DMM FX |
| 証拠金計算機 | margin-calculator.html | FX 証拠金 計算 | DMM FX |
| pips計算機 | pips-calculator.html | pips 計算 ツール | - |
| 税金シミュレーター | tax-simulator.html | FX 税金 計算 シミュレーション | - |
| リスクリワード計算機 | rr-calculator.html | リスクリワード 計算 | TradingView |

---

## 4. 全ページ一覧（新サイトマップ）

### 4-1. 統計

| 区分 | ページ数 |
|---|---|
| 既存(維持) | 13 |
| 既存(改修) | 15 |
| 新規(手動作成) | 45 |
| 新規(pSEO テンプレート生成) | 15 (比較6 + 通貨ペア10 - 重複1) |
| 新規(計算ツール) | 7 |
| **合計** | **約95ページ（初期リリース）** |
| 第2期(pSEO追加) | +22 (残りのブローカー比較) |
| **最終規模** | **約120ページ** |

### 4-2. URL構造

```
hajimete-fx.com/
  index.html                              -- トップ（全ピラーへのハブ）
  about.html                              -- 運営者情報
  legal/
    disclaimer.html                       -- 免責事項
    pr-policy.html                        -- 広告掲載ポリシー
  guide/
    fx-kouza-hikaku.html                  -- [ピラー1] FX口座比較
    fx-jidou-baibai.html                  -- [ピラー2] 自動売買/EA/VPS
    fx-chart-bunseki.html                 -- [ピラー3] チャート分析
    fx-hajimekata.html                    -- [ピラー4] 初心者ロードマップ
    fx-fukugyou.html                      -- [ピラー5] 副業/税金
    kouza-ranking.html                    -- [1-1] 口座ランキング
    spread-hikaku.html                    -- [1-2] スプレッド比較
    ... (クラスター記事群)
    fx-hikaku-vs-dmmfx-gmo.html          -- [pSEO] ブローカー比較
    fx-hikaku-vs-dmmfx-fxtf.html         -- [pSEO] ブローカー比較
    ...
  guide/currency/
    usdjpy.html                           -- [pSEO] USD/JPY
    eurjpy.html                           -- [pSEO] EUR/JPY
    ...
  tools/
    calculator.html                       -- リスク管理計算ツール（既存）
    tracker.html                          -- 進捗トラッキング（既存）
    lot-calculator.html                   -- ロット計算機
    profit-calculator.html                -- 利益損失計算機
    swap-calculator.html                  -- スワップ計算機
    margin-calculator.html                -- 証拠金計算機
    pips-calculator.html                  -- pips計算機
    tax-simulator.html                    -- 税金シミュレーター
    rr-calculator.html                    -- リスクリワード計算機
  assets/
    links.js                              -- アフィリエイト設定
    site.js                               -- UIロジック
    site.css                              -- スタイル
  images/
    og-default.png                        -- OGP画像
```

---

## 5. 各テンプレートの骨格HTML構造

### 5-1. ピラーページテンプレート

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>{ピラータイトル}｜FXコンパス</title>
  <meta name="description" content="{120文字以内のメタディスクリプション}" />
  <link rel="canonical" href="https://hajimete-fx.com/guide/{slug}.html" />

  <!-- OGP -->
  <meta property="og:type" content="article" />
  <meta property="og:title" content="{ピラータイトル}｜FXコンパス" />
  <meta property="og:description" content="{メタディスクリプション}" />
  <meta property="og:url" content="https://hajimete-fx.com/guide/{slug}.html" />
  <meta property="og:site_name" content="FXコンパス" />
  <meta property="og:image" content="https://hajimete-fx.com/images/{slug}-og.png" />
  <meta name="twitter:card" content="summary_large_image" />

  <link rel="stylesheet" href="../assets/site.css" />

  <!-- 構造化データ: Article -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "{ピラータイトル}",
    "description": "{メタディスクリプション}",
    "inLanguage": "ja",
    "author": { "@type": "Organization", "name": "FXコンパス編集部" },
    "publisher": { "@type": "Organization", "name": "FXコンパス" },
    "datePublished": "{公開日}",
    "dateModified": "{更新日}",
    "mainEntityOfPage": "https://hajimete-fx.com/guide/{slug}.html"
  }
  </script>

  <!-- 構造化データ: BreadcrumbList -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "BreadcrumbList",
    "itemListElement": [
      { "@type": "ListItem", "position": 1, "name": "ホーム", "item": "https://hajimete-fx.com/" },
      { "@type": "ListItem", "position": 2, "name": "{ピラーカテゴリ}", "item": "https://hajimete-fx.com/guide/{slug}.html" }
    ]
  }
  </script>

  <!-- 構造化データ: FAQPage -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": [
      {
        "@type": "Question",
        "name": "{質問1}",
        "acceptedAnswer": { "@type": "Answer", "text": "{回答1}" }
      }
    ]
  }
  </script>

  <!-- AI検索対応: Speakable -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "WebPage",
    "speakable": {
      "@type": "SpeakableSpecification",
      "cssSelector": [".lead", ".article-head h1", ".ai-summary"]
    },
    "url": "https://hajimete-fx.com/guide/{slug}.html"
  }
  </script>
</head>
<body>
  <header class="site-header" id="siteHeader"></header>

  <!-- パンくずリスト -->
  <nav class="breadcrumb" aria-label="パンくず">
    <a href="../index.html">ホーム</a><span class="sep">></span>{ピラータイトル}
  </nav>

  <main>
    <article>
      <!-- 記事ヘッダ -->
      <header class="article-head">
        <h1>{ピラータイトル}</h1>
        <div class="article-meta">
          公開: <time datetime="{公開日}">{公開日表示}</time>
          ／ 更新: <time datetime="{更新日}">{更新日表示}</time>
          ／ FXコンパス編集部
        </div>
      </header>

      <!-- AI検索向け要約（1行。AI Overviewに引用されやすい） -->
      <p class="ai-summary">{記事全体を1文で要約。50-80文字}</p>

      <!-- リード文 -->
      <p class="lead">{リード文。記事の価値と対象読者を明確に}</p>

      <!-- ===== CTA配置点1: 記事上部（ソフトCTA） ===== -->
      <div class="cta-inline cta-soft" data-cta="top">
        <p class="cta-context">{文脈に沿った1行の導入文}</p>
        <a class="btn btn-outline" href="{アフィリURL}" rel="nofollow sponsored">
          {ソフトなCTAテキスト。例: 「口座の詳細を見る」}
        </a>
        <span class="pr-badge">PR</span>
      </div>

      <!-- 目次 -->
      <nav class="toc" aria-label="目次">
        <span class="toc-title">この記事の内容</span>
        <ol>
          <li><a href="#sec1">1. {見出し1}</a></li>
          <li><a href="#sec2">2. {見出し2}</a></li>
          <!-- ... -->
          <li><a href="#faq">よくある質問</a></li>
        </ol>
      </nav>

      <!-- 本文セクション群 -->
      <h2 id="sec1">1. {見出し1}</h2>
      <p>{本文}</p>

      <!-- ===== 比較テーブル ===== -->
      <div class="tbl-wrap scroll">
        <p class="scroll-hint">表は横にスクロールできます</p>
        <table class="compare-table">
          <caption>{テーブルの説明}</caption>
          <thead>
            <tr>
              <th>比較項目</th>
              <th class="reco">{おすすめ業者}<span class="reco-tag">おすすめ</span></th>
              <th>{業者2}</th>
              <th>{業者3}</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th>スプレッド(USD/JPY)</th>
              <td class="reco">0.2銭</td>
              <td>0.2銭</td>
              <td>0.3銭</td>
            </tr>
            <!-- ... -->
            <tr class="cta-row">
              <th></th>
              <td class="reco">
                <a class="btn btn-primary btn-sm" href="{URL}" rel="nofollow sponsored">
                  口座を開設する
                </a>
                <span class="pr-badge">PR</span>
              </td>
              <td><!-- ... --></td>
              <td><!-- ... --></td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- ===== CTA配置点2: 記事中間（ミディアムCTA） ===== -->
      <div class="cta-inline cta-medium" data-cta="mid">
        <div class="cta-card">
          <div class="cta-card-body">
            <h3 class="cta-card-title">{おすすめ業者名}</h3>
            <ul class="cta-card-features">
              <li>{特徴1}</li>
              <li>{特徴2}</li>
              <li>{特徴3}</li>
            </ul>
          </div>
          <div class="cta-card-action">
            <a class="btn btn-primary" href="{URL}" rel="nofollow sponsored">
              無料で口座を開設する
            </a>
            <span class="pr-badge">PR</span>
            <p class="cta-note">口座開設は最短5分・無料</p>
          </div>
        </div>
      </div>

      <h2 id="sec2">2. {見出し2}</h2>
      <p>{本文}</p>

      <!-- 編集部メモ（人間味・差別化） -->
      <div class="editor-memo">
        <span class="tag">編集部メモ</span>
        <p>{主観的だが誠実な所感。AIが書かない人間味}</p>
      </div>

      <!-- FAQ -->
      <section class="faq" id="faq">
        <h2>よくある質問</h2>
        <dl>
          <dt>{質問1}</dt>
          <dd>{回答1。事実ベース。助言はしない}</dd>
          <dt>{質問2}</dt>
          <dd>{回答2}</dd>
        </dl>
      </section>

      <!-- ===== CTA配置点3: 結論直後（ハードCTA） ===== -->
      <div class="cta-inline cta-hard" data-cta="bottom">
        <h3>この記事のまとめ</h3>
        <p>{3行の結論要約}</p>
        <div class="cta-buttons">
          <a class="btn btn-primary btn-lg" href="{メインCTA URL}" rel="nofollow sponsored">
            {メインCTAテキスト。例: 「DMM FXの口座を開設する（無料）」}
          </a>
          <span class="pr-badge">PR</span>
        </div>
        <p class="cta-sub">
          <a href="{サブCTA URL}">{サブCTA。例: 「FXTFの口座も比較する」}</a>
        </p>
      </div>

      <!-- 自動生成プロモ枠（site.jsが出力） -->
      <div id="promos"></div>

      <!-- クラスター記事への内部リンク -->
      <nav class="cluster-links">
        <h2>関連記事</h2>
        <div class="cluster-grid">
          <a href="{クラスター1 URL}" class="cluster-card">
            <span class="cluster-card-title">{記事タイトル}</span>
            <span class="cluster-card-desc">{1行説明}</span>
          </a>
          <!-- ... 6-8枚 -->
        </div>
      </nav>

      <!-- 他ピラーへの橋渡し -->
      <nav class="related-pillars">
        <h2>他のガイド</h2>
        <ul>
          <li><a href="{ピラー2 URL}">{ピラー2タイトル}</a></li>
          <li><a href="{ピラー3 URL}">{ピラー3タイトル}</a></li>
        </ul>
      </nav>

      <!-- 運営者カード -->
      <div data-author-card></div>

      <!-- 出典 -->
      <div class="source-list">
        <strong>出典</strong>
        <ol>
          <li>{出典1: 具体名・URL}</li>
          <li>{出典2}</li>
        </ol>
      </div>
    </article>
  </main>

  <footer class="site-footer" id="siteFooter"></footer>

  <script src="../assets/links.js"></script>
  <script src="../assets/site.js"></script>

  <!-- スティッキーCTA（モバイル用。本文を50%以上スクロールした時に表示） -->
  <div class="sticky-cta" id="stickyCta" aria-hidden="true">
    <a class="btn btn-primary btn-sm" href="{メインCTA URL}" rel="nofollow sponsored">
      {短いCTAテキスト}
    </a>
    <span class="pr-badge">PR</span>
    <button class="sticky-cta-close" aria-label="閉じる">&times;</button>
  </div>
</body>
</html>
```

### 5-2. クラスター記事テンプレート（ハウツー型）

```html
<!-- head部はピラーと同様。BreadcrumbListの階層が1段深くなる -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "ホーム", "item": "https://hajimete-fx.com/" },
    { "@type": "ListItem", "position": 2, "name": "{親ピラータイトル}", "item": "https://hajimete-fx.com/guide/{pillar-slug}.html" },
    { "@type": "ListItem", "position": 3, "name": "{クラスター記事タイトル}", "item": "https://hajimete-fx.com/guide/{cluster-slug}.html" }
  ]
}
</script>

<!-- HowTo構造化データ（手順系記事用） -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "{手順タイトル。例: FX口座の開設手順}",
  "description": "{概要}",
  "step": [
    {
      "@type": "HowToStep",
      "position": 1,
      "name": "{ステップ1タイトル}",
      "text": "{ステップ1の説明}",
      "url": "https://hajimete-fx.com/guide/{slug}.html#step1"
    },
    {
      "@type": "HowToStep",
      "position": 2,
      "name": "{ステップ2タイトル}",
      "text": "{ステップ2の説明}"
    }
  ]
}
</script>

<body>
  <!-- ... header/breadcrumb ... -->
  <main>
    <article>
      <header class="article-head">
        <h1>{クラスター記事タイトル}</h1>
        <div class="article-meta">...</div>
      </header>

      <p class="ai-summary">{1行要約}</p>
      <p class="lead">{リード文}</p>

      <!-- CTA配置点1: ソフト（「まだ口座を持っていない方はこちら」程度） -->
      <div class="cta-inline cta-soft" data-cta="top">...</div>

      <nav class="toc" aria-label="目次">...</nav>

      <!-- ステップ型の本文 -->
      <h2 id="step1">ステップ1: {タイトル}</h2>
      <div class="step-content">
        <div class="step-number">1</div>
        <div class="step-body">
          <p>{説明}</p>
          <!-- 画像があれば -->
          <figure>
            <img src="../images/{slug}-step1.webp"
                 alt="{代替テキスト}"
                 width="800" height="450"
                 loading="lazy" decoding="async" />
            <figcaption>{キャプション}</figcaption>
          </figure>
        </div>
      </div>

      <h2 id="step2">ステップ2: {タイトル}</h2>
      <div class="step-content">...</div>

      <!-- CTA配置点2: ステップの途中 or 直後 -->
      <div class="cta-inline cta-medium" data-cta="mid">...</div>

      <!-- FAQ -->
      <section class="faq" id="faq">...</section>

      <!-- CTA配置点3: 結論 -->
      <div class="cta-inline cta-hard" data-cta="bottom">...</div>

      <!-- 親ピラーへのリンク（必須。クラスター->ピラーの上向きリンク） -->
      <nav class="back-to-pillar">
        <a href="{親ピラー URL}">← {親ピラータイトル}に戻る</a>
      </nav>

      <!-- 同一クラスター内の関連記事 -->
      <nav class="related">
        <h2>関連記事</h2>
        <ul>
          <li><a href="{同クラスター記事1}">{タイトル1}</a></li>
          <li><a href="{同クラスター記事2}">{タイトル2}</a></li>
        </ul>
      </nav>

      <div data-author-card></div>
      <div class="source-list">...</div>
    </article>
  </main>
</body>
```

### 5-3. ブローカー比較ページテンプレート（pSEO）

```html
<!-- XX vs YY 比較ページ。データはbrokers.jsonからテンプレートに注入 -->
<head>
  <title>{ブローカーA} vs {ブローカーB} 徹底比較｜FXコンパス</title>
  <meta name="description"
        content="{ブローカーA}と{ブローカーB}をスプレッド・取引単位・ツール・スワップの4軸で比較。あなたに合うのはどちらか事実ベースで整理。" />

  <!-- Review構造化データ -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "WebPage",
    "mainEntity": {
      "@type": "ItemList",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "item": {
            "@type": "FinancialProduct",
            "name": "{ブローカーA}",
            "description": "{ブローカーAの1行説明}",
            "provider": { "@type": "Organization", "name": "{ブローカーA運営会社}" }
          }
        },
        {
          "@type": "ListItem",
          "position": 2,
          "item": {
            "@type": "FinancialProduct",
            "name": "{ブローカーB}",
            "description": "{ブローカーBの1行説明}",
            "provider": { "@type": "Organization", "name": "{ブローカーB運営会社}" }
          }
        }
      ]
    }
  }
  </script>
</head>

<body>
  <main>
    <article>
      <header class="article-head">
        <h1>{ブローカーA} vs {ブローカーB}｜どっちがいい？徹底比較</h1>
        <div class="article-meta">...</div>
      </header>

      <p class="ai-summary">
        {ブローカーA}と{ブローカーB}の主な違いは{差別化ポイント}です。
        {用途1}なら{ブローカーA}、{用途2}なら{ブローカーB}が向いています。
      </p>

      <!-- 結論ファースト: どちらが向くか -->
      <div class="verdict-box">
        <h2>結論: こんな人におすすめ</h2>
        <div class="verdict-grid">
          <div class="verdict-card verdict-a">
            <h3>{ブローカーA}が向く人</h3>
            <ul>
              <li>{理由1}</li>
              <li>{理由2}</li>
            </ul>
            <a class="btn btn-primary" href="{URL}" rel="nofollow sponsored">
              {ブローカーA}の口座を開設する
            </a>
            <span class="pr-badge">PR</span>
          </div>
          <div class="verdict-card verdict-b">
            <h3>{ブローカーB}が向く人</h3>
            <ul>
              <li>{理由1}</li>
              <li>{理由2}</li>
            </ul>
            <a class="btn btn-outline" href="{URL}" rel="nofollow sponsored">
              {ブローカーB}の口座を開設する
            </a>
            <span class="pr-badge">PR</span>
          </div>
        </div>
      </div>

      <!-- 比較テーブル（コスト関連を左に配置） -->
      <h2>スペック比較一覧</h2>
      <div class="tbl-wrap scroll">
        <table class="compare-table vs-table">
          <thead>
            <tr><th>比較項目</th><th>{ブローカーA}</th><th>{ブローカーB}</th></tr>
          </thead>
          <tbody>
            <tr><th>USD/JPYスプレッド</th><td>{値A}</td><td>{値B}</td></tr>
            <tr><th>最小取引単位</th><td>{値A}</td><td>{値B}</td></tr>
            <tr><th>通貨ペア数</th><td>{値A}</td><td>{値B}</td></tr>
            <tr><th>スワップポイント</th><td>{値A}</td><td>{値B}</td></tr>
            <tr><th>取引ツール</th><td>{値A}</td><td>{値B}</td></tr>
            <tr><th>デモ口座</th><td>{値A}</td><td>{値B}</td></tr>
          </tbody>
        </table>
      </div>

      <!-- 各項目の詳細比較（H2 x 4-5本） -->
      <h2>1. スプレッドの比較</h2>
      <p>{詳細な比較文。出典付き}</p>

      <!-- ... -->

      <!-- FAQ -->
      <section class="faq" id="faq">
        <h2>よくある質問</h2>
        <dl>
          <dt>{ブローカーA}と{ブローカーB}はどちらが初心者向きですか？</dt>
          <dd>{回答}</dd>
          <dt>両方の口座を開設することはできますか？</dt>
          <dd>可能です。FX口座は複数持つことができ... </dd>
        </dl>
      </section>

      <!-- CTA: 結論 -->
      <div class="cta-inline cta-hard" data-cta="bottom">
        <div class="cta-buttons cta-vs">
          <a class="btn btn-primary" href="{URL-A}" rel="nofollow sponsored">
            {ブローカーA}を開設する
          </a>
          <a class="btn btn-outline" href="{URL-B}" rel="nofollow sponsored">
            {ブローカーB}を開設する
          </a>
          <span class="pr-badge">PR</span>
        </div>
      </div>

      <!-- 親ピラーへ -->
      <nav class="back-to-pillar">
        <a href="fx-kouza-hikaku.html">← FX口座比較ガイドに戻る</a>
      </nav>

      <div class="source-list">...</div>
    </article>
  </main>
</body>
```

### 5-4. 計算ツールページテンプレート

```html
<head>
  <title>{ツール名}｜FXコンパス 無料ツール</title>
  <meta name="description" content="{ツールの説明。50-120文字}" />

  <!-- SoftwareApplication構造化データ -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": "{ツール名}",
    "applicationCategory": "FinanceApplication",
    "operatingSystem": "Web",
    "offers": {
      "@type": "Offer",
      "price": "0",
      "priceCurrency": "JPY"
    },
    "description": "{ツールの1行説明}"
  }
  </script>
</head>

<body>
  <main>
    <article>
      <header class="article-head">
        <h1>{ツール名}</h1>
        <p class="lead">{1行の価値提案}</p>
      </header>

      <!-- 計算ツール本体 -->
      <section class="tool-widget" id="toolWidget">
        <div class="tool-inputs">
          <div class="input-group">
            <label for="input1">{入力項目1}</label>
            <input type="number" id="input1" value="{デフォルト}" />
            <span class="input-unit">{単位}</span>
          </div>
          <!-- ... -->
          <button class="btn btn-primary" id="calcBtn">計算する</button>
        </div>

        <div class="tool-results" id="toolResults">
          <div class="result-card">
            <span class="result-label">{結果ラベル}</span>
            <span class="result-value" id="result1">-</span>
            <span class="result-unit">{単位}</span>
          </div>
          <!-- ... -->
        </div>

        <p class="tool-disclaimer">
          ※ この計算結果は目安です。実際の取引条件は各FX会社の公式サイトでご確認ください。
          投資助言ではありません。
        </p>
      </section>

      <!-- ツール使用後のCTA（自然な文脈） -->
      <div class="cta-inline cta-medium" data-cta="after-tool">
        <p class="cta-context">計算結果を確認したら、次は口座を選びましょう。</p>
        <a class="btn btn-primary" href="{URL}" rel="nofollow sponsored">
          DMM FXで口座を開設する（無料）
        </a>
        <span class="pr-badge">PR</span>
      </div>

      <!-- ツールの使い方 -->
      <h2>使い方</h2>
      <p>{ステップバイステップの説明}</p>

      <!-- 関連知識 -->
      <h2>{関連するFXの基礎知識}</h2>
      <p>{SEO向けのテキストコンテンツ。ツールページも検索流入を取る}</p>

      <!-- FAQ -->
      <section class="faq" id="faq">...</section>

      <!-- 関連ツール -->
      <nav class="related-tools">
        <h2>他のFXツール</h2>
        <div class="tools-grid">
          <a href="{他ツール1}" class="tool-card">
            <span class="tool-card-icon">{アイコン}</span>
            <span class="tool-card-title">{ツール名}</span>
          </a>
          <!-- ... -->
        </div>
      </nav>
    </article>
  </main>
</body>
```

### 5-5. 通貨ペアページテンプレート（pSEO）

```html
<head>
  <title>{通貨ペア名}({コード})の特徴・スプレッド・取引戦略｜FXコンパス</title>

  <!-- FinancialProduct構造化データ -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FinancialProduct",
    "name": "{通貨ペア名}",
    "description": "{通貨ペアの特徴を1行で}",
    "category": "ForeignExchange"
  }
  </script>
</head>

<body>
  <main>
    <article>
      <header class="article-head">
        <h1>{通貨ペア名}({コード})の特徴と取引のポイント</h1>
      </header>

      <p class="ai-summary">
        {コード}は{特徴の1行要約}。
        主要FX業者のスプレッドは{範囲}で、{取引に向く時間帯}の取引量が多い。
      </p>

      <!-- 基本スペック表 -->
      <div class="pair-specs">
        <div class="spec-item">
          <span class="spec-label">通貨ペア</span>
          <span class="spec-value">{コード}</span>
        </div>
        <div class="spec-item">
          <span class="spec-label">平均スプレッド</span>
          <span class="spec-value">{値}銭</span>
        </div>
        <div class="spec-item">
          <span class="spec-label">1日の平均値幅</span>
          <span class="spec-value">{値}pips</span>
        </div>
        <div class="spec-item">
          <span class="spec-label">活発な時間帯</span>
          <span class="spec-value">{時間帯}</span>
        </div>
      </div>

      <!-- 各社スプレッド比較（CTA付き） -->
      <h2>{コード}を取引できるFX口座比較</h2>
      <div class="tbl-wrap scroll">
        <table class="compare-table">
          <thead>
            <tr><th>FX口座</th><th>スプレッド</th><th>スワップ</th><th></th></tr>
          </thead>
          <tbody>
            <tr>
              <td>DMM FX</td><td>{値}</td><td>{値}</td>
              <td><a class="btn btn-sm btn-primary" href="{URL}" rel="nofollow sponsored">口座開設 <span class="pr-badge">PR</span></a></td>
            </tr>
            <!-- ... -->
          </tbody>
        </table>
      </div>

      <!-- 通貨ペアの特徴 -->
      <h2>{コード}の特徴</h2>
      <p>{通貨ペア固有の解説。pSEOでもここに固有価値を入れる}</p>

      <!-- 関連通貨ペア -->
      <nav class="related-pairs">
        <h2>関連する通貨ペア</h2>
        <ul>
          <li><a href="{関連ペア1}.html">{関連ペア1名}</a></li>
          <!-- ... -->
        </ul>
      </nav>
    </article>
  </main>
</body>
```

---

## 6. CTA配置の設計図

### 6-1. CTA配置ルール

```
記事の流れ:
  [ヘッダ]
  [パンくず]
  [H1 + メタ]
  [AI要約]
  [リード文]
  ┌─────────────────────┐
  │ CTA-1: ソフト        │  ← スクロール開始前に見える位置
  │ 「口座の詳細を見る」    │     CVR低いがインプレッション最大
  │ ボタン: btn-outline    │     記事を読まずに行動する層を拾う
  └─────────────────────┘
  [目次]
  [H2: セクション1]
  [H2: セクション2]
  ┌─────────────────────┐
  │ CTA-2: ミディアム      │  ← 記事の40-60%地点
  │ カード型（特徴3点+ボタン）│     文脈に沿った自然な挿入
  │ ボタン: btn-primary     │     比較テーブルの直後が最適
  └─────────────────────┘
  [H2: セクション3]
  [編集部メモ]
  [FAQ]
  ┌─────────────────────┐
  │ CTA-3: ハード          │  ← 結論直後（記事の最後）
  │ まとめ+大きなボタン      │     最もCVRが高い（読了者は意欲が高い）
  │ ボタン: btn-primary lg  │     メインCTA + サブCTA の2段構え
  └─────────────────────┘
  [関連記事]
  [出典]
  ┌─────────────────────────────────┐
  │ スティッキーCTA（モバイル底部）       │  ← 50%スクロール後に表示
  │ 薄いバー: ブランド色 + 短いテキスト   │     閉じるボタンあり（UX配慮）
  │ CTA疲れ防止: 1セッション1回まで       │     閉じたらsessionStorageで非表示
  └─────────────────────────────────┘
```

### 6-2. CTA文言のルール

| CTA段階 | 文言パターン | NG文言（法規制） |
|---|---|---|
| ソフト | 「口座の詳細を見る」「スペックを確認する」 | 「今すぐ稼ぐ」「必ず儲かる」 |
| ミディアム | 「無料で口座を開設する」「詳細を公式で確認」 | 「おすすめNo.1」（根拠なし） |
| ハード | 「DMM FXの口座を開設する（無料・最短5分）」 | 「勝てる口座」「プロが使う」 |
| スティッキー | 「口座開設はこちら」 | 「チャンスを逃すな」 |

### 6-3. ページタイプ別CTA配置

| ページタイプ | CTA-1(上部) | CTA-2(中間) | CTA-3(結論) | スティッキー |
|---|---|---|---|---|
| ピラー(比較系) | ソフト | カード型 | ハード+サブ | あり |
| クラスター(ハウツー) | ソフト | テーブル内ボタン | ハード | あり |
| ブローカー比較(pSEO) | なし(結論ファーストで代替) | テーブル内ボタン | 2社並列ボタン | あり |
| 計算ツール | なし | ツール後の自然導線 | ハード | なし(ツール操作を妨げない) |
| 通貨ペア(pSEO) | なし | テーブル内ボタン | ハード | あり |
| 税金/副業(信頼系) | なし | なし or ソフトのみ | ソフト(控えめ) | なし |
| 法務ページ | なし | なし | なし | なし |

### 6-4. モバイルCTA実装仕様

```css
/* スティッキーCTA（モバイル専用） */
.sticky-cta {
  display: none;               /* デフォルト非表示 */
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: var(--navy);
  padding: 12px 16px;
  z-index: 1000;
  box-shadow: 0 -2px 10px rgba(0,0,0,0.15);
  /* 親指ゾーンに配置 */
  align-items: center;
  justify-content: space-between;
}

/* 50%スクロール後に表示（JSで制御） */
.sticky-cta.visible {
  display: flex;
}

/* 768px以上では非表示（PCは記事内CTAで十分） */
@media (min-width: 769px) {
  .sticky-cta { display: none !important; }
}
```

```javascript
// スティッキーCTA制御
(function() {
  const sticky = document.getElementById('stickyCta');
  if (!sticky) return;

  // 1セッション1回まで（閉じたら出さない）
  if (sessionStorage.getItem('sticky-cta-dismissed')) {
    sticky.remove();
    return;
  }

  const closeBtn = sticky.querySelector('.sticky-cta-close');
  closeBtn.addEventListener('click', function() {
    sticky.classList.remove('visible');
    sticky.setAttribute('aria-hidden', 'true');
    sessionStorage.setItem('sticky-cta-dismissed', '1');
  });

  // 50%スクロールで表示
  let shown = false;
  window.addEventListener('scroll', function() {
    if (shown) return;
    const scrollPct = window.scrollY / (document.body.scrollHeight - window.innerHeight);
    if (scrollPct > 0.5) {
      sticky.classList.add('visible');
      sticky.setAttribute('aria-hidden', 'false');
      shown = true;
    }
  }, { passive: true });
})();
```

---

## 7. 技術的SEO実装リスト

### 7-1. 構造化データ一覧（JSON-LD）

| スキーマタイプ | 使用ページ | 目的 |
|---|---|---|
| WebSite | index.html のみ | サイト全体の識別。sitelinks検索ボックス候補 |
| Article | 全記事ページ | 検索結果でのリッチスニペット |
| BreadcrumbList | 全ページ（法務除く） | パンくずのリッチ結果 |
| FAQPage | FAQ付き記事全て | FAQ リッチスニペット。検索結果面積の拡大 |
| HowTo | 手順系記事(口座開設/VPS設定/EA設定等) | ステップ表示のリッチ結果 |
| SoftwareApplication | 計算ツール全ページ | ツールのリッチ結果 |
| FinancialProduct | ブローカー比較/通貨ペアページ | 金融商品としての認識 |
| ItemList | ランキング/比較ページ | リスト表示のリッチ結果 |
| AboutPage | about.html | E-E-A-T: 運営者情報 |
| SpeakableSpecification | 全記事ページ | AI音声検索・AI Overview対応 |

### 7-2. Core Web Vitals最適化チェックリスト

| 指標 | 目標 | 実装手段 |
|---|---|---|
| LCP (Largest Contentful Paint) | < 2.5s | 画像はWebP + width/height明示 + loading="lazy"。CSSはインライン化不要(小さいため)。フォントはfont-display:swap + セルフホスト |
| INP (Interaction to Next Paint) | < 200ms | vanilla JS(フレームワークなし)。イベントハンドラにpassive:true。計算処理はrequestIdleCallback使用 |
| CLS (Cumulative Layout Shift) | < 0.1 | 全img/iframeにwidth/height。広告バナーは固定サイズのコンテナ内。フォントはfallback指定 |

### 7-3. メタタグチェックリスト（全ページ必須）

```
- [ ] <title> 30-60文字。KW前方配置。「｜FXコンパス」で終わる
- [ ] <meta name="description"> 80-120文字。KW含む。行動喚起を含む
- [ ] <link rel="canonical"> 正規URLを指定。末尾スラッシュの統一
- [ ] <meta property="og:type"> article(記事) / website(トップ)
- [ ] <meta property="og:title"> titleと同じ or 短縮版
- [ ] <meta property="og:description"> descriptionと同じ
- [ ] <meta property="og:url"> canonicalと同じ
- [ ] <meta property="og:image"> 1200x630のOGP画像
- [ ] <meta name="twitter:card"> summary_large_image
- [ ] JSON-LD Article (記事ページ)
- [ ] JSON-LD BreadcrumbList (全ページ)
- [ ] JSON-LD FAQPage (FAQ付きページ)
- [ ] JSON-LD SpeakableSpecification (全記事ページ)
- [ ] robots: noindex指定なし（法務ページ含む全公開）
```

### 7-4. 内部リンク戦略

```
ルール:
1. クラスター -> ピラー: 必須。本文中にアンカーテキスト（ピラーのターゲットKW）で1回以上
2. ピラー -> クラスター: 必須。クラスターリンクセクションで全クラスターへ
3. クラスター間: 関連があれば。同一ピラー内を優先
4. ピラー間: 「他のガイド」セクションで相互リンク
5. 計算ツール -> 関連記事: 「この計算に関連する記事」
6. 記事 -> 計算ツール: 文脈に合う箇所で自然にリンク
7. 全ページ -> トップ: パンくずで担保
8. 1ページあたりの内部リンク: 10-30本（150本以下のGoogleガイドライン内）
```

### 7-5. サイト内検索（将来実装）

現時点では不要（95ページ規模では目次+カテゴリナビで十分）。
120ページを超えた段階で、以下の軽量実装を検討:
- Pagefind（静的サイト向け全文検索。ビルド時にインデックス生成。CDNゼロ）
- またはlunr.js（クライアントサイド検索。JSONインデックス）

---

## 8. プログラマティックSEO用 生成スクリプト設計

### 8-1. アーキテクチャ

```
data/
  brokers.json          -- ブローカーのスペックデータ
  currency-pairs.json   -- 通貨ペアのデータ
  tools-meta.json       -- 計算ツールのメタデータ

templates/
  broker-vs.html        -- XX vs YY テンプレート
  currency-pair.html    -- 通貨ペアテンプレート
  tool-page.html        -- 計算ツールテンプレート

generate_pages.py       -- テンプレート + データ -> HTML生成
```

### 8-2. generate_pages.py の設計

```python
#!/usr/bin/env python3
"""
generate_pages.py -- プログラマティックSEOページの生成

テンプレートHTMLとJSONデータから、ブローカー比較・通貨ペア・ツールページを生成。
既存のpublish.pyの仕組み（テンプレート変数の置換）と互換性を保つ。

使い方:
  python3 generate_pages.py                     # 全ページ生成
  python3 generate_pages.py --type broker-vs    # ブローカー比較のみ
  python3 generate_pages.py --type currency     # 通貨ペアのみ
  python3 generate_pages.py --dry-run           # 生成ファイル一覧のみ表示
"""

import json
import itertools
from pathlib import Path
from datetime import date

ROOT = Path(__file__).resolve().parent
DATA = ROOT / "data"
TEMPLATES = ROOT / "templates"
OUTPUT_GUIDE = ROOT / "guide"
OUTPUT_CURRENCY = ROOT / "guide" / "currency"
OUTPUT_TOOLS = ROOT / "tools"


def load_json(name):
    return json.loads((DATA / name).read_text(encoding="utf-8"))


def render_template(template_path, variables):
    """テンプレートHTML内の {variable_name} を置換"""
    text = template_path.read_text(encoding="utf-8")
    for key, value in variables.items():
        text = text.replace("{" + key + "}", str(value))
    return text


def generate_broker_vs():
    """ブローカー比較ページ (XX vs YY) を生成"""
    brokers = load_json("brokers.json")
    template = TEMPLATES / "broker-vs.html"
    today = date.today().isoformat()

    # 主要ブローカーの組み合わせ（初期は6組）
    priority_pairs = [
        ("dmmfx", "gmo"),
        ("dmmfx", "fxtf"),
        ("dmmfx", "sbi"),
        ("fxtf", "gmo"),
        ("gmo", "sbi"),
        ("dmmfx", "minnano"),
    ]

    generated = []
    for key_a, key_b in priority_pairs:
        a = brokers[key_a]
        b = brokers[key_b]
        slug = f"fx-hikaku-vs-{key_a}-{key_b}"
        variables = {
            "broker_a_name": a["name"],
            "broker_b_name": b["name"],
            "broker_a_spread": a["spread_usdjpy"],
            "broker_b_spread": b["spread_usdjpy"],
            "broker_a_min_unit": a["min_unit"],
            "broker_b_min_unit": b["min_unit"],
            "broker_a_pairs": str(a["pairs"]),
            "broker_b_pairs": str(b["pairs"]),
            "broker_a_affiliate_key": a.get("affiliate_key", ""),
            "broker_b_affiliate_key": b.get("affiliate_key", ""),
            "slug": slug,
            "date_published": today,
            "date_modified": today,
        }
        # 比較テーブルの各行を構築
        rows_html = build_comparison_rows(a, b)
        variables["comparison_rows"] = rows_html

        # 「こんな人に」の判定ロジック
        verdict_a, verdict_b = build_verdict(a, b)
        variables["verdict_a"] = verdict_a
        variables["verdict_b"] = verdict_b

        # AI要約の自動生成
        variables["ai_summary"] = (
            f"{a['name']}と{b['name']}の主な違いは最小取引単位です。"
            f"{a['name']}は{a['min_unit']}単位、"
            f"{b['name']}は{b['min_unit']}単位から取引可能です。"
        )

        html = render_template(template, variables)
        output = OUTPUT_GUIDE / f"{slug}.html"
        output.write_text(html, encoding="utf-8")
        generated.append(output)

    return generated


def generate_currency_pages():
    """通貨ペア個別ページを生成"""
    pairs = load_json("currency-pairs.json")
    template = TEMPLATES / "currency-pair.html"
    today = date.today().isoformat()

    OUTPUT_CURRENCY.mkdir(exist_ok=True)
    generated = []

    for key, pair in pairs.items():
        variables = {
            "pair_code": pair["code"],
            "pair_name": pair["name"],
            "pair_description": pair["description"],
            "avg_spread": pair["avg_spread"],
            "avg_daily_range": pair["avg_daily_range"],
            "active_hours": pair["active_hours"],
            "characteristics": pair["characteristics"],
            "slug": key,
            "date_published": today,
            "date_modified": today,
        }
        # 各社スプレッド比較テーブル
        variables["broker_spreads_table"] = build_pair_broker_table(pair)
        # 関連通貨ペアリンク
        variables["related_pairs"] = build_related_pairs(key, pairs)

        html = render_template(template, variables)
        output = OUTPUT_CURRENCY / f"{key}.html"
        output.write_text(html, encoding="utf-8")
        generated.append(output)

    return generated


def build_comparison_rows(a, b):
    """比較テーブルの行HTMLを構築"""
    rows = []
    fields = [
        ("USD/JPYスプレッド", "spread_usdjpy"),
        ("最小取引単位", "min_unit"),
        ("通貨ペア数", "pairs"),
        ("スワップ(USD/JPY)", "swap_usdjpy"),
        ("取引ツール", "tools"),
        ("デモ口座", "demo"),
    ]
    for label, key in fields:
        val_a = str(a.get(key, "要確認"))
        val_b = str(b.get(key, "要確認"))
        if isinstance(a.get(key), bool):
            val_a = "あり" if a[key] else "なし"
        if isinstance(b.get(key), bool):
            val_b = "あり" if b[key] else "なし"
        rows.append(f"<tr><th>{label}</th><td>{val_a}</td><td>{val_b}</td></tr>")
    return "\n".join(rows)


def build_verdict(a, b):
    """結論テキストを自動生成"""
    verdict_a = []
    verdict_b = []
    # 最小取引単位で判定
    if "1,000" in a.get("min_unit", "") or "1通貨" in a.get("min_unit", ""):
        verdict_a.append("少額から始めたい初心者")
    else:
        verdict_b.append("少額から始めたい初心者")
    # スプレッドで判定（簡易）
    verdict_a.append(f"スプレッド{a.get('spread_usdjpy', '')}で取引コストを重視する人")
    return "<li>" + "</li><li>".join(verdict_a) + "</li>", \
           "<li>" + "</li><li>".join(verdict_b) + "</li>"


def build_pair_broker_table(pair):
    """通貨ペアページの各社スプレッド比較テーブルHTML"""
    # 実装は brokers.json から該当ペアのスプレッドを引く
    return "<!-- brokers.jsonから動的に生成 -->"


def build_related_pairs(current_key, all_pairs):
    """関連通貨ペアリンクHTML"""
    links = []
    for key, pair in all_pairs.items():
        if key != current_key:
            links.append(f'<li><a href="{key}.html">{pair["name"]}({pair["code"]})</a></li>')
    return "\n".join(links[:5])  # 最大5件


if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="プログラマティックSEOページ生成")
    parser.add_argument("--type", choices=["broker-vs", "currency", "all"],
                        default="all", help="生成するページタイプ")
    parser.add_argument("--dry-run", action="store_true", help="生成せずファイル一覧のみ表示")
    args = parser.parse_args()

    generated = []
    if args.type in ("broker-vs", "all"):
        generated += generate_broker_vs()
    if args.type in ("currency", "all"):
        generated += generate_currency_pages()

    print(f"生成完了: {len(generated)}ページ")
    for f in generated:
        print(f"  {f.relative_to(ROOT)}")
```

### 8-3. データファイル（brokers.json）の構造

```json
{
  "dmmfx": {
    "name": "DMM FX",
    "company": "株式会社DMM.com証券",
    "registration": "関東財務局長(金商)第1629号",
    "spread_usdjpy": "0.2銭",
    "spread_eurjpy": "0.4銭",
    "spread_gbpjpy": "0.9銭",
    "min_unit": "10,000通貨",
    "pairs": 21,
    "swap_usdjpy": "要公式確認",
    "tools": "DMMFX PLUS / スマホアプリ",
    "demo": true,
    "affiliate_key": "dmmfx",
    "strengths": [
      "業界最狭水準のスプレッド",
      "LINEでの問い合わせ対応",
      "取引ツールの直感的なUI"
    ],
    "weaknesses": [
      "最小取引単位が10,000通貨（少額取引不向き）",
      "スキャルピングは公式には非推奨"
    ],
    "best_for": "スプレッド重視でコストを抑えたい人",
    "official_url": "https://fx.dmm.com/"
  },
  "fxtf": {
    "name": "FXTF（ゴールデンウェイ・ジャパン）",
    "company": "ゴールデンウェイ・ジャパン株式会社",
    "registration": "関東財務局長(金商)第258号",
    "spread_usdjpy": "0.1銭",
    "spread_eurjpy": "0.3銭",
    "min_unit": "1,000通貨",
    "pairs": 30,
    "swap_usdjpy": "要公式確認",
    "tools": "MT4 / GX(独自)",
    "demo": true,
    "affiliate_key": "fxtf",
    "strengths": [
      "業界最狭のスプレッド（USD/JPY 0.1銭）",
      "MT4対応（EA・自動売買が可能）",
      "1,000通貨から取引可能"
    ],
    "weaknesses": [
      "知名度がDMM FXほどではない"
    ],
    "best_for": "MT4を使いたい人・スプレッド最狭を求める人",
    "official_url": "https://www.fxtrade.co.jp/"
  }
}
```

### 8-4. currency-pairs.json の構造

```json
{
  "usdjpy": {
    "code": "USD/JPY",
    "name": "米ドル/円",
    "description": "世界で最も取引量の多い通貨ペアの一つ。日本人トレーダーに最も人気があり、情報量も豊富。",
    "avg_spread": "0.2銭",
    "avg_daily_range": "80-120pips",
    "active_hours": "東京市場(9-15時)・NY市場(22-翌6時)",
    "characteristics": "米国の経済指標（雇用統計・FOMC）と日銀政策に大きく反応。トレンドが出やすい。",
    "related": ["eurjpy", "gbpjpy", "eurusd"],
    "brokers": {
      "dmmfx": "0.2銭",
      "fxtf": "0.1銭",
      "gmo": "0.2銭原則固定",
      "sbi": "0.18銭"
    }
  }
}
```

---

## 9. 実装ロードマップ（タスク分解）

### Phase 1: 基盤構築（1-2週間）

| # | タスク | 粒度 | 依存 |
|---|---|---|---|
| T1 | brokers.json / currency-pairs.json のデータ整備 | 2h | なし |
| T2 | 5本のピラーページ作成（fx-kouza-hikaku, fx-jidou-baibai, fx-chart-bunseki, fx-hajimekata改修, fx-fukugyou改修） | 2h x 5 = 10h | なし |
| T3 | 既存15ページのtitle/description/構造化データ全面改修 | 4h | なし |
| T4 | CTA配置コンポーネント（cta-soft/medium/hard/sticky）のCSS+JS実装 | 3h | なし |
| T5 | スティッキーCTAのJS実装（50%スクロール検知・sessionStorage制御） | 1h | T4 |
| T6 | sitemap.xmlの全URL更新 | 1h | T2,T3 |
| T7 | publish.pyの拡張（新ディレクトリ対応） | 1h | T2 |

### Phase 2: クラスター記事量産（3-6週間）

| # | タスク | 粒度 | 依存 |
|---|---|---|---|
| T8 | ピラー1クラスター（口座比較系18記事）| 1.5h x 18 = 27h | T2,T4 |
| T9 | ピラー2クラスター（VPS/EA系14記事）| 1.5h x 14 = 21h | T2,T4 |
| T10 | ピラー3クラスター（チャート分析系12記事）| 1.5h x 12 = 18h | T2,T4 |
| T11 | ピラー4クラスター（初心者系12記事）| 1.5h x 12 = 18h | T2,T4 |
| T12 | ピラー5クラスター（税金系8記事）| 1.5h x 8 = 12h | T2,T4 |

### Phase 3: pSEO + ツール（2-3週間）

| # | タスク | 粒度 | 依存 |
|---|---|---|---|
| T13 | generate_pages.pyの実装 | 3h | T1 |
| T14 | ブローカー比較テンプレート + 6ページ生成 | 2h | T1,T13 |
| T15 | 通貨ペアテンプレート + 10ページ生成 | 2h | T1,T13 |
| T16 | 計算ツール7本の実装（ロット/利益/スワップ/証拠金/pips/税金/RR） | 2h x 7 = 14h | T4 |
| T17 | 全ページのcheck_links.py検証 + 修正 | 2h | T8-T16 |

### Phase 4: 品質向上（継続）

| # | タスク | 粒度 | 依存 |
|---|---|---|---|
| T18 | 全ページのCore Web Vitals計測・修正 | 4h | T17 |
| T19 | 残りのブローカー比較ページ(+22ページ) | 1h x 22 = 22h | T14 |
| T20 | Google Search Console登録・インデックス確認 | 1h | T17 |
| T21 | 内部リンクの総点検・強化 | 3h | T17 |

### 総工数の見積もり

| Phase | 工数 | 期間目安 |
|---|---|---|
| Phase 1: 基盤 | 22h | 1-2週間 |
| Phase 2: クラスター | 96h | 3-6週間 |
| Phase 3: pSEO+ツール | 23h | 2-3週間 |
| Phase 4: 品質 | 30h | 継続 |
| **合計** | **171h** | **8-12週間** |

---

## 10. 内部リンク構造図

```
                         index.html (トップ)
                              |
          ┌───────┬───────┬────┴────┬───────┐
          |       |       |         |       |
       [P1]    [P2]    [P3]      [P4]    [P5]
      口座比較  自動売買  チャート   初心者   副業税金
       /|\      /|\      /|\      /|\      /|\
      / | \    / | \    / | \    / | \    / | \
   C1-1 ... C2-1 ... C3-1 ... C4-1 ... C5-1 ...
   C1-2     C2-2     C3-2     C4-2     C5-2
   ...      ...      ...      ...      ...

   ← → ピラー間相互リンク
   ← → クラスター間（同一ピラー内）
   ← → クラスター間（ピラー横断、関連性がある場合）

   [ツール群] ←→ 関連する記事（例: ロット計算機 ← レバレッジ記事）
   [pSEO比較] → P1(口座比較ピラー)
   [pSEO通貨] → P1(口座比較) + P3(チャート分析)

   全ページ → about.html (フッタ)
   全ページ → legal/* (フッタ)
```

---

## 11. 収益化のための優先順位

### 最も早く収益化できるページ（優先度A = 最初に作る）

1. **fx-kouza-hikaku.html**（ピラー1）-- 全案件への入口
2. **kouza-ranking.html**（改修）-- 検索ボリュームが最大
3. **spread-hikaku.html**（改修）-- FXTF訴求
4. **fx-hajimekata.html**（改修）-- ドメイン名と完全一致
5. **fx-kouza-kaisestu-tejun.html**（新規）-- 口座開設直前の検索意図
6. **dmm-fx-kuchikomi.html**（新規）-- 商標KWで指名検索を拾う

### 高単価だが時間がかかるページ（優先度B = Phase 2で作る）

7. **fx-vps-hikaku.html**（改修）-- ConoHa 5万円/件
8. **conoha-vps-fx-setup.html**（新規）-- 具体的な設定手順
9. **ea-hajimekata.html**（改修）-- EA導入の入口
10. **tradingview.html**（改修）-- 継続報酬30%

### 信頼構築ページ（優先度C = Phase 2後半）

11. **kakutei-shinkoku.html**（改修）-- 税金系は信頼性に直結
12. **fx-fukugyou-kaishain.html**（新規）-- 副業会社員の指名検索
13. **fx-risk-kanri.html**（新規）-- 信頼構築

---

## 12. KPI管理

### 検索パフォーマンス（Google Search Console）

| 指標 | 1か月後 | 3か月後 | 6か月後 |
|---|---|---|---|
| インデックス済みページ数 | 50+ | 95+ | 120+ |
| 表示回数/月 | 5,000 | 50,000 | 200,000 |
| クリック数/月 | 100 | 5,000 | 30,000 |
| 平均掲載順位 | 40位 | 20位 | 10位 |

### 収益（アフィリエイト）

| 指標 | 1か月後 | 3か月後 | 6か月後 | 12か月後 |
|---|---|---|---|---|
| 月間PV | 1,000 | 10,000 | 40,000 | 60,000+ |
| アフィリクリック数 | 50 | 500 | 2,000 | 3,000+ |
| 成約件数 | 0-1 | 5-10 | 20-30 | 40-50 |
| 月間収益 | 0-2万円 | 5-15万円 | 30-60万円 | 80-100万円 |

仮定: 新規ドメインのSEO効果発現は3-6か月。YMYL（Your Money Your Life）領域はE-E-A-T評価が厳しく時間がかかる。上記は楽観シナリオではなく、質の高いコンテンツを継続投入した場合の実績ベースの目安。
