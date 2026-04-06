# 診断コンテンツの更新（Q1〜Q4と4タイプの診断結果）

ユーザーからのリクエストに基づき、診断の質問、選択肢、および結果タイプを更新します。

## ユーザーレビューが必要な事項
- 診断結果のロジック（どの回答がどのタイプに繋がるか）についての提案。
- 各タイプ（エンジョイ習慣化、サポート活用、最短結果、コンディショニング改善）の解説テキストの調整（仮の文章を作成しますが、必要に応じて修正してください）。

## 修正内容の概要

### HTML/JavaScript

#### [MODIFY] [index.html](file:///c:/Users/Public/Desktop/workspace/fitnessDiagnosis/index.html)
- `q1`〜`q4` の質問文（HTML上の `h2.q-title` および JSの `questions` 配列内）を更新。
- 選択肢（A〜Eなど）のテキストを更新。
- 診断結果タイプを以下の4つに変更：
    1. ① エンジョイ習慣化タイプ (ENJOY)
    2. ② サポート活用タイプ (SUPPORT)
    3. ③ 最短結果タイプ (SHORTEST)
    4. ④ コンディショニング改善タイプ (CONDITIONING)
- `calculateResult` 関数内の判定ロジックを新タイプに合わせて更新。
- コメントアウトされている箇所（GASへの送信処理など）はそのまま保持。

## 回答とタイプのマッピング案（スコア制）
各選択肢に特定のタイプへの重み（スコア）を持たせ、合計が最も高いタイプを結果とします。

| 質問 | A | B | C | D | E |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q1 (目的)** | SHORTEST/SUPPORT | ENJOY/CONDITIONING | CONDITIONING | ENJOY | SHORTEST |
| **Q2 (理由)** | SUPPORT | SUPPORT | ENJOY | SUPPORT | SHORTEST |
| **Q3 (スタイル)** | ENJOY | SUPPORT/SHORTEST | SUPPORT | ENJOY | - |
| **Q4 (サポート)** | ENJOY | SUPPORT | SHORTEST | SHORTEST | - |

## オープンな質問
- 各診断タイプの「解説（res-desc）」や「おすすめプラン（res-suggestion）」に具体的なサービス名や詳細を記載する必要はありますか？

## 検証プラン
### 手動検証
- ブラウザで診断を最後まで進め、Q1〜Q4の内容が正しく表示されるか確認。
- 回答の組み合わせを変えて、4つのタイプすべてが正しく表示されるか確認。
- コメントアウトされている箇所が表示上やスクリプト実行に影響を与えていないか確認。
