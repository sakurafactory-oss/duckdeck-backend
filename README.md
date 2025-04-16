# DuckDeck Backend

**DuckDeck は、ログやサーバー内情報を DuckDB に蓄積・分析する軽量な国産サーバー情報可視化エンジンです。**  
このリポジトリはそのバックエンドを Go + Gin で実装した REST API サーバーです。

---

## 特徴

- **構造化ログ／メトリクス情報を SQL で統合分析**
- DuckDB を利用したファイルベースの軽量データストア
- ローカル、オンプレ、クラウドすべてに対応
- REST API 経由でログ投入・サーバー情報登録・即時クエリ実行
- クライアントは Web UI / CLI / ノーコードツールから自由に接続可能

---

## 使用技術（常に最新安定版を使用）

- **Go**（Gin フレームワーク使用）
- **DuckDB**（組み込み列指向分析DB）
- RESTful JSON API（OpenAPI対応予定）

> ※ 本プロジェクトではバージョン固定は行わず、常に安定版の最新依存ライブラリを利用します。

---

## ディレクトリ構成（予定）

duckdeck-backend/
├── cmd/             # サーバー起動エントリ
├── api/             # REST APIルーティング
├── db/              # DuckDB接続とクエリ処理
├── collector/       # サーバー情報取得ロジック
├── models/          # ログ／メトリクスの構造体
├── alerts/          # アラート評価・通知
└── go.mod / go.sum

---

## クイックスタート

### 前提：Go（最新版）とDuckDBが使える環境

```bash
# クローン
git clone https://github.com/yourname/duckdeck-backend
cd duckdeck-backend

# モジュール取得
go mod tidy

# 起動
go run cmd/main.go
```


⸻

サンプルAPI

ログ投入
```
POST /api/logs
Content-Type: application/json

{
  "timestamp": "2025-04-17T01:00:00Z",
  "level": "INFO",
  "message": "CPU usage normal"
}
```
サーバーメトリクス登録
```
POST /api/metrics
Content-Type: application/json

{
  "hostname": "server01",
  "cpu_percent": 72.3,
  "mem_used_mb": 6144,
  "load_avg": 0.81
}
```
SQLクエリ実行
```
POST /api/query
Content-Type: application/json

{
  "sql": "SELECT avg(cpu_percent) FROM metrics WHERE timestamp > now() - INTERVAL 10 MINUTE"
}
```


⸻

ライセンス

Apache License 2.0

⸻

開発・コントリビューション

軽量なサーバー監視やログ分析、オンプレにも強い国産エンジンを目指しています。
バグ報告・機能提案・プルリク歓迎です！

---
