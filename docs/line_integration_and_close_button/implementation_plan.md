# 実装計画 - LINEへの送信機能および閉じるボタンの追加

ユーザーが診断を完了した際に、その結果をLINEのトークルームに自動送信し、最後にページを閉じることができるように機能を拡張します。

## ユーザーレビューが必要な事項
> [!IMPORTANT]
> `liff.sendMessages()` を使用する場合、LIFFアプリに `chat_message.write` 権限が必要です。LINE Developers コンソールで権限が有効になっているかご確認ください。

## 変更内容

### index.html
診断完了時の処理 (`submitDiagnosis`) と、結果画面のUIを変更します。

#### [MODIFY] [index.html](file:///c:/Users/Public/Desktop/workspace/juninjuieDNA/index.html)
- `submitDiagnosis` 関数内に `liff.sendMessages()` を追加し、診断結果をトークルームに送信するようにします。
- `screen-result` セクションに「LINEを閉じてトーク画面に戻る」ボタンを追加します。
- `liff.closeWindow()` を実行する `closeLiff()` 関数を実装します。

## 検証計画

### 自動テスト
- 特になし（フロントエンドUIおよびLIFF APIのインタラクションのため）

### 手動確認
- LIFFブラウザで診断を実行し、完了後にLINEトークルームにメッセージが送信されるか確認。
- 「閉じる」ボタンを押して、LIFFウィンドウが正常に閉じるか確認。
- （デスクトップブラウザでの動作確認用に、コンソールログも出力するようにします）
