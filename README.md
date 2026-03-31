# Choreia Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/使ってみる-GitHub%20Pages-brightgreen)](https://choreia.github.io/Guide/)

**社内ルールについて質問するだけ。AIがスプレッドシートから回答。**

Googleスプレッドシートに書かれた社内ルールをもとに、AIが社員の質問に回答します。不確定な回答は自動でシートに蓄積され、管理者が正解を入力することでFAQとして育ちます。

**[使ってみる](https://choreia.github.io/Guide/)**

## 使い方

1. 「Googleでログイン」をタップ（組織のGoogleアカウント）
2. 初回のみ：管理者がルール集スプレッドシートを設定
3. 質問を入力するだけでAIが回答

## 特徴

- **スプレッドシートがそのままナレッジベース** — 既存のルール集をそのまま使える。新しいツールを覚える必要なし
- **AIが自動回答** — Geminiがルール集の内容をもとに回答。確信度も表示
- **育てるFAQ** — AIが確信を持てなかった回答は自動でシートに蓄積。管理者が正解を入力すると、次回から確定回答として使用
- **マルチテナント** — ドメイン単位で組織を分離。同じドメインのメンバーは同じルール集を共有
- **管理者機能** — スプレッドシートの変更、管理者の追加/削除
- **完全無料** — オープンソース（MIT）、サーバー不要

## アーキテクチャ

```
社員（ブラウザ）
    │
    ├── Googleログイン（OAuth）
    │
    ├── 共有ドライブの設定ファイル（choreia-guide-config.json）
    │   → ドメイン単位のマルチテナント
    │
    ├── Google Sheets API → ルール集スプレッドシートの全シートを読み取り
    │
    ├── 質問テキスト + ルール全文 → Gemini API → 回答 + 確信度
    │
    └── 不確定な回答 → Guide_QA シートに自動保存
        → 管理者が確定回答を入力 → 次回から確定回答として使用
```

- サーバー不要（GitHub Pages）
- AIはGoogleログインのOAuthトークンで利用（APIキー不要）
- データはすべてユーザーの組織のGoogle Driveに保存

## 関連プロジェクト

- [Choreia Expense](https://github.com/Choreia/Expense) — レシートAI自動仕訳
- [Choreia Photos](https://github.com/Choreia/Photos) — 写真をDriveに一括転送
- [Choreia Books](https://github.com/Choreia/Books) — 無料会計ソフト
- [Choreia Forms](https://github.com/Choreia/Forms) — 無料フォームビルダー

## ライセンス

[MIT](LICENSE)
