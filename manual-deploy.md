# Vercel手動デプロイ方法

## 方法1: Vercel CLIを使用

```bash
# Vercel CLIをインストール
npm i -g vercel

# プロジェクトディレクトリで実行
cd /Users/kotarokashiwai/playbook/medent-website
vercel

# 質問に答える：
# ? Set up and deploy "~/playbook/medent-website"? [Y/n] → Y
# ? Which scope do you want to deploy to? → あなたのアカウントを選択
# ? Link to existing project? [y/N] → N
# ? What's your project's name? → medent-website
# ? In which directory is your code located? → ./
# ? Want to override the settings? [y/N] → N
```

## 方法2: Git URLを直接使用

1. Vercelダッシュボードで「Import Git Repository」
2. 下部の「Import Third-Party Git Repository」をクリック
3. URLを入力: `https://github.com/kashiwai/medent-website`
4. 「Continue」をクリック

## 方法3: GitHubとの連携をリセット

1. **GitHubから一度Vercelを削除**
   - https://github.com/settings/installations
   - Vercelを「Uninstall」

2. **Vercelから再度連携**
   - Vercelで「Import Git Repository」
   - 「Continue with GitHub」で再認証
   - 新しい権限でリポジトリが表示されるはず

## トラブルシューティング

### リポジトリが表示されない場合のチェックリスト：

1. **リポジトリの可視性**
   - Privateリポジトリの場合、Vercelに権限があるか確認
   - 一時的にPublicにして試す

2. **組織のリポジトリの場合**
   - 組織の設定でVercelアプリが許可されているか確認
   - Organization settings → Third-party access

3. **ブラウザの問題**
   - 別のブラウザで試す
   - Cookieとキャッシュをクリア
   - 広告ブロッカーを無効化

4. **アカウントの問題**
   - 正しいGitHubアカウントでログインしているか確認
   - 複数のGitHubアカウントがある場合は注意

### 最終手段：

もし何も機能しない場合は、GitHubのPersonal Access Tokenを使用：

1. GitHub → Settings → Developer settings → Personal access tokens
2. 「Generate new token」でrepoスコープを持つトークンを作成
3. VercelのImport画面で「Import Third-Party Git Repository」を使用
4. URLとトークンを使用してインポート