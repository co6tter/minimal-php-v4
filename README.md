# minimal-php-v4

## Overview

シンプルなTODOリスト管理アプリケーションです。Docker環境でPHP + Nginx + MySQLを使用したミニマルなWebアプリケーション構成を実現しています。

主な機能:
- TODOアイテムの追加
- 完了/未完了の切り替え
- 個別削除
- 完了済みアイテムの一括削除
- CSRFトークンによる保護

## Tech Stack

- **PHP**: 8.4 FPM (Alpine)
- **Webサーバー**: Nginx 1.26 (Alpine)
- **データベース**: MySQL 8.4
- **依存関係管理**: Composer
  - vlucas/phpdotenv: 環境変数管理
- **コンテナ**: Docker / Docker Compose

## Setup

1. リポジトリのクローン
```bash
git clone <repository-url>
cd minimal-php-v4
```

2. 環境変数ファイルの設定
```bash
cp .env.sample .env
```

`.env` ファイルを編集して、データベース接続情報を設定してください:
```
DB_HOST=db
DB_PORT=3306
DB_ROOT_PASS=your_root_password
DB_NAME=your_database_name
DB_USER=your_username
DB_PASS=your_password
DB_CHARSET=utf8mb4
```

3. Dockerコンテナの起動
```bash
docker compose up -d
```

4. Composerの依存関係をインストール
```bash
docker compose exec php composer install
```

5. データベースの初期化
```bash
# MySQLコンテナに接続
docker compose exec db mysql -u your_username -p your_database_name

# SQLファイルを実行（または手動でテーブル作成）
# src/app/main.sql の内容を実行
```

6. ブラウザでアクセス
```
http://localhost:8080
```

## Usage

```bash

docker compose config
docker compose up -d

```

### TODOアイテムの管理

- **追加**: フォームにタイトルを入力して送信
- **完了切り替え**: チェックボックスをクリック
- **削除**: 削除ボタンをクリック
- **完了済みの一括削除**: Purgeボタンをクリック

### 開発時のコマンド

```bash
# コンテナの起動
docker compose up -d

# コンテナの停止
docker compose down

# ログの確認
docker compose logs -f

# PHPコンテナに入る
docker compose exec php sh

# MySQLコンテナに入る
docker compose exec db mysql -u root -p
```

## Directory Structure

```
.
├── .env                    # 環境変数ファイル（Git管理外）
├── .env.sample            # 環境変数のサンプル
├── docker-compose.yml     # Docker Compose設定
├── nginx/
│   └── default.conf       # Nginx設定ファイル
├── php/
│   ├── Dockerfile         # PHPコンテナ設定
│   └── php.ini           # PHP設定ファイル
└── src/
    ├── app/
    │   ├── Database.php   # データベース接続クラス
    │   ├── Todo.php       # TODOロジッククラス
    │   ├── Token.php      # CSRFトークンクラス
    │   ├── Utils.php      # ユーティリティクラス
    │   ├── config.php     # 設定ファイル
    │   └── main.sql       # データベース初期化SQL
    ├── public/
    │   ├── index.php      # エントリーポイント
    │   ├── css/          # スタイルシート
    │   └── js/           # JavaScriptファイル
    ├── composer.json      # Composer依存関係
    └── vendor/           # Composer依存パッケージ
```

## License

This repository is for personal/private use only.
