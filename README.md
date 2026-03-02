# claude-test

GitHub Actions を使った CI（継続的インテグレーション）の練習用リポジトリです。

---

## 概要

このリポジトリは、**GitHub Actions** の基本的な使い方を学ぶためのサンプルプロジェクトです。

コードを `main` ブランチにプッシュしたり、プルリクエストを作成したりすると、自動で CI ワークフローが実行されます。現在のワークフローは Node.js の動作確認（バージョン表示）を行います。

```
コードをプッシュ → GitHub Actions が自動起動 → Node.js のセットアップ → node -v を実行
```

---

## セットアップ

### 必要なもの

- [Git](https://git-scm.com/) がインストールされていること
- GitHub アカウント

### 手順

1. **このリポジトリをクローンする**

   ```bash
   git clone https://github.com/<あなたのユーザー名>/claude-test.git
   cd claude-test
   ```

2. **GitHub でリポジトリを開く**

   ブラウザで `https://github.com/<あなたのユーザー名>/claude-test` にアクセスし、**Actions** タブを確認します。

---

## 使い方

### CI を動かしてみる

ファイルを変更してプッシュするだけで、自動的に CI が実行されます。

```bash
# 例：README を少し編集してプッシュ
git add README.md
git commit -m "READMEを更新"
git push origin main
```

プッシュ後、GitHub の **Actions** タブを開くと、ワークフローの実行状況をリアルタイムで確認できます。

### ワークフローの内容

`.github/workflows/ci.yml` に CI の設定が書かれています。

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4       # コードを取得
      - uses: actions/setup-node@v4     # Node.js をセットアップ
        with:
          node-version: '20'
      - run: node -v                    # バージョンを表示して動作確認
```

---

## 次のステップ

CI に慣れてきたら、以下のカスタマイズに挑戦してみましょう。

- **テストを追加する** — `npm test` を実行するステップを追加して、コードの品質を自動チェックする
- **複数の Node.js バージョンでテストする** — `matrix` 戦略を使って Node.js 18 / 20 / 22 を並列実行する
- **Lint を追加する** — ESLint などを組み込んでコードスタイルを統一する
- **デプロイを自動化する** — テスト通過後に自動でデプロイするステップを追加する

GitHub Actions の公式ドキュメントも参考にしてください。
https://docs.github.com/ja/actions
