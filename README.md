# FX Schedule Feed

日本時間の火曜〜金曜の早朝取引について、EURUSD / GBPUSD / AUDUSD の新規エントリー可否を公開するJSON配信リポジトリです。

## 取得URL

`https://raw.githubusercontent.com/pic5/schedule-feed/main/schedule.json`

ファイル名とURLは毎週変わりません。

## 更新

日本時間の毎週日曜日19:00に、翌週の事前公開済み経済指標・中央銀行予定を使って、AIによる判定およびファイル更新を試行します。完全無人でのGitHub書き込みは定期タスクの実行時に確認が必要です。

## フィールド

- `schema_version`: JSONスキーマバージョン
- `week_start_jst`: 対象週の月曜日（`YYYY-MM-DD`）
- `generated_at_jst`: 判定生成日時（日本時間）
- `timezone`: `Asia/Tokyo`
- `server_session`: ThreeTraderサーバー時刻の対象時間
- `publication_ready`: 判定が利用可能な場合のみ `true`
- `days`: 火曜〜金曜の4件。各日の `EURUSD` / `GBPUSD` / `AUDUSD` は `稼働` または `停止`
- `reasons`: 各通貨の判定理由
- `trigger_events`: 判定に影響する事前公表済みイベント
- `sources`: 予定情報の参照元
- `uncertainties`: 予定の不確実性など

## 制御ソフト側の注意

取得できたことだけを稼働許可と解釈しないでください。JSONの構文、`schema_version`、`publication_ready === true`、`week_start_jst` と現在の日本時間の週の一致、`date_jst` の一致、対象通貨の判定値を確認します。

取得失敗・期限切れ・形式不正・日付不一致は**新規エントリー停止**とし、**保有ポジションの決済管理はそのまま継続**してください。

JSON配信は判断情報の提供だけであり、取引結果や利益を保証しません。
