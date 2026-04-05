# Woolworths Price Tracker

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.jp)
[![Woolworths Price Tracker](https://img.shields.io/badge/Woolworths%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.jp/products/insights/price-tracker/woolworths)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.jp/products/insights/price-tracker/woolworths)

リアルタイムのWoolworths価格トラッキング - オーストラリア最大のスーパーマーケットチェーン。開始方法は2通りあります: **フルマネージド**のインテリジェンスプラットフォーム、またはBright DataのAI Scraper Builderで構築する**カスタムスクレイパー**です。

---

## Option 1: Bright Insights - AI搭載価格トラッキング（推奨）

**[Bright Insights](https://brightdata.jp/products/insights/price-tracker/woolworths)** は、Bright Dataのフルマネージドなリテールインテリジェンスプラットフォームです。スクレイパーの構築も、インフラの保守も不要で、構造化された分析対応の価格データをダッシュボード、データフィード、またはBIツールにそのまま配信できます。

**チームがBright Insightsを選ぶ理由:**
- 🚀 **セットアップ不要** - すぐに使えるダッシュボードとデータフィードで数分で本番稼働
- 🤖 **AI搭載レコメンデーション** - 対話型AIアシスタントが数百万のデータポイントを即座に実用的なインサイトへ変換
- ⚡ **リアルタイム監視** - 1時間ごとから日次までの更新頻度と即時アラート（email、Slack、webhook）
- 🌍 **無制限のスケール** - あらゆるWebサイト、あらゆる地域、あらゆる更新頻度に対応
- 🔗 **プラグアンドプレイ統合** - AWS、GCP、Databricks、Snowflake など
- 🛡️ **フルマネージド** - スキーマ変更、サイト更新、データ品質をBright Dataが自動で処理

**主なユースケース:**
- ✅ Woolworthsのカテゴリ横断で**食料品価格インフレを追跡**
- ✅ **プロモーション**や週間セールを自動監視
- ✅ バスケット分析のための**価格履歴データベースを構築**
- ✅ MAPポリシー準拠を監視し、価格違反を検出
- ✅ 競合のプロモーションと販促動向を追跡
- ✅ クリーンで正規化されたデータを動的価格設定アルゴリズムやAIモデルへ直接投入

> **月額$250から - [お客様向け見積もりを取得 →](https://brightdata.jp/products/insights/price-tracker/woolworths)**

---

## Option 2: 独自のWoolworthsスクレイパーを構築

Woolworths向けの事前構築済みスクレイパーAPIがない？問題ありません。Bright Dataの**AI Scraper Builder**なら、数クリックでカスタムWoolworthsスクレイパーを生成できます — コーディングは不要です。

### 数分でWoolworthsスクレイパーを構築

**[Woolworths AI Scraper Builderを開く →](https://brightdata.jp/products/web-scraper/woolworths)**

ドメインを選択し、必要なデータ要件を記述するだけで、AIスクレイパービルダーが自動的にAPIを作成します。

1. **必要なデータを平易な英語で記述**
2. **AIが即座にスクレイパーAPIを生成**
3. **APIリクエストを実行してすぐに結果を取得**
4. 必要に応じて**組み込みIDEでコードを編集**

構築が完了すると、スクレイパーには**Web Scraper ID**（`gd_xxxxxxxxxxxx`）が付与されます — 以下のセットアップ手順で使用するためにコピーしてください。

### 前提条件

- Python 3.9 以上
- [Bright Data account](https://brightdata.jp)（無料トライアルあり）
- Bright Dataの**API token**（[取得方法](https://docs.brightdata.jp/general/account/account-settings#api-token)）
- Woolworths用の**Web Scraper ID**（上記の構築手順で取得）

### セットアップ

1. **このrepositoryをclone**

   ```bash
   git clone https://github.com/bright-jp/woolworths-price-tracker.git
   cd woolworths-price-tracker
   ```

2. **依存関係をインストール**

   ```bash
   pip install -r requirements.txt
   ```

3. **認証情報を設定**

   `.env.example` を `.env` にコピーし、値を入力します:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Your Web Scraper ID**
   > [AI Scraper Builder dashboard](https://brightdata.jp/products/web-scraper/woolworths) のWeb Scraper IDを
   > `BRIGHTDATA_DATASET_ID` に貼り付けてください（形式: `gd_xxxxxxxxxxxx`）。

---

## 使用方法

Woolworthsスクレイパーの構築が完了し、Web Scraper IDが `.env` に設定されると、Pythonインターフェースは同じ方法で利用できます。

### 1. URLで特定の商品を追跡

Woolworthsの商品URLのリストを渡して、構造化された価格データを取得します:

```python
from price_tracker import track_prices

urls = [
    "https://www.woolworths.com.au/products/sample-product",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

または直接実行:

```bash
python price_tracker.py
```

### 2. キーワードで商品を検索

キーワード検索に一致する商品を見つけます:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. カテゴリURLで商品を閲覧

Woolworthsのカテゴリページからすべての商品を収集します:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://woolworths.com.au/category/example",
    limit=100,
)
```

---

## 出力フィールド

各結果レコードには次のフィールドが含まれます:

| Field | Description |
|-------|-------------|
| `url` | 商品ページURL |
| `name` | 商品名 |
| `brand` | ブランド |
| `price` | 現在価格 |
| `currency` | 通貨コード |
| `unit_price` | 単位/重量あたりの価格 |
| `in_stock` | 在庫状況 |
| `category` | 商品カテゴリ |
| `sku` | SKU / バーコード |
| `images` | 商品画像URL |
| `description` | 商品説明 |
| `timestamp` | 収集タイムスタンプ |

### 出力例

```json
[
  {
    "url": "https://www.woolworths.com.au/products/sample-product",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://woolworths.com.au/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## 高度なオプション

`trigger_collection()` 関数は、データ収集を制御するためのオプションパラメータを受け付けます:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 返されるレコードの最大数 |
| `include_errors` | boolean | `true` | 結果にエラーレポートを含める |
| `notify` | string (URL) | - | スナップショットの準備完了時に呼び出すWebhook URL |
| `format` | string | `json` | 出力形式: `json`、`csv`、または `ndjson` |

オプション付きの例:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.woolworths.com.au/products/sample-product"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## リソース

- 🌟 [Woolworths Price Tracker - Bright Insights (Managed)](https://brightdata.jp/products/insights/price-tracker/woolworths)
- 🏗️ [Build a Woolworths Scraper](https://brightdata.jp/products/web-scraper/woolworths)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.jp/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.jp/cp/scrapers)
- 🔑 [How to get an API token](https://docs.brightdata.jp/general/account/account-settings#api-token)
- 🌐 [Bright Data Homepage](https://brightdata.jp)

---

*[Bright Data](https://brightdata.jp) を使用して構築 - 業界をリードするWebデータプラットフォーム。*