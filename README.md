# claude-skills

Claude Code 用の共通スキル置き場です。ここが**スキルの原本**です。

クラウド環境のセットアップスクリプトが、セッション開始時にこのリポジトリをダウンロードし、
`skills/` の中身を `~/.claude/skills/` にコピーします。
そのため、どのリポジトリ（my-first-app、unique-tool など）でセッションを始めても同じスキルが使えます。

## スキル一覧

| スキル | 内容 |
|---|---|
| commit-message | 日本語の決まった形式でコミットメッセージを書く |
| full-check | 1ファイルWebアプリの変更後のチェック（普段は簡易、条件を満たすと総チェック） |
| publish-unique-tool | unique-tool へ noindex 付きで更新・公開する |
| pwa-single-file | 1ファイルWebアプリの PWA 化 |
| safe-data-change | 利用者の保存データを壊さない変更のルール |
| session-handoff | 長くなったセッションを新しいセッションに引き継ぐ準備（保存・HANDOFF 更新・貼るだけの依頼文） |
| visual-ux-principles | スマホ・PC両対応の操作性、数値の見やすさ、自然な日本語UIの原則 |
| app-evaluator | 自作アプリを3つのサブエージェントで評価（品質・使いやすさ・類似サービス調査）し、採点と改善フィードバックを返す |

## スキルを直すとき

1. このリポジトリの `skills/<スキル名>/SKILL.md` を直して、main に取り込む
2. **次の新しいセッションから**反映される

セッション中に `~/.claude/skills/` を直接書き換えても、次のセッションでは元に戻ります。

## スキルを追加するとき

`skills/<スキル名>/SKILL.md` を作る。フォルダ名と SKILL.md の `name` は同じにする。

## 注意

- このリポジトリは **public** のままにする（セットアップスクリプトは非公開リポジトリをダウンロードできない）
- 秘密の情報（パスワード・APIキーなど）をスキルに書かない
- 各プロジェクトの `.claude/skills/` には同じスキルを置かない（二重に読み込まれる）

## セットアップスクリプト（クラウド環境に登録するもの）

```bash
rm -rf /tmp/claude-skills-src
if git clone --depth 1 https://github.com/pierrotmask/claude-skills /tmp/claude-skills-src; then
  mkdir -p ~/.claude/skills
  cp -r /tmp/claude-skills-src/skills/. ~/.claude/skills/
fi
# frontend-design プラグインを入れる（失敗してもセッションは止めない）
claude plugin install frontend-design@anthropic-plugin-directory --scope user || true
```

スキルはこのリポジトリからコピーしますが、プラグインはマーケットプレイスからインストールします（中身をこのリポジトリに置く必要はありません）。
