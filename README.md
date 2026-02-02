# TriOrb-n8n-Sequencer

TriOrb AMR（BISON 1.2.3）のAPIを利用して、n8n上でシーケンス制御（複数タスク実行など）を行う環境を構築するためのリポジトリです。

- AMR API ドキュメント: https://triorb-inc.github.io/TriOrb-AMR-Robot-Controller/bison1.2.3/

## 前提条件

- Windows 11/10 + WSL2（Ubuntu）
- Docker Desktop（WSL2統合が有効）
- Git

## セットアップ手順（WSL Ubuntu + Docker）

1. リポジトリを取得します。
   
   ```bash
   git clone <このリポジトリのURL>
   cd TriOrb-n8n-Sequencer
   ```

2. WSL Ubuntu上でDockerが利用できることを確認します。
   
   ```bash
   docker version
   ```

3. .env の作成（必要に応じて変更）
   
   ```bash
   cp .env.example .env
   ```

4. n8n を起動します。
   
   ```bash
   docker compose up -d
   ```

5. 設定を反映するため、Docker Compose環境を再起動します。

   ```bash
   docker compose restart
   ```

6. ブラウザで n8n にアクセスします。
   
   - http://localhost:5678

7. AMR API 連携のためのフローは `Agent.md` の例を参照してください（AMRのIPはn8nのダッシュボード側で追加します）。

## ディレクトリ構成（想定）

```
.
├── README.md
├── Agent.md
├── docker-compose.yml
├── .env.example
└── workflows/
```

## 補足

- APIの認証やエンドポイントは、AMRコントローラ側の設定に合わせて変更してください。
- n8nの環境変数は `.env` で管理します。
- AMRのIPアドレスは `.env` に保存せず、n8nのダッシュボードから対象機器を追加する運用を想定しています。

## n8nダッシュボードの多言語対応について

- 本リポジトリではn8nのUI言語設定は扱っていません。n8n側の設定メニューで言語切り替え項目が提供されている場合は、そちらを利用してください。
- 言語切り替えが提供されていない場合は、ブラウザの翻訳機能（例: Chromeのページ翻訳）での運用を検討してください。
