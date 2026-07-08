# 恋詠ノ書（恋愛タロット鑑定アトリエ）— 引き継ぎガイド

このリポジトリは **占い師向けの業務ツール「恋詠ノ書（こいよみ）」** です。
AI占いコンサルの購入者特典などとして配れます。

- フォームに相談内容を入力 → **そのまま納品できる鑑定書を作るためのAIプロンプト**を生成
- ワンボタンで **ChatGPT / Claude** を開いて貼るだけ → 鑑定書ができる
- **納品前チェック**：出力した鑑定書を貼ると、納品ルール（冒頭文・見出し・締め文・禁止表現など）を自動確認
- デザイン：墨色の夜空 × アンティークゴールドの和風世界観

> このファイルは、あなた（＝新しい持ち主）の **Claude Code にそのまま渡して**、
> 「このHANDOFF.mdの手順で、私のGitHubに公開して」と頼めば進められるように書いています。

---

## 大事なポイント：このツールは **APIキー不要**

星詠ノ書（体験版占いツール）とは違い、恋詠ノ書は **AIのAPIを直接呼びません**。
「利用者が自分のChatGPT / Claudeに貼って使う」仕組みなので、**Workerもキー設定も不要**。
`index.html` 1ファイルだけの完全自己完結。GitHub Pagesに置くだけで動きます。

---

## 1. 用意するもの
- **GitHubアカウント**（サイトの公開先）だけ。以上です。

## 2. 自分のGitHubに公開する

> このフォルダは、お渡しした **`koiyomi.zip` を展開したもの**です。
> Zipの置き場所でClaude Codeを開き、「このZipを展開して、中の HANDOFF.md の通りに進めて」と伝えれば、
> 解凍から公開まで進めてくれます（Claude Code は `unzip` で展開できます）。

### Claude Code に頼む場合（推奨）
> 「この（展開した）フォルダを私のGitHubに `koi-tarot-atelier` という公開リポジトリで作成して、
>  GitHub Pages（mainブランチ / ルート）を有効化して、公開URLを教えて」

### 手動でやる場合の参考コマンド
```bash
git init && git add index.html HANDOFF.md && git commit -m "init koiyomi"
gh repo create koi-tarot-atelier --public --source=. --push
gh api -X POST repos/<あなたのユーザー名>/koi-tarot-atelier/pages -f "source[branch]=main" -f "source[path]=/"
```
数分後、`https://<あなたのユーザー名>.github.io/koi-tarot-atelier/` で開けます。

---

## 3. ファイルの役割

| ファイル | 役割 |
|---|---|
| `index.html` | ツール本体（これ1つで完結。フォーム＋プロンプト生成＋納品前チェック） |
| `HANDOFF.md` | この引き継ぎガイド |
| `CLAUDE.md` | Claude Code 向けの運用ルール（このZipを渡すと自動で読まれる） |

---

## 4. デプロイ後にやるとよいこと（Claude Codeに頼めばOK）

公開できたら、まず **精度チェック**、その後 **デザイン・機能の調整** がおすすめです。
Claude Code からも折を見て提案してくれます。

- **精度チェック**：ツールが作ったプロンプトを ChatGPT / Claude に貼って、出てきた鑑定書を確認
  （名前で書けているか／断定を避けているか／見出し・固定文が入っているか。ツール内蔵の「納品前チェック」も活用）。
  直したい時は `index.html` の `SYSTEM_PROMPT`（占い師AIへの指示文）を調整。
- **入力項目を足す/減らす** → `index.html` のフォーム部分
- **納品前チェックの条件を変える** → `index.html` の `checkBtn` 周り
- **色・タイトルを変える** → `index.html` 冒頭の `<style>` 内 `:root`（`--gold` などの変数）

すべて `index.html` 1ファイルの中にあります。変更は「ローカルでプレビュー確認 → 問題なければ push」の順で。
困ったら、このファイルを Claude Code に見せて相談してください。

---

## 5. メモ
- 入力内容はブラウザ（localStorage）に保存されるだけで、外部には送信されません。
- 生成されるのは「AIに渡すプロンプト」。実際の鑑定文は、利用者自身のChatGPT / Claudeが作ります。
