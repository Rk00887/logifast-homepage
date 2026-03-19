# Devlog — ロジファスト ホームページ再現プロジェクト

## 概要

WordPress（Avada テーマ）で構築された [logifast.jp](https://logifast.jp/) のトップページを、WordPress なしの **純粋な HTML + CSS + JavaScript** の単一ファイルとして再現するプロジェクト。

---

## 2026-03-19

### Phase 1 — WordPress XML の解析

**作業内容：**
- WordPress エクスポートファイル（`ec.WordPress.2026-03-19.xml`、5.4MB）を取得
- ファイル構造を解析：WXR 1.2 形式、Avada Fusion Builder ショートコードで構成されていることを確認
- サイト基本情報を抽出：
  - サイト名：EC通販の発送代行・物流代行・物流アウトソーシングなら横浜のロジファスト株式会社
  - URL：https://logifast.jp
  - 作成者：KIN CHIN（kin@shinpur.jp）

**発見した主要ページ：**
- よくある質問（FAQ）：EC物流代行・FBA納品代行・オリジナルダンボール・名入れギフトの4カテゴリ
- 特長、サービスメニュー、事例、会社概要、料金 など

---

### Phase 2 — ベースHTML の構築

**作業内容：**
- 単一ファイル `index.html` として初期ホームページを構築
- 実サイトのカラーパレットを再現：
  ```css
  --blue:   #009fe3
  --navy:   #3d66ae
  --dark:   #222222
  --gray:   #4f4f4f
  --lgray:  #f2f3f5
  --lblue:  #f5fcff
  --border: #e2e2e2
  ```
- 使用フォント：Noto Sans JP（Google Fonts）
- 実装セクション：Header / Hero / Intro / Problems / Features / Services / Products / Integrations / Credentials / Testimonials / Cases / Pricing / Flow / FAQ / Contact / Footer

---

### Phase 3 — WordPress XML からコンテンツ抽出・反映

**作業内容：**
- XML の `[fusion_toggle]`・`[fusion_text]` ショートコードからテキストを抽出
- FAQ を 5件 → **40件超**（11カテゴリ）に拡充
- 実サイトのサービス説明文・会社説明文を正確なテキストに差し替え
- 実績数値を XML 実データに修正

**主な修正：**
| 項目 | 修正前 | 修正後 |
|------|--------|--------|
| 誤出荷率 | 0.007%（誤） | 0.0013%以下（正） |
| 会社紹介文 | 汎用テキスト | XML の実際のミッション文 |
| FAQ件数 | 5件 | 40件超 |

---

### Phase 4 — 実サイト HTML ソースとの照合・全面更新

**作業内容：**
- https://logifast.jp/ の実際のページソースを取得・解析（623行）
- Avada テーマの HTML 構造からテキスト・画像 URL を抽出
- `index.html` を実サイトに完全一致するよう全面更新

**更新内容詳細：**

| セクション | 変更内容 |
|-----------|---------|
| ヒーロー背景 | `20241227-160516.jpg` → `mvBg.png` |
| 会社紹介見出し | 「中堅・中小企業バックアップ」 → 「売上アップする EC物流・発送代行とは？」 |
| お悩みカード | 6項目 → 12項目 |
| 8つの特長 | 全説明文を実サイトの詳細テキストに差し替え |
| 取り扱い商品 | 6種 → 16種（URLも正番号に修正） |
| 実績（Credentials） | 創業12年以上・3,651㎡・0.0013%以下 |
| お客様の声 | 3件 → 6件（実サイトの実際の声） |
| 導入事例画像 | `case-study-04` のみ → 04 / 06 / 07 に差し替え |
| フォームの流れ | 電話番号 045-315-5250 追加 |
| フッターナビ | 3列 → 4列（対応可能な業務 11項目追加） |

---

### Phase 5 — GitHub へのアップロード

**作業内容：**
```bash
git init
git add index.html
git commit -m "feat: logifast homepage initial build"
git remote add origin https://github.com/Rk00887/logifast-homepage.git
git push -u origin master
```

**リポジトリ：** https://github.com/Rk00887/logifast-homepage

---

## 技術スタック

| 種別 | 内容 |
|------|------|
| HTML | セマンティック HTML5、単一ファイル構成 |
| CSS | CSS カスタムプロパティ、Flexbox、CSS Grid、レスポンシブ対応 |
| JavaScript | バニラ JS（FAQ トグル・スムーズスクロール・トップボタン） |
| フォント | Google Fonts / Noto Sans JP |
| 画像 | logifast.jp WordPress CDN を直接参照 |
| ホスティング | GitHub / GitHub Pages 対応 |

---

## ファイル構成

```
logifast-homepage/
└── index.html   # 全コード（CSS・JS含む）を内包した単一ファイル
```

---

## 今後の課題

- [ ] お問い合わせフォームのバックエンド連携
- [ ] ヒーローセクションのスライダー実装
- [ ] SNS リンク（Facebook / X / Instagram / YouTube / LinkedIn）の追加
- [ ] Google Analytics / HubSpot トラッキングの設定
- [ ] プライバシーマーク画像の追加
