# SearXNG Gemini Summary

## 概要

SearXNGの検索結果ページに、Geminiによる概要を表示するユーザースクリプトです。

検索クエリと検索結果スニペットを収集し、Geminiが生成した情報を、検索結果上部に表示します。





## インストール方法

- 1.ブラウザに、いずれかのユーザースクリプトの拡張機能をインストールします。

  - **[Violentmonkey](https://violentmonkey.github.io/)**

  - **[Tampermonkey](https://www.tampermonkey.net/)**

- 2.下記リンクから、スクリプトをインストールします。

  - **[SearXNG Gemini Summary]()**

- 3.APIキーを入力

  - 初回検索時のみ、Gemini APIキーの入力が必要です。

  - **[Google AI Studio](https://aistudio.google.com/api-keys)** でAPIキーを取得してください。

## 対応サイト

- @match

  - *://*/searx/search*
 
  - *://*/searxng/search*
 
  - *://searx.*/*
 
  - *://*.searx.*/*
 
  - https://search.charleseroop.com/*
 
  - https://opnxng.com/*
 
  - http://127.0.0.1:8888/search*
 
  - http://localhost:8888/search*

- 利用するSearXNGインスタンスのURLによつては対応しない場合があります。

- その場合は .user.js 内の @match を修正してください。












## 動作機構

### 1.ページ判定

- SearXNGの検索ページか確認

### 2.APIをキー取得

- LocalStorageから暗号化キーを取得し、APIキーを復元
- 存在しなければ、ユーザーにAPIキーの入力を求める

### 3.検索クエリを取得

- input[name="q"] で取得

### 4.キャッシュ確認

- キャッシュに同じクエリがあるかチェック
  - あれば、キャッシュを表示して終了
  - ないければ、次へ

### 5.UIを構築

- 検索結果上部に「Geminiによる概要」を追加

### 6.スニペットを取得

- 最大(MAX_RESULTS)件まで取得
- 足りなければ、次のページ分のスニペットを取得
- 各検索結果から必要なテキストのみ取得

### 7.プロンプトを作成

- クエリ + スニペット + 概要の作成指示で構成されたプロンプトを作成
- JSON形式で出力を指定

### 8.Gemini API呼び出し

- プロンプトをGeminiに送信

### 9.JSON解析

- Geminiの応答からJSONを抽出
- JSONからHTMLに変形

### 10.概要表示

- 導入文・セクション・出典を整形して表示
- キャッシュを更新

- 処理終了














---

実装ポイント

fetch で Gemini API (generateContent) を呼び出し

検索結果スニペットを収集してプロンプトを生成

APIキーはAES-GCMで暗号化して localStorage に保存

ダークモードは matchMedia('(prefers-color-scheme: dark)') で判定

応答JSONをパースしてHTMLに整形

セクション・出典URL付きで表示

キャッシュ機能あり（sessionStorage、7日間有効）



---

関連リンク

Google Gemini API (PaLM) 公式ドキュメント

SearxNG GitHub

Violentmonkey

Tampermonkey



---

## ライセンス

MIT License
自由に改変・再配布可能ですが、使用は自己責任でお願いします。
