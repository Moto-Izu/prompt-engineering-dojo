# プロンプト寺子屋 📚

Anthropicのプロンプトエンジニアリング教本を、実際の会話窓で実践できる形にアレンジして学習するプロジェクトです。

## 🎯 学習目標

- この会話窓で**即実践できる**プロンプトエンジニアリング技術の習得
- APIキーやPython不要で、**理論 + 実践**を両立
- 実際のユーザーニーズ（作詞、開発、翻訳等）に直結する技術習得

## 👤 学習者プロフィール

- 日本男性、アメリカ音楽愛好家
- **AI Singer REIA** や自身名義での楽曲制作（作詞、SUNO AI活用）
- **Windsurf/Cursor** での開発（Claude使用）
- **MCP** での諸々のお願い
- 英文翻訳作業
- 基本的なやり取りは日本語、他言語使用時は明示希望

## 📖 学習方針

### 各章の進め方
1. **理論解説**（この会話窓向けにアレンジ）
2. **❌悪い例 vs ✅良い例**で効果を体感
3. **実際のニーズで実践**（REIA楽曲、開発、翻訳等）
4. **日常活用への応用**

### 重要な指示・注意事項
- エラー対応時は必ずスレッド全体の文脈を確認してから解決策を提示
- 一度指示した内容と矛盾する新しい指示を出す前に、必ず経緯を振り返る
- 技術的問題で行き詰まった時は「thinking hard please」で一度立ち止まり、根本から見直す
- ユーザーが求めていない機能を勝手に提案しない
- 作詞の際は歌のパート名毎に [Verse1][Chorus] のように [ ] をつける

---

## 📚 学習進捗

### ✅ 第1章: 基本的なプロンプト構造 

**習得した4つの基本要素:**
1. **タスク (Task)** - 何をしてほしいか
2. **文脈 (Context)** - 背景情報  
3. **例示 (Examples)** - 期待する形式
4. **制約 (Constraints)** - 条件・制限

**実践例で確認済み:**

#### 作詞の改善例
```
❌ 悪い例: 「愛をテーマにした歌詞を書いて」

✅ 良い例:
【タスク】失恋をテーマにしたバラードの歌詞を作成してください
【文脈】20代女性の心境を歌った楽曲で、別れた恋人への想いを歌います。SUNO AIで生成予定です。
【例示】以下の構成で：
[Verse1] - 別れの瞬間の描写
[Chorus] - 失った愛への想い  
[Verse2] - 一人になった現在の心境
【制約】
- 各パート4-8行
- 繰り返しやすいメロディアスな言葉遣い
- 過度に暗くならず、希望も込める
```

#### 開発指示の改善例
```
❌ 悪い例: 「ログイン機能を作って」

✅ 良い例:
【タスク】React + TypeScriptでログイン機能を実装してください
【文脈】音楽配信アプリのユーザー認証機能として使用します。バックエンドはFirebaseを想定しています。
【例示】必要な機能：
- ユーザー名/パスワード入力フォーム
- バリデーション（メール形式、パスワード強度）
- ログイン状態の管理
- エラーハンドリング
【制約】
- TypeScriptで型安全に
- 既存のデザインシステム（Tailwind CSS）を使用
- 日本語対応
- モバイルフレンドリー
```

---

## 📋 今後の学習予定

### 未学習の章
- 第2章: Being Clear and Direct
- 第3章: Assigning Roles  
- 第4章: Separating Data from Instructions
- 第5章: Formatting Output & Speaking for Claude
- 第6章: Precognition (Thinking Step by Step)
- 第7章: Using Examples
- 第8章: Avoiding Hallucinations
- 第9章: Building Complex Prompts

### 実践予定テーマ
- **AI Singer REIAの新曲コンセプト**
- **音楽制作MCPワークフロー設計**  
- **英文翻訳精度向上**
- **開発指示の最適化**

---

## 🔗 参考資料

- [Anthropic公式プロンプトエンジニアリング教本](https://github.com/anthropics/prompt-eng-interactive-tutorial)
- [解答集](https://docs.google.com/spreadsheets/d/1jIxjzUWG-6xBVIa2ay6yDpLyeuOh_hR_ZB75a47KX_E/edit)
- [Anthropic公式ドキュメント](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)

---

*最終更新: 2025年6月6日*
*学習形式: 時間があるときに少しずつ継続学習*