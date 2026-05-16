# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

Claude Code スキルプラグインのマーケットプレイスリポジトリ。ユーザーが Claude Code の `/plugin` コマンドでインストールするプラグインをホストする。ビルド・lint・テストコマンドはなく、リポジトリの内容は Markdown と JSON のみ。

## プラグインの構成

各プラグインは `plugins/<plugin-name>/` 以下に置き、以下のレイアウトに従う：

```
plugins/<plugin-name>/
├── README.md                          # ユーザー向けドキュメント
├── .claude-plugin/
│   └── plugin.json                    # プラグインメタデータ
└── skills/<skill-name>/
    ├── SKILL.md                       # Claude のコンテキストに読み込まれるスキル定義
    └── references/                    # SKILL.md から参照される補助ファイル（任意）
        └── *.md
```

1つのプラグインに複数のスキルを持てる。

## プラグイン名とスキル名の区別

**プラグイン名**はスキルのコンテナ。スキルが増えても名前が腐らないよう、対象ドメイン全体を指す広い名前にする（例: `pokemon-champions`）。

**スキル名**は個々の機能単位。具体的な役割を示す名前にする（例: `pokemon-party-builder`、`pokemon-damage-calc`）。プラグイン名とスキル名を同一にしない。

## ファイルのスキーマ

### `plugin.json`

```json
{
  "name": "<plugin-name>",
  "description": "ユーザー向けの説明文",
  "version": "1.0.0"
}
```

未公開のプラグインはバージョン `1.0.0` から始める。

### `marketplace.json`

```json
{
  "name": "teitaraku",
  "owner": { "name": "teitaraku" },
  "plugins": [
    {
      "name": "<plugin-name>",
      "source": "./plugins/<plugin-name>",
      "description": "ユーザー向けの説明文"
    }
  ]
}
```

### `SKILL.md` フロントマター

```yaml
---
name: <skill-name>
description: スキルの自動起動トリガーになる説明文。「〜について言及されたら使用する」などトリガー条件を具体的に書く。
---
```

## スキルの仕組み

- `description` の内容が Claude がスキルを自動起動するトリガーになる。トリガー条件は具体的に記述する。
- `references/` 内のファイルは自動では読み込まれない。`SKILL.md` の中で「どの場面でどのファイルを参照するか」を明示的に指示する。複数ある場合は使い分け表を含める。

## 新しいプラグインの追加手順

1. `plugins/<new-plugin-name>/` 以下にディレクトリ構成を作成する。
2. `plugin.json` に `name`・`description`・`version` を記載する。
3. 各スキルの `SKILL.md` を作成する。
4. `.claude-plugin/marketplace.json` にエントリを追加する。
5. ルートの `README.md` の収録プラグイン一覧を更新する。

## インストール方法（参考）

```
/plugin add-marketplace teitaraku/claude-skills
/plugin install <plugin-name>@teitaraku
```
