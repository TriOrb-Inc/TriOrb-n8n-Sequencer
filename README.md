# TriOrb-n8n-Sequencer

TriOrb AMRのWeb APIを利用して、n8n上でシーケンス制御（複数タスク実行など）を行う環境を構築するためのリポジトリです。

- AMR API ドキュメント: https://triorb-inc.github.io/TriOrb-AMR-Robot-Controller/

## 前提条件
- Ubuntu + Docker
- Windows 11/10 + WSL2（Ubuntu）+ Docker
- Windows + Docker Desktop

## セットアップ手順（WSL Ubuntu + Docker）

1. リポジトリを取得します。
   
   ```bash
   git clone https://github.com/TriOrb-Inc/TriOrb-n8n-Sequencer.git
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
   
## 起動・再起動手順
### 初回起動：```docker compose up -d```
- 起動完了後にブラウザでn8nダッシュボード（[http://localhost:5678](http://localhost:5678)）にアクセスします
### 再起動：```docker compose restart```

## 補足
- APIの認証やエンドポイントは、AMRコントローラ側の設定に合わせて変更してください。
- n8nの環境変数は `.env` で管理します。
- AMRのIPアドレスは `.env` に保存せず、n8nのダッシュボードから対象機器を追加する運用を想定しています。
