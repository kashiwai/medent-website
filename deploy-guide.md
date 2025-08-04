# Vercelへのデプロイと独自ドメイン設定ガイド

## 前提条件
- GitHubアカウント
- Vercelアカウント（無料で作成可能）
- 独自ドメイン

## ステップ1: GitHubリポジトリの作成

1. GitHubで新しいリポジトリを作成
2. 以下のコマンドでローカルプロジェクトをプッシュ:

```bash
cd /Users/kotarokashiwai/playbook/medent-website
git init
git add .
git commit -m "Initial commit: MedEnt website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/medent-website.git
git push -u origin main
```

## ステップ2: Vercelへのデプロイ

### 方法1: Vercel CLIを使用（推奨）

```bash
# Vercel CLIのインストール
npm i -g vercel

# デプロイ
vercel

# プロンプトに従って設定
# - GitHubアカウントと連携
# - プロジェクト名を設定
# - ビルド設定はデフォルトでOK
```

### 方法2: Vercelダッシュボードから

1. [vercel.com](https://vercel.com)にログイン
2. "New Project"をクリック
3. GitHubリポジトリをインポート
4. デプロイ設定はデフォルトでOK
5. "Deploy"をクリック

## ステップ3: 独自ドメインの設定

### Vercel側の設定

1. Vercelダッシュボードでプロジェクトを開く
2. "Settings" → "Domains"に移動
3. 独自ドメイン（例: medent.co.jp）を入力
4. "Add"をクリック

### ドメイン側の設定

ドメインレジストラ（お名前.com、ムームードメインなど）で以下のいずれかを設定：

#### オプション1: Aレコード（推奨）
```
Type: A
Name: @ (またはルートドメイン)
Value: 76.76.21.21
```

#### オプション2: CNAMEレコード（サブドメインの場合）
```
Type: CNAME
Name: www (または任意のサブドメイン)
Value: cname.vercel-dns.com
```

### SSL証明書

- Vercelが自動的にLet's EncryptのSSL証明書を設定
- 設定後、数分で有効になります

## ステップ4: 確認

1. DNS設定が反映されるまで待つ（最大48時間、通常は数分〜数時間）
2. https://your-domain.com でアクセス確認

## 追加設定

### リダイレクト設定

`vercel.json`に以下を追加してwwwありなしを統一：

```json
{
  "redirects": [
    {
      "source": "/",
      "has": [
        {
          "type": "host",
          "value": "www.medent.co.jp"
        }
      ],
      "destination": "https://medent.co.jp",
      "permanent": true
    }
  ]
}
```

### 環境変数（必要な場合）

Vercelダッシュボードの"Settings" → "Environment Variables"で設定

## トラブルシューティング

### デプロイが失敗する場合
- `vercel.json`の構文を確認
- ファイルパスが正しいか確認

### ドメインが機能しない場合
- DNS設定が正しいか確認
- DNSの伝播を待つ（nslookupコマンドで確認）
- Vercelのドメイン設定画面でエラーメッセージを確認

### サポート
- Vercel公式ドキュメント: https://vercel.com/docs
- Vercelサポート: https://vercel.com/support