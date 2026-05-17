# claude-skills

Claude Code 向けスキルプラグインのマーケットプレイスリポジトリです。

## 収録プラグイン

| プラグイン                                        | 説明                                                                                                                |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| [pokemon-champions](./plugins/pokemon-champions/) | ポケモンチャンピオンズ（Pokémon Champions）のパーティ構築・ダメージ計算を支援するスキル集。各レギュレーション対応。 |

## セットアップ

まずマーケットプレイスを登録します。

```
/plugin marketplace add teitaraku/claude-skills
```

## インストール

マーケットプレイス登録後、プラグインをインストールします。

```
/plugin install <plugin-name>@teitaraku
```

plugin を再読み込みします

```
/reload-plugins
```
