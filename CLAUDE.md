# CLAUDE.md

LT会用のMarpスライド置き場。ビルド設定やpackage.jsonは無く、Markdownと画像だけのリポジトリ。

## ディレクトリ構成

- 発表ごとに `YYYYMMDD/` フォルダを作る（日付は発表日）
- フォルダ内に `slide.md`（本体）、使用する画像、エクスポートした `slide.pdf` を置く
- 画像はフォルダ直下に置き、`slide.md` から相対パス（`![alt text](01.png)` など）で参照する
- 例外: `20251223/` は本体が `copilot-instructions.md` という名前になっている（触る必要がなければそのままにする）

## スライドの書式

新規作成時は既存スライドと同じフロントマター・1枚目の書き方に揃える。

```markdown
---
marp: true
theme: default
paginate: true
header: 'タイトル'
style: |
    section.title * , h1{
        text-align: center;
    }
---

<!-- _class: lead -->
<!-- _header: "" -->

# タイトル

---

## 見出し

- 箇条書き
```

- `header` とタイトルスライドの `# ` は同じ文言にする
- タイトルスライドは `_class: lead` と `_header: ""` でヘッダーを消す
- 各スライドは `## 見出し` + 箇条書きが基本。強調したい結論は `**太字**` や `⇒` を使う
- 画像は Marp の背景画像構文をよく使う: `![bg right:40% contain](image.png)`、`![bg left:45%](02.jpg)`、サイズ指定は `![w:700px](lt04.jpg)`
- 最後のスライドは `## まとめ` で締める

## 分量

- 発表時間は **3分**。1分1枚が理想だが早めにめくるので、**多くても6枚程度**に収める
- 1枚あたりの文字量は少なめに。詰め込みすぎていたら分割より削る方向で提案する

## 頼まれる作業

- **新しいスライドの作成**: テーマを受けて `YYYYMMDD/slide.md` を上記書式で作る。日付が分からなければ確認する。画像はユーザーが用意するので、必要な箇所にはプレースホルダ（ファイル名と何の画像が欲しいか）を置いて伝える
- **推敲・校正**: 誤字脱字、言い回し、構成の改善。口語でくだけたトーン（「〜してみた」「めちゃくちゃかっこいい」など）は本人の味なので、硬い文章に書き換えない。事実関係（数字・固有名詞）が怪しければ指摘する
- **PDF出力**: 普段はユーザーが VS Code の Marp 拡張でエクスポートしている。Claude が出力する場合は Marp CLI を使う（ローカル画像を読むため `--allow-local-files` が必要）

  ```powershell
  npx @marp-team/marp-cli@latest YYYYMMDD/slide.md --pdf --allow-local-files -o YYYYMMDD/slide.pdf
  ```

## コミット規則

- 新しいスライドの追加: `feat: YYYYMMDD`
- 既存スライドの修正: `fix: YYYYMMDD`
- `YYYYMMDD` は**作業した日**（スライドのフォルダ名の日付ではない）
- 新規・修正ともに PDF を再出力し、`slide.md` と `slide.pdf` を一緒にコミットする
