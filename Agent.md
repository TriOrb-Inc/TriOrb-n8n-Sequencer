# Agent.md（例）

本ファイルは、n8n上でTriOrb AMRのAPIを使ってシーケンス制御するための例をまとめたものです。

## 目的

- AMRのタスク起動・停止をn8nワークフローで統合する
- 複数タスクの順序制御（シーケンス）を可視化する

## 想定する環境変数

```
AMR_API_PORT=8080
AMR_API_KEY=<必要に応じて設定>
```

> AMRのIPアドレスは複数台になる前提のため、n8nのダッシュボードで対象機器を追加して運用します。

## n8nワークフロー例（概要）

1. **Webhook**: 外部からのリクエストでシーケンス開始
2. **HTTP Request**: AMRの状態取得
3. **IF**: 状態が `IDLE` の場合のみ次に進む
4. **HTTP Request**: 目的地への移動タスクを作成
5. **Wait**: 一定間隔で状態をポーリング
6. **IF**: タスク完了を判定
7. **HTTP Request**: 次のタスク（例: 充電ステーションへ移動）を作成

## HTTP Request ノード例

- **Method**: `POST`
- **URL**: `http://<AMRのIP>:${AMR_API_PORT}/api/v1/tasks`
- **Headers**:
  - `Content-Type: application/json`
  - `Authorization: Bearer ${AMR_API_KEY}`（必要な場合）
- **Body**:

```json
{
  "type": "MOVE",
  "target": "STATION_A"
}
```

## 運用のヒント

- 失敗時のリトライは `Error Trigger` + `Wait` で制御すると運用が楽になります。
- AMRの状態ポーリング間隔は、機器側の負荷に応じて調整してください。
