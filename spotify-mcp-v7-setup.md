# Spotify MCP v7 完全セットアップ引き継ぎ書

**最終更新**: 2025年6月16日  
**バージョン**: v7.0 (認証済み・動作確認済み)  
**ステータス**: ✅ 完全動作

## 📋 概要

marcelmarais/spotify-mcp-server (Node.js実装) を使用したSpotify MCP サーバーの完全動作版セットアップ手順です。Claude Desktop、Cursor、その他MCP対応アプリケーションで使用可能です。

## ⚠️ 重要な前提条件

- **Spotify Premium アカウント** が必須（無料アカウントでは動作しません）
- **Node.js v16+** が必要
- **Spotify Developer App** の作成が必要

## 🎯 完全動作確認済み設定値

### Spotify Developer App 設定
- **App Name**: SonicPulse MCP v2
- **Client ID**: `9e1931d0bde44dcd9612ab68920ec4cb` ✅
- **Client Secret**: `c27dff0e4e1f4755b53110bcd05985b0` ✅
- **Redirect URI**: `http://127.0.0.1:8888/callback` ✅
- **APIs Used**: Web API, Web Playback SDK ✅
- **App Status**: Development mode ✅

### 認証済みトークン情報
- **Access Token**: 取得済み（自動更新対応）
- **Refresh Token**: 取得済み（永続化）
- **認証状態**: ✅ 成功確認済み

## 🚀 セットアップ手順

### Step 1: プロジェクトのクローンとセットアップ

```bash
# 作業ディレクトリの作成
mkdir ~/spotify-mcp-v7
cd ~/spotify-mcp-v7

# リポジトリのクローン
git clone https://github.com/marcelmarais/spotify-mcp-server.git
cd spotify-mcp-server

# 依存関係のインストール
npm install

# プロジェクトのビルド
npm run build
```

### Step 2: 設定ファイルの作成

```bash
# spotify-config.json を作成
cat > spotify-config.json << 'EOF'
{
  "clientId": "9e1931d0bde44dcd9612ab68920ec4cb",
  "clientSecret": "c27dff0e4e1f4755b53110bcd05985b0",
  "redirectUri": "http://127.0.0.1:8888/callback"
}
EOF
```

### Step 3: Spotify認証の実行

```bash
# 認証プロセスの開始
npm run auth
```

**重要**: 
1. ブラウザが自動で開きます
2. Spotifyにログインし、アプリケーションを承認してください
3. "Authentication Successful!" が表示されれば完了

### Step 4: 動作確認

```bash
# 設定ファイルの確認（トークンが追加されているか）
cat spotify-config.json
```

正常に認証されると、`accessToken` と `refreshToken` が追加されます。

## 🔧 Claude Desktop での設定

### macOS の場合
設定ファイル: `~/Library/Application Support/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "spotify": {
      "command": "node",
      "args": ["/Users/[USERNAME]/spotify-mcp-v7/spotify-mcp-server/build/index.js"]
    }
  }
}
```

**[USERNAME]を実際のユーザー名に置き換えてください**

### 設定の適用
```bash
# Claude Desktop を完全に終了
# Claude Desktop を再起動
```

## 🎪 Cursor での設定

1. Cursor で `Command + Shift + J` を押す
2. MCP タブを開く
3. サーバーを追加:
   - **Command**: `node`
   - **Args**: `/Users/[USERNAME]/spotify-mcp-v7/spotify-mcp-server/build/index.js`

## 🧪 動作テスト用コマンド

Claude Desktop または Cursor で以下をテストしてください：

```
現在再生中の曲を教えて
```

```
"Bohemian Rhapsody" を検索して
```

```
私のプレイリスト一覧を表示して
```

## 🔧 トラブルシューティング

### よくある問題と解決法

#### 1. INVALID_CLIENT エラー
**原因**: Client ID の文字間違い（特に「1」と「f」の混同）
**解決**: Client ID を文字単位で正確に確認

#### 2. Port 8888 already in use
```bash
# ポートをクリア
lsof -ti:8888 | xargs kill -9
```

#### 3. Premium アカウント要件
- Spotify Premium が必須
- 無料アカウントでは「User not registered in the Developer Dashboard」エラー

#### 4. トークン期限切れ
```bash
# 再認証の実行
cd ~/spotify-mcp-v7/spotify-mcp-server
npm run auth
```

## 📊 利用可能な機能

### 再生制御
- ✅ 現在の再生状況取得
- ✅ 楽曲の再生/一時停止
- ✅ 次の曲/前の曲
- ✅ ボリューム調整

### 検索・管理
- ✅ 楽曲・アーティスト・アルバム検索
- ✅ プレイリスト作成・管理
- ✅ 楽曲をプレイリストに追加
- ✅ 最近再生した楽曲の取得

### AI連携機能
- ✅ 自然言語での楽曲制御
- ✅ ムードベースのプレイリスト作成
- ✅ 楽曲推薦・類似曲検索

## 🚨 セキュリティ注意事項

- **spotify-config.json** には機密情報が含まれます
- ファイルを共有する際は十分注意してください
- 定期的にClient Secretをローテーションすることを推奨

## 🔄 引き継ぎ時のチェックリスト

### 新しいMacでの設定時
- [ ] Node.js v16+ のインストール確認
- [ ] Spotify Premium アカウントでのログイン確認
- [ ] リポジトリのクローン
- [ ] 依存関係のインストール
- [ ] ビルドの実行
- [ ] 設定ファイルの作成
- [ ] 認証の実行
- [ ] Claude Desktop/Cursor の設定
- [ ] 動作テストの実行

### 既存環境での確認
- [ ] トークンの有効性確認
- [ ] 最新版への更新確認
- [ ] 設定パスの確認

## 📝 バージョン履歴

- **v7.0** (2025-06-16): 完全動作版・認証成功・引き継ぎ書作成
- **v6.x**: Python実装版（過去バージョン）
- **v5.x**: 統合試行版（過去バージョン）

## 🤝 サポート

この引き継ぎ書で問題が発生した場合：
1. トラブルシューティングセクションを確認
2. GitHub Issues で報告
3. 設定値の再確認

---

**⚡ 重要**: この設定は2025年6月16日時点で完全動作確認済みです。Spotify API や MCP仕様の変更により、将来的に調整が必要になる可能性があります。