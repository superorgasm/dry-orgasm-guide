# dry-orgasm-guide

購入者向けガイドサイトを `src/` から `docs/` にビルドし、各HTMLをパスワード保護して配布するためのリポジトリです。

## 前提

1. Node.js 18 以上をインストールする
2. リポジトリ直下で依存をインストールする

```bash
npm install
```

## 運用手順（手順重視）

### 1) コンテンツを更新する

- 元データは `src/` 配下を編集します
  - トップ: `src/index.html`
  - 下層ページ: `src/pages/*.html`
  - スタイル: `src/css/style.css`

### 2) パスワード付きでビルドする

> パスワードは履歴・チケット・PR本文に書かず、環境変数やシークレット経由で扱ってください。

方法A（推奨: 環境変数）

```bash
STATICRYPT_PASSWORD='<your-password>' npm run build
```

方法B（引数）

```bash
npm run build -- '<your-password>'
```

### 3) 生成物を確認する

- ビルド後に `docs/` が再生成されます
- 暗号化対象
  - `docs/index.html`
  - `docs/pages/audio.html`
  - `docs/pages/items.html`
  - `docs/pages/links.html`

### 4) 差分を確認してコミットする

```bash
git status
git diff -- docs src README.md
```

必要な変更のみをコミットしてください。

## ビルドの挙動

`build.js` は以下を実行します。

1. `docs/` を削除
2. `src/` を `docs/` にコピー（テンプレートやローカル画像は除外）
3. HTML 内の `cover-image.jpg` 参照を外部URLへ置換
4. `staticrypt` で各HTMLを個別に暗号化

## よく使うコマンド

```bash
npm run build -- '<your-password>'
```

```bash
git status
```
