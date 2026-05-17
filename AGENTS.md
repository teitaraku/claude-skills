# Repository Guidelines

## プロジェクト構成とモジュール整理

このリポジトリは Claude Code 向けプラグインのマーケットプレイスです。主な内容は Markdown と JSON で、アプリケーションコード、パッケージマネージャー、ビルド成果物はありません。

- `.claude-plugin/marketplace.json`: マーケットプレイスのメタデータとプラグイン一覧。
- `plugins/<plugin-name>/`: プラグインごとの配置先。
- `plugins/<plugin-name>/README.md`: ユーザー向けのプラグイン説明。
- `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`: Claude が読み込むスキル定義。
- `plugins/<plugin-name>/skills/<skill-name>/references/`: スキルが参照する補助 Markdown。
- `.github/workflows/release.yml`: タグを契機にしたリリース自動化。

プラグイン名は `pokemon-champions` のように広い領域名、スキル名は `pokemon-party-builder` のように具体的な機能名にします。

## ビルド、テスト、開発コマンド

ローカルのビルドやテストランナーはありません。Pull Request 前に軽量な検証を行ってください。

```sh
rg --files
git diff --check
python3 -m json.tool .claude-plugin/marketplace.json
```

`rg --files` はファイル配置の確認、`git diff --check` は末尾空白やパッチ形式の検出、`python3 -m json.tool` は JSON 構文の検証に使います。

リリースは次の形式のタグを push すると作成されます。

```sh
git tag pokemon-champions-v1.0.0
git push origin pokemon-champions-v1.0.0
```

## コーディングスタイルと命名規則

ドキュメントとスキル本文は Markdown で記述します。見出しは簡潔にし、箇条書きと fenced code block を使ってコマンドや例を示してください。文字コードは UTF-8 を前提とし、日本語の説明文を基本にします。

プラグインとスキルのディレクトリ名は小文字の kebab-case にします。`SKILL.md` のフロントマターは有効な YAML にし、`description` には自動起動条件として機能する具体的な説明を書いてください。

## テスト方針

現在、自動テストは定義されていません。Markdown の読みやすさ、JSON 構文、内部リンクを手動で確認してください。スキルを更新する場合は、`references/` 配下の参照ファイル名が正しく、必要に応じて `SKILL.md` から明示的に案内されていることを確認します。

## コミットと Pull Request の指針

直近のコミットは `README.md 修正` や `ポケモンパーティ構築 plugin を作成` のような短い日本語要約です。この形式に合わせ、変更内容や追加内容が直接わかる件名にしてください。

Pull Request には概要、影響を受けるプラグインまたはスキルのパス、実施した検証、ユーザー向け文書の変更点を含めます。関連 Issue があればリンクしてください。スクリーンショットは、表示結果の確認が必要な場合のみ添付します。

## エージェント向け補足

プラグインを追加する場合は `.claude-plugin/marketplace.json` とルートの `README.md` を両方更新してください。スキルを追加する場合は `SKILL.md`、必要な `references/` ファイル、利用方法を説明するプラグイン側ドキュメントを揃えます。
