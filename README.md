SearXNG Gemini Summary

概要

SearXNGの検索結果ページに、Google Gemini のAIによる簡潔な概要を表示するユーザースクリプトです。
検索クエリと検索結果スニペットをもとにGeminiが生成した情報を、検索結果上部に自然に表示します。

APIキーはローカルストレージに保存、再入力可

ダークモードに対応

検索結果最上部に表示



---

インストール方法

1. ブラウザに Violentmonkey または Tampermonkey をインストール


2. 下記リンクからスクリプトをインストール
SearXNG Gemini Summary


3. 初回使用時に Gemini APIキー の入力が必要
Google AI StudioでAPIキーを取得




---

主な機能

検索クエリを自動取得してGeminiに送信

GeminiのHTML形式の回答を検索結果上部に表示

APIキーを暗号化してローカルに保存

APIキーの再入力・変更に対応

fetchを利用してCORSやGM_系grant不要



---

対応サイト

// @match        *://*/searx/search*
// @match        *://*/searxng/search*
// @match        *://searx.*/*
// @match        *://*.searx.*/*
// @match        https://search.charleseroop.com/*
// @match        https://opnxng.com/*
// @match        http://127.0.0.1:8888/search*
// @match        http://localhost:8888/search*

⚠️ 利用するSearXNGインスタンスによりマッチしない場合があります。その場合は .user.js 内の @match を修正してください。


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

ライセンス

MIT License
自由に改変・再配布可能ですが、使用は自己責任でお願いします.


---

SearXNGの検索結果をGeminiで即時強化。検索クエリに対して信頼できる情報を簡潔に表示します。

