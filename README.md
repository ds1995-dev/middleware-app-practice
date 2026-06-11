# middleware-app-practice

## 概要
COACHTECH 教材 Tutorial 10-2「ミドルウェア」
middlewareを作成して管理者チェックロジックを実装

## 使用技術
- Laravel 10.x + Sail
- Fortify認証（ログイン / 登録 / ログアウト）
- Userモデル（is_adminカラム付き）
- テストユーザー（シーダー）
  - 管理者: admin@example.com / password
  - 一般: user@example.com / password
- AdminController
- 管理者ページ（/admin）

## セットアップ

```bash
git clone https://github.com/ds1995-dev/middleware-app-practice.git
cd middleware-app-practice

# 依存関係インストール
docker run --rm \
  -u "$(id -u):$(id -g)" \
  -v "$(pwd):/var/www/html" \
  -w /var/www/html \
  -e COMPOSER_CACHE_DIR=/tmp/composer_cache \
  laravelsail/php82-composer:latest \
  composer install

# 環境ファイル作成
cp .env.example .env

# Sail起動
./vendor/bin/sail up -d

# アプリケーションキー生成
./vendor/bin/sail artisan key:generate

# マイグレーション・シーダー実行
./vendor/bin/sail artisan migrate --seed
```

## 動作確認

1. http://localhost にアクセス
2. admin@example.com / password でログイン
3. 「管理者ページにアクセス」をクリック → 表示される
4. ログアウトして user@example.com / password でログイン
5. 「管理者ページにアクセス」をクリック → 403エラー

