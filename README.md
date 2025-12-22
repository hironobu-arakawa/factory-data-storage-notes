# factory-data-shapes

工場データの「フロー途中の形（shape）」を、製品・実装から独立して残すためのリポジトリ。

ここで扱うのは **縦持ち / 横持ち / イベント / スナップショット** と、
それらを成立させる **Identity（同定）・Timestamp（時刻）・Quality（品質）** の契約です。

> データは一元化できる。だが shape は一元化するな。

---

## Scope

### In scope
- timeseries_long（縦持ち・tidy）
- timeseries_wide（時間×タグ行列）
- event_log（状態変化・変化点）
- snapshot_table（参照配布用の切り出し）
- tag identity / timestamp rules / quality flags
- shape conversion rules
- shape selection rules (AI向け)

### Out of scope
- Kafka/MQTT/OPC-UA等の配信実装
- DB/TSDB/ストレージ製品選定、性能チューニング
- BIツールの設定、ダッシュボード設計

---

## Reading map

### Human
- `human/00_manifesto.md` : 宣言（短い）
- `human/01_choose_shape_by_workload.md` : 形の選び方
- `human/02_long_vs_wide.md` : 縦/横のトレードオフ
- `human/03_event_is_not_timeseries.md` : イベントの扱い
- `human/04_identity_and_time.md` : 同定と時刻が先

### AI / RAG
- `ai/concepts/` : 辞書
- `ai/formats/` : 形（契約）
- `ai/decision_rules/` : 判断ルール（設計支援の中核）
- `ai/fingerprints` は扱わない（別repo想定）。ただし `identity` に拡張余地あり

---

## Quick principle (1-liners)
- Shapeは「正しさ」ではなく「用途と責務」で選ぶ
- Identity と Timestamp は Shape より先に決める
- Quality（欠損/補完/異常）は値と一緒に運ぶ
- wide は投影（projection）。canonical（正本）にしない
