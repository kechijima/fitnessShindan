# 実装計画: ボディタイプ診断 LIFF の改修

LINE公式アカウントを通じた女性向けフィットネス診断アプリを構築します。

## ユーザーレビューが必要な事項

> [!IMPORTANT]
> - 診断結果を LINE に送信するため、LIFF のスコア設定（`chat_message.write`）が必要です。
> - 送信先 GAS の URL は、デプロイ後に `index.html` 内で環境変数または直接指定していただく必要があります。

## 変更内容

### UI/UX & デザイン [NEW DESIGN]

- **カラーパレット**: 
  - メイン: `#FFB6C1` (LightPink)、`#FF69B4` (HotPink)
  - 背景: `#FFF5F7` (Very Light Pink)
  - アクセント: `#FF1493` (DeepPink)
- **スタイル**:
  - ガラスモーフィズムを用いた透過カードデザイン
  - 滑らかな画面遷移アニメーション
  - モダンなタイポグラフィ（Google Fonts: Jost/Inter）
  - 各質問と結果に合わせた高品質な絵文字/アイコン

### フロントエンド (index.html) [MODIFY]

- [index.html](file:///c:/Users/Public/Desktop/workspace/fitnessDiagnosis/index.html)
  - 既存の「暮らしDNA診断」から「ボディタイプ診断」へ全構造を書き換え
  - **診断ロジックの統合**:
    - Q2, Q3, Q4 のスコアリング（合計3点以上でパーソナル）
    - Q1 によるスタジオタイプの分岐（ボディシェイプ/ファンクショナル/マインドボディ）
  - **LIFF SDK 2.x の活用**:
    - `liff.init()`
    - `liff.getProfile()` でユーザー名を取得
    - `liff.sendMessages()` で診断結果をトークルームに送信
  - **データ保存**:
    - `fetch` API を用いて直接 GAS (doPost) へ診断データを送信

## 診断ロジック詳細

- **PERSONAL**: スコア合計 3点以上
- **STUDIO**: スコア合計 2点以下
  - Q1 回答 A or B -> **BODY_SHAPE**
  - Q1 回答 C -> **FUNCTIONAL**
  - Q1 回答 D -> **MIND_BODY**

## 検証プラン

### 自動テスト / 手動検証
- **ブラウザ検証**: `Chrome` で全質問に回答し、ロジック通りに結果が出るか確認
- **LINE連携**: LIFF URL を実機で開き、メッセージが送信されるか確認
- **GAS保存**: スプレッドシートにデータが正しく書き込まれるか確認
- **モックテスト**: `liff.isInClient()` が false の場合の挙動（ブラウザ単体動作）を確認
