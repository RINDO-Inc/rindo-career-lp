# rindo-career-lp — 林業キャリア無料相談 LP

株式会社RINDO（林業専門求人サイト RINDO）が運営する、林業キャリア無料オンライン面談への申込みを目的としたランディングページ（LP）です。

## 目的

林業に興味がある未経験者・経験者が、転職を決めていない段階でも気軽に無料オンライン面談を予約できるようにすることを目的としています。
「応募・転職ありき」ではなく、情報収集の入り口として使ってもらうことを重視しています。

## 公開URL

- **Netlify仮URL：** https://bejewelled-kangaroo-b517c8.netlify.app/
- **本番予定URL：** https://career.rinroad.com/

## ファイル構成

```
rindo-career-lp/
├── index.html            # LP本体（1ページ構成）
├── style.css             # スタイルシート
├── _headers              # Netlify用キャッシュ設定
├── README.md             # このファイル
├── CLAUDE.md              # Claude Code向け運用ルール
├── .gitignore
└── assets/
    ├── logo-forest.webp      # ヘッダーロゴ（緑背景用）
    ├── forest-3.webp         # ヒーロー背景画像
    ├── advisor-tsuji.webp    # アドバイザー紹介写真
    └── logo-white.webp       # フッターロゴ（白抜き）
```

## 更新時の注意

- **予約ウィジェット（Spir）とLINEリンクは絶対に削除・変更しないこと。**
  - `index.html` 内の `<div class="spir-widget" data-url="...">` と、外部スクリプト `https://app.spirinc.com/js/external/iframe.js` を壊さないでください。
  - LINEリンク `https://lin.ee/My8T9kC` を壊さないでください。
- ページ内リンク `#reserve`（予約セクションへのジャンプ）を残してください。
- 画像・CSSのパスはすべて相対パス（`assets/...`、`style.css`）です。絶対パスやローカル環境依存のパスに変更しないでください。
- 「利用者の声」セクションは現在サンプル文です。**公開前に実際の声へ差し替え、または一時的に非表示にすることを推奨します。**（`index.html` 内 `<p class="disclaimer">` 参照）
- 詳しい編集ルールは [CLAUDE.md](./CLAUDE.md) を参照してください。

## ローカルでの表示確認方法（非エンジニア向け）

コードを直接ダブルクリックで開くと、画像やCSSが正しく表示されないことがあります。以下のいずれかの方法でご確認ください。

### 方法A：VS CodeのLive Serverを使う（おすすめ）

1. VS Codeでこのフォルダ（`rindo-career-lp`）を開く
2. 拡張機能タブで「Live Server」（作者：Ritwick Dey）をインストール
3. `index.html` を開いた状態で、右下の「Go Live」をクリック、または `index.html` を右クリック →「Open with Live Server」
4. ブラウザが自動的に開き、LPが表示されます

### 方法B：ターミナルでPythonの簡易サーバーを使う

1. ターミナル（Macなら「ターミナル」アプリ）を開く
2. このフォルダに移動する（例）
   ```
   cd "このフォルダのパス"
   ```
3. 以下を実行
   ```
   python3 -m http.server 8000
   ```
4. ブラウザで `http://localhost:8000` を開く
5. 確認が終わったら、ターミナルで `Control + C` を押してサーバーを停止

## Netlifyでの公開方法（GitHub連携）

1. GitHubで `rindo-career-lp` という名前のリポジトリを作成する
2. このフォルダの中身（`index.html`、`style.css`、`_headers`、`assets/`、`README.md`、`CLAUDE.md`、`.gitignore`）をリポジトリに入れてpushする
3. [Netlify](https://app.netlify.com/) にログインし、「Add new site」→「Import an existing project」を選択
4. 連携先として GitHub を選び、`rindo-career-lp` リポジトリを選択
5. ビルド設定は以下の通り（このLPはビルド不要な静的サイトのため）
   - **Build command：** 空欄のまま
   - **Publish directory：** `.`（ルート）を指定
6. 「Deploy site」をクリックすると、Netlifyの無料URL（例：`https://random-name-1234.netlify.app`）でLPが公開されます
7. 表示を確認し、問題がなければ本番用のサブドメインを設定します（下記参照）

以降は、GitHubリポジトリに変更をpushするだけで、Netlifyが自動的に再ビルド・再公開してくれます（自動デプロイ）。

## サブドメイン設定方針（career.rinroad.com）

本番では `rinroad.com` のトップドメインではなく、**サブドメイン `career.rinroad.com` を新規に切り出して使う**方針です。
これは、既存のWordPressサイト（`rinroad.com` 本体）に影響を与えないための安全策です。

### Netlify側の設定

1. Netlifyのサイト管理画面 →「Domain settings」→「Add custom domain」
2. `career.rinroad.com` を入力して追加

### DNS側の設定（ドメインを管理している側で設定）

以下のようなCNAMEレコードを追加します。

| 種類  | 名前     | 値（例）                              |
|-------|----------|---------------------------------------|
| CNAME | career   | rindo-career-soudan.netlify.app        |

※値は実際にNetlifyが発行するサイトURL（`◯◯◯.netlify.app`）に置き換えてください。

**注意点：**
- 値に `https://` は含めない
- 値の末尾に `/` を付けない
- DNSの反映には数分〜数時間かかる場合がある（反映まで待つ）
- 既存の `rinroad.com` 本体（WordPress）はNetlifyに向けない。今回はサブドメイン `career.rinroad.com` のみを追加する
- 反映後、Netlify側で自動的にHTTPS（SSL証明書）が有効になることを確認する

## 公開前チェックリスト

- [ ] PCブラウザで表示確認した
- [ ] スマホで表示確認した
- [ ] ヘッダーのロゴ（緑背景用）が表示される
- [ ] ヒーロー画像（森の写真）が表示される
- [ ] アドバイザー紹介の写真が表示される
- [ ] `style.css` のデザインが正しく反映されている（崩れていない）
- [ ] 「面談日程を予約する（無料）」ボタンを押すと予約セクションまで移動する
- [ ] LINEリンク（「まずはLINEで気軽に相談」「LINEで気軽に相談する」）が正しく開く
- [ ] Spir予約ウィジェット（カレンダー）が表示される
- [ ] 予約ウィジェットで日時選択などの操作が途中まで進められる
- [ ] Safariで表示・動作確認した
- [ ] Chromeで表示・動作確認した
- [ ] 表示速度が極端に遅くない
- [ ] フッターの電話番号（050-5530-0436）が正しい
- [ ] 「利用者の声」がサンプル文のままなら、公開前に実データへ差し替え、または非表示にした

## 今後の改善候補（メモ）

- ファーストビューのCTA文言・配置の改善
- 「利用者の声」の実データへの差し替え
- FAQの追加
- Google Analytics / Google Search Consoleの導入
- OGP画像（SNSシェア時のサムネイル）の設定
- コンバージョン（予約完了）計測の設計
- 表示速度のさらなる改善（画像圧縮など）
