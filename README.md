# 一巻だけの本屋 レジ — VOLUME ONE BOOKS register

フリマ出店「一巻だけの本屋」の当日用レジアプリ。単一HTML・インストール不要・データは端末のブラウザ（IndexedDB）に保存。

https://v1books.github.io/register/

## 機能

- **レジ**：カメラでISBNバーコードを連続スキャン → カート → 合計・お釣り → 会計確定
  - 基本価格100円、100円の本5冊ごとに300円（まとめ割）。価格・冊数は設定で変更可
  - 本ごとの任意価格、値引き調整、会計の取消（返品・打ち間違い）
  - 下段の価格コード（192…）は自動で無視
- **棚出し（任意）**：事前スキャンで在庫・値付けを登録。レジで読むと自動で紐付け
- **分析**：時間帯別（売上／冊数／会計、1h／30分）、お客様属性別の集計
  - 属性（年代・性別・連れ・メモ）は会計時でも、あとから履歴でも記入可。選択肢は設定で編集
- **データ**：明細CSV（1冊1行）・会計CSV・全データJSONの書き出し／JSONからの復元

## 運用メモ

- カメラはHTTPSでのみ動作（GitHub Pagesで公開）
- iPhoneはSafariで開いて「ホーム画面に追加」
- データはドメイン（v1books.github.io）単位で保存。開催中にURLを変えないこと
- 昼と終了後に「全データJSON」を書き出してバックアップ
- リハーサル後は「データ → 全データを消去」

## データ

- IndexedDB `IkkanHonya_v1`（蔵書管理ツール reitovc/library とは別データ）
- 明細CSVはISBN・実売価格（まとめ割・値引きを按分）・販売時刻・お客様属性を含む。蔵書CSVとの統合はISBNで照合する想定

## 外部依存

- [zxing-wasm](https://github.com/Sec-ant/zxing-wasm)（zxing-cpp。`vendor/` に同梱、バーコード読取）
- [openBD](https://openbd.jp/) / Google Books API（書誌情報）
- Noto Sans JP（Google Fonts）
