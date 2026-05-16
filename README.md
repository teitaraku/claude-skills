# claude-skills

Claude Code 向けスキルプラグインのマーケットプレイスリポジトリです。

## 収録プラグイン

| プラグイン | 説明 |
|-----------|------|
| [pokemon-champions](./plugins/pokemon-champions/) | ポケモンチャンピオンズ（Pokémon Champions）のパーティ構築・ダメージ計算を支援するスキル集。各レギュレーション対応。 |

## セットアップ

まずマーケットプレイスを登録します。

```
/plugin add-marketplace teitaraku/claude-skills
```

## インストール

マーケットプレイス登録後、プラグインをインストールします。

```
/plugin install <plugin-name>@teitaraku
```

## プラグインの追加

新しいプラグインを追加する場合は以下の構成に従ってください。

```
plugins/
└── <plugin-name>/
    ├── README.md
    ├── .claude-plugin/
    │   └── plugin.json
    └── skills/
        └── <skill-name>/
            └── SKILL.md
```

追加後、`.claude-plugin/marketplace.json` のプラグイン一覧を更新してください。
