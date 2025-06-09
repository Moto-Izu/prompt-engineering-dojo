# Claude Code CLAUDE.md 実践ガイド 📝

このガイドは、[syu-m氏の実践記事](https://syu-m-5151.hatenablog.com/entry/2025/06/06/190847)を基に、Claude CodeのCLAUDE.md設定ファイルの効果的な活用方法をまとめたものです。

## 🎯 CLAUDE.mdとは

### 基本概念
CLAUDE.mdは、Claude Codeが起動時に自動読み込みする設定ファイルで、**AIとの共通言語**として機能します。

- **プロジェクトの文脈**: アーキテクチャ、技術スタック、開発フロー
- **コーディング規約**: チーム全員が守るべきルール
- **よく使うコマンド**: 定型的なタスクの自動化
- **AIへの具体的指示**: 動作制御のための明確なガイドライン

### 3つの配置パターン

1. **プロジェクトメモリ** (`./CLAUDE.md`)
   - Git管理でチーム共有
   - プロジェクト固有の設定

2. **ユーザーメモリ** (`~/.claude/CLAUDE.md`) 
   - 個人的な設定（全プロジェクト適用）
   - 「console.logではなくlogger使用」等

3. **サブディレクトリメモリ** (`./src/services/CLAUDE.md`)
   - モジュール固有の設定
   - 特定ディレクトリでの作業時に自動参照

## 🔄 効果的なワークフロー

### 1. 探索・計画・コード・コミットの流れ

**探索フェーズ**
```bash
# 関連ファイルの理解（実装は避ける）
@src/services/UserService.ts を読んで、まだコードは書かないで

# 依存関係の調査
UserServiceが依存している他のサービスも確認して

# サブエージェント活用
サブエージェントで、UserServiceのメソッドがどこから呼ばれているか調査して
```

**計画フェーズ（think モード活用）**
```bash
# 基本的な分析
このアーキテクチャをthinkで分析して、改善計画を立てて

# 複雑な問題
この認証システムの問題をthink hardで検討して、複数の解決策を提示して

# システム全体への影響
システム全体への影響をthink harderで評価して

# 計画の文書化
作成した計画をarchitecture-decisions/001-user-service-refactoring.mdに保存して
```

**実装フェーズ**
```bash
# 段階的実装
計画に従って、まずUserServiceの基本的なリファクタリングを実装して

# 継続的検証
実装した部分のユニットテストを実行して、既存の機能が壊れていないか確認して

# エラーハンドリング強化
nullやundefinedの場合の処理を追加して、エラーハンドリングを強化して
```

**コミットフェーズ**
```bash
# 論理的分割
変更をリファクタリング、機能追加、テスト追加の3つのコミットに分けて

# PR作成
PRを作成して。以下を含めて：
- 変更の背景と目的
- 実装アプローチの説明  
- テスト方法
- 破壊的変更の有無
- レビュアーへの注意点
```

## 🧪 TDD（テスト駆動開発）での活用

### TDDを使う場面
1. **APIインターフェースが確定している時**
2. **既存機能のリファクタリング**  
3. **バグ修正**（再発防止）

### TDDワークフロー

**Step 1: テストファースト**
```bash
UserService.authenticateメソッドのテストを作成して。
以下のケースをカバー：
- 正常な認証成功
- パスワード不一致
- ユーザーが存在しない
- アカウントがロックされている
- 連続失敗によるロック

# モック回避（実DB使用）
実際のデータベース接続を使用してテストを作成。モックは使わない
```

**Step 2: RED - 失敗確認**
```bash
npm test -- UserService.test.ts

# 失敗理由の分析
テストの失敗理由を分析して。以下の観点で：
- コンパイルエラーか実行時エラーか
- 期待値と実際の値の差異
- 未実装による失敗か、バグによる失敗か
```

**Step 3: GREEN - 最小実装**
```bash
テストが通る最小限の実装を作成して。
過度な最適化や追加機能は含めない

IMPORTANT: テストケース以外の機能は実装しない
YOU MUST: 各実装ステップ後にテストを実行して確認

# 段階的進行
まず最も単純なケース（正常な認証）から実装を始めて
```

**Step 4: REFACTOR - 改善**
```bash
テストが通ることを確認しながら、以下の観点でリファクタリング：
- 重複コードの除去
- 可読性の向上
- パフォーマンスの最適化
- ドキュメントの記載(README.md,CLAUDE.md,etc)
- コメントの記載
```

## 🛠️ 便利なショートカットとツール

### @ ファイル選択の効果的活用
```bash
# 基本形
@src/services/UserService.ts のcreateUserメソッドを改善して

# 複数ファイル横断分析
@src/services/UserService.ts と @src/models/User.ts を見て、データフローを説明して

# ディレクトリ全体
@src/services/ ディレクトリのすべてのサービスの概要を説明して

# ワイルドカード
@**/*Service.ts すべてのサービスファイルで共通のパターンを見つけて
```

### # ルール追加の戦略的活用
```bash
#このプロジェクトではzodでバリデーション。yupは使わない
#エラーメッセージは必ず日本語で記述
#APIレスポンスは必ずcamelCaseで統一
```

**優先順位**:
1. セッション中の `#` コマンド（最優先）
2. プロジェクトのCLAUDE.md
3. ユーザーのCLAUDE.md（~/.claude/）

### セッション管理
```bash
# 前回の続きから
$ claude --continue

# 特定セッション選択
$ claude --resume

# プロンプト履歴編集
[Esc][Esc] → 前のプロンプトを編集 → Enter

# コンテキストクリア
/clear
```

## 📸 ビジュアル活用（CleanShot X推奨）

### Claude Codeとの連携
```bash
# デザインモックアップ実装
このデザインモックアップに基づいてコンポーネントを実装して
[画像添付]

# バグ報告
このエラー画面が表示される原因を調査して修正して
[スクリーンショット添付]
```

CleanShot Xの優位性：
- 撮影後すぐに注釈追加（矢印、テキスト、モザイク）
- スクロールキャプチャ
- GIF録画で操作手順記録
- クラウドアップロード・URL共有

## 📋 実践的なCLAUDE.md設定例

### プロジェクト概要部分
```markdown
# 🔄 CLAUDE.md - プロジェクトドキュメント

## 📋 Project Overview
**プロジェクト名** はXXXを目的とした、YYY技術を使用したZZZシステムです。

## 🏗️ Architecture
### 🎯 Core Concept
- **🔧 主要機能**: 機能の説明
- **⚡ 技術スタック**: React + TypeScript + Firebase
- **📁 ディレクトリ構造**: src/components, src/services, src/utils
- **📊 状態管理**: Zustand使用
```

### AIへの具体的指示
```markdown
## 📚 Notes for AI Assistants
When working on this codebase:

1. **NEVER パスワードやAPIキーをハードコーディングしない**
2. **YOU MUST すべての公開APIにドキュメントを記載**
3. **IMPORTANT パフォーマンスへの影響を考慮**

Remember: This tool is about speed and simplicity. 
**Predictability beats cleverness.**
```

### 開発ガイドライン
```markdown
### Testing Checklist
When testing changes, verify:
- [ ] 基本機能が正常動作
- [ ] エラーハンドリングが適切
- [ ] パフォーマンスに問題なし
- [ ] 既存テストが通る
- [ ] ドキュメント更新済み
```

## 🚀 高度な活用パターン

### カスタムスラッシュコマンド
`.claude/commands/optimize.md`:
```markdown
このコードのパフォーマンスを分析し、3つの具体的な最適化案を提案してください：

1. **計算量の観点**で最適化ポイントを特定
2. **メモリ使用量**の改善案を提示  
3. **可読性を保った**実装方法を提案

使用例とベンチマーク結果も含めてください。
```

使用方法：
```bash
claude /optimize
```

### Git Worktreeと組み合わせ
```bash
# 機能開発用worktree
$ git worktree add ../project-feature-auth feature/auth

# バグ修正用worktree  
$ git worktree add ../project-bugfix-api bugfix/api-error

# 各worktreeで独立セッション
$ cd ../project-feature-auth && claude
$ cd ../project-bugfix-api && claude
```

### CI/CD統合
```yaml
# GitHub Actions例
- name: Claude Code Review
  run: |
    claude -p "このPRの変更をレビューして、以下の観点で問題を指摘：
    - セキュリティ脆弱性
    - パフォーマンス問題  
    - コーディング規約違反" \
    --output-format json > review.json
```

## 🎵 音楽制作・REIAプロジェクト特化設定

### 楽曲制作ワークフロー
```markdown
## 🎵 Music Production Guidelines

### Lyrics Format
- **YOU MUST** 歌詞は必ず[Verse1][Chorus]形式で記載
- **IMPORTANT** SUNO AI用の構造を意識（繰り返し、韻律）
- **NEVER** 著作権のある歌詞を参考にしない

### REIA Project Rules
- 楽曲メタデータは統一フォーマットで管理
- ジャンル、BPM、キー情報を必須記載
- バージョン管理で楽曲の変更履歴を追跡
```

### 音楽ツール開発用設定
```markdown
### Audio Processing
- **YOU MUST** Web Audio API使用時はブラウザ互換性を考慮
- **IMPORTANT** 音声ファイルサイズの最適化を実装
- **NEVER** 未圧縮音声をそのまま配信しない
```

## 💰 コスト効率化の実践

### 推奨アプローチ
1. **小さくテスト**: 1ファイルで動作確認後にスケールアップ
2. **適切なモデル選択**: 日常タスクはSonnet 4、複雑タスクはOpus 4
3. **コンテキストクリア**: `/clear`で不要な履歴削除

### permissions.allow推奨設定
```json
{
  "permissions": {
    "allow": [
      "List(*)",
      "Fetch(https://*)",
      "Edit(*)",
      "Bash(git:*)",
      "Bash(npm:*)",
      "Bash(ls:*)",
      "Bash(cat:*)",
      "Bash(mkdir:*)",
      "Bash(mv:*)"
    ]
  }
}
```

## 🔍 トラブルシューティング

### よくある問題と対処法

**コンテキスト過多**
```bash
# 解決策: 定期的にクリア
/clear

# コンテキスト復元
@CLAUDE.md を読んで、プロジェクトのコンテキストを復元して
```

**AIの「親切すぎる」実装**
```bash
# 制約を明確化
IMPORTANT: テストケース以外の機能は実装しない
YOU MUST: 各実装ステップ後にテストを実行して確認
```

**長時間タスクの管理**
```bash
# 通知設定でタスク完了を確認
# 段階的実装で進捗追跡
まず1つのファイルで動作確認してから全体に適用
```

## 🎯 成功の秘訣

### 強調表現の使い分け

**NEVER（絶対禁止）**
```markdown
NEVER: パスワードやAPIキーをハードコーディングしない
NEVER: ユーザーの確認なしにデータを削除しない
NEVER: テストなしで本番環境にデプロイしない
```

**YOU MUST（必須事項）**
```markdown
YOU MUST: すべての公開APIにドキュメントを記載
YOU MUST: エラーハンドリングを実装
YOU MUST: 変更前に既存テストが通ることを確認
```

**IMPORTANT（重要事項）**
```markdown
IMPORTANT: パフォーマンスへの影響を考慮
IMPORTANT: 後方互換性を維持
IMPORTANT: セキュリティベストプラクティスに従う
```

### 予測可能性を重視
> **"Predictability beats cleverness."**
> 
> AIは時々賢すぎる解決策を提案してくる。しかしユーザーが求めているのは、予測可能な動作。

### 日々の習慣
```bash
# 一日の終わりに
今日の作業内容を要約して、明日やるべきことをリストアップして

# 朝一番に
$ claude --continue
```

## 📈 開発スタイルの変化

### 3ヶ月前との比較

**変わったこと**:
- ✅ 理論が実践になった
- ✅ 曖昧な指示でも伝わるようになった  
- ✅ コードの品質が向上した
- ✅ 開発速度が圧倒的に向上

**変わらなかったこと**:
- 📝 計画を立てるのは相変わらず苦手
- 🧪 TDDへの抵抗感は残っている
- 🚀 「とりあえず動かしてみる」精神は健在
- 😊 コードを書く楽しさは失われていない

### 役割分担の最適化

**人間（助手席）の役割**:
- 🎯 目的地を決める（何を作るか）
- 🗺️ ルートを提案する（アーキテクチャ）
- ⚠️ 危険を察知する（セキュリティ、パフォーマンス）

**Claude（運転席）の役割**:
- 💻 実際の運転（コーディング）
- 📏 交通ルールの遵守（言語仕様、ベストプラクティス）
- 🛣️ 効率的なルート選択（アルゴリズム、最適化）

## 💡 今後の展望

### 期待される進化
- **他社ツール**: Codex CLI、jules（Google）との競争
- **機能改善**: ツール呼び出し信頼性、長時間実行サポート
- **UI向上**: アプリ内レンダリング改善

### 継続的改善のポイント
1. **CLAUDE.mdの継続的アップデート**
2. **チーム内でのベストプラクティス共有**
3. **プロジェクト固有のカスタマイズ**
4. **コスト効率性の継続監視**

---

*参考記事: [Claude Code の CLAUDE.mdは設定した方がいい](https://syu-m-5151.hatenablog.com/entry/2025/06/06/190847)*

*最終更新: 2025年6月9日*

## 🔗 関連リソース

- [Claude Code完全ガイド](./claude-code-guide.md)
- [プロンプトエンジニアリング寺子屋 メインページ](./README.md)
- [Anthropic公式ドキュメント](https://docs.anthropic.com/en/docs/claude-code/overview)