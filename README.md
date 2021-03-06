# PoSo's Note
サイト: https://posonote.com/

## microcms-blogからclone
クローン元サイト: https://blog.microcms.io  
github: https://github.com/wantainc/microcms-blog  
このソフトウェアは、 [Apache 2.0ライセンス](https://www.apache.org/licenses/LICENSE-2.0.html)で配布されている製作物が含まれています。

## 機能
- 記事一覧
- カテゴリー別記事一覧
- 人気の記事一覧
- 最新の記事一覧
- 検索
- パンくずリスト
- 記事詳細
  - 目次
  - **リッチテキスト・囲み枠・HTML同時入稿** *←Changes*
  - 著者
  - SNSシェアボタン
  - 下書きプレビュー
  - 関連記事
- **問い合わせフォーム** *←Changes*
- サイトマップ
- バナー
- Google Analytics
- RSS
- PWA

## 技術構成
- Nuxt（SSG）
- microCMS（コンテンツ）
- Netlify（Hosting, Functions）
- ESLint
- Prettier
- PostCSS
- PWA

## microCMSのAPIスキーマ設定
### ブログ
endpoint: blog  
type: リスト形式

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| title | タイトル | テキストフィールド |
| category | カテゴリー | コンテンツ参照 - カテゴリー |
| introduction | 前置き文 | 繰り返し -3件のフィールド[1](#1-カスタムフィールド-Changes) | *←Changes*
| toc_visible | 目次 | 真偽値 |
| body | 本文 | 繰り返し -3件のフィールド[1](#1-カスタムフィールド-Changes) | *←Changes*
| description | 概要 | テキストフィールド |
| ogimage | OGP画像 | 画像 |
| writer | 著者 | コンテンツ参照 - 著者 |
| ~~partner~~ | ~~パートナー~~ | ~~コンテンツ参照 - パートナー~~ |
| related_blogs | 関連記事 | 複数コンテンツ参照 - ブログ |

#### [1]: カスタムフィールド *←Changes*
カスタムフィールド名: リッチエディタ  
カスタムフィールドID: richEditor

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| text | リッチエディタ | リッチエディタ |

カスタムフィールド名: 色付き囲み枠  
カスタムフィールドID: frame

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| color | 色 | セレクトフィールド |
| title | 枠のタイトル | テキストフィールド |
| list | 枠のリスト | リッチエディタ |

カスタムフィールド名: HTML  
カスタムフィールドID: html

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| text | HTML | テキストエリア |

参照: [microcms-blog:リッチエディタを使いつつ一部はHTMLで入稿する](https://blog.microcms.io/input-richeditor-and-html "microcms-blog")

### 著者
endpoint: authors  
type: リスト形式

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| name | 名前 | テキストフィールド |
| text | 自己紹介 | テキストエリア |
| image | 画像 | 画像 |

### カテゴリー
endpoint: categories  
type: リスト形式

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| name | 名前 | テキストフィールド |

### ~~パートナー~~
~~endpoint: partners~~  
~~type: リスト形式~~

| ~~フィールドID~~ | ~~表示名~~ | ~~種類~~ |
| ------------- | ------------- | ----- |
| ~~company~~ | ~~会社名~~ | ~~テキストフィールド~~ |
| ~~url~~ | ~~会社URL~~ | ~~テキストフィールド~~ |
| ~~description~~ | ~~説明文~~ | ~~テキストエリア~~ |
| ~~logo~~ | ~~ロゴ~~ | ~~画像~~ |

### 人気の記事
endpoint: popular-articles  
type: オブジェクト形式

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| articles | 人気の記事 | 複数コンテンツ参照 - ブログ |

### バナー
endpoint: banner  
type: オブジェクト形式

| フィールドID | 表示名 | 種類 |
| ------------- | ------------- | ----- |
| image | 画像 | 画像 |
| url | リンク先URL | テキストフィールド |
| alt | 代替テキスト | テキストフィールド |

## 環境変数
プロジェクトルートに`.env`ファイルを作成し、以下の項目を設定してください。
- API_KEY（microCMSのAPIキー）
- SERVICE_ID（microCMSのサービスID）
- GA_ID（Google AnalyticsのID）  
***↓Changes***
- USER (メールアドレス)
- PASSWORD (メールアドレスのパスワード)

例:
```
API_KEY=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
SERVICE_ID=your-service-id
GA_ID=UA-xxxxxxxxx-x
  ↓Changes
USER=ユーザ名@ドメイン名
PASSWORD=パスワード
```

## 開発方法

```bash
# パッケージをインストール
$ npm install

# 開発サーバーを起動（localhost:3000）
$ npm run dev

# Netlify Functionsをローカルで起動（localhost:9000）
$ npm run functions:serve

# アプリケーションを静的生成
$ npm run generate

# 静的生成したアプリケーションを起動
$ npm start
```

## ライセンス
Apache License 2.0
