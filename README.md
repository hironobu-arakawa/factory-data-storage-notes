# factory-data-storage-notes

Factory data storage design notes  
— 工場データを「どう保存するか」を判断するための設計メモ集

---

## What is this repository?

このリポジトリは、**工場データ基盤における「保存（Storage）」に関する設計判断を整理したノート集**です。

- どのデータを **保存すべきか / しなくてよいか**
- どこまでを **不可逆（immutable）**として扱うか
- 「後で使える」ために **何を残す必要があるか**
- データ品質（保障・補正・欠損）を **保存層でどう扱うか**

といった問いに対して、  
**製品選定ではなく、判断軸・思考プロセスそのもの**を残すことを目的としています。

---

## What this is NOT

このリポジトリは、以下を目的としていません。

- ❌ 特定製品（PI System / Snowflake / TimescaleDB など）の比較
- ❌ スキーマ設計やフォーマット定義のカタログ
- ❌ 「正解の保存方式」を提示するガイド

**保存方式そのもの（shape / format）**については、  
👉 別リポジトリ **factory-data-shapes** を参照してください。

---

## Positioning in the whole architecture

このリポジトリが扱うのは、データ基盤全体の中でいうと次の位置です。

[ Data Flow / Semantics ]
↓
（どこで確定するか）
↓
[ Storage Decision ]
↓
[ DB / TSDB / Object Storage ]


- Flow（流れ）や Semantics（意味付け）を前提に
- **「ここで保存してよいか」「ここで確定してしまってよいか」**を考える層

VCD / BOA 的に言えば、  
**Fact / Interpretation / Responsibility のうち、Fact をどこで固定するか**の話です。

---

## Repository structure
factory-data-storage-notes/
├─ human/ # 人が読むための設計メモ・考え方
└─ ai/ # AIに読ませる前提の判断ルール・補助資料

---

## How to read this repository

This repository is structured as a **decision guide**, not a reference manual.

### Human-readable design notes

Read in order:

1. **human/00_introduction.md**  
   → なぜ「保存」は技術ではなく意思決定なのか

2. **human/01_common_storage_mistakes.md**  
   → 保存判断で人が必ず踏む失敗パターン

3. **human/02_when_not_to_store.md**  
   → 「保存しない」と判断してよい条件

4. **human/03_where_storage_freezes_responsibility.md**  
   → DB / TSDB / Object Storage が固定する責任の違い

5. **human/04_storage_and_future_ai.md**  
   → AI時代に保存判断が最重要になる理由

These documents form a single logical flow and are meant to be read sequentially.

---

### AI-oriented decision rules

- **ai/decision_rules/where_to_store.yaml**  
  → Decide *where* data may be stored when storage is justified

- **ai/decision_rules/when_not_to_store.yaml**  
  → Explicit rules for *not storing* data and preserving optionality

These rules are intended to be consumed by:
- LLM-based design reviewers
- AI-assisted data platform agents
- Automated architecture checks

AI must respect **do_not_store** decisions defined here.

---

## Relation to other repositories

This repository focuses on **storage decisions only**.

For related topics:

- Data shapes / formats  
  → see **factory-data-shapes**

- DB layer responsibilities  
  → see **db-layer-design-principles**

- Async-first system design  
  → see **ot-it-async-design-appendix**

Each repository handles a different decision layer.
They are designed to be used together, but not merged.

---


### human/

- 保存判断で迷いやすい論点
- 現場・運用・将来拡張とのトレードオフ
- 「なぜその保存は危険か / 有効か」の言語化

設計レビューや、後からの振り返り用途を想定しています。

### ai/

- LLM に設計判断を支援させるための材料
- 「どこに保存すべきか」「保存してはいけない条件は何か」
- storage / db / lake / cache の切り分け判断ルール

**人が毎回考え直さなくてよい部分を、AIに委ねるための前提知識**です。

---

## Typical questions this repo tries to answer

- このデータは **履歴として保存すべきか**？
- 後から補正される前提のデータを **どこまで残すべきか**？
- 一度保存したら **意味が固定されてしまう危険**はないか？
- 「分析で使いたい」という理由だけで **保存してよいのか**？

---

## Relation to other repositories

- **factory-data-shapes**  
  → データの「形（縦持ち / 横持ち / event / snapshot）」を扱う  
- **db-layer-design-principles**  
  → DB 層の責務分離・アンチパターン  
- **ot-it-async-design-appendix**  
  → 非同期前提の設計思想（保存判断の前提）

このリポジトリは、それらの**中間にある「保存の判断」だけを切り出したもの**です。

---

## Intended audience

- 工場DX / 製造IT / OT-IT 連携に関わる設計者
- 「とりあえず全部保存」に違和感を持っている人
- データ基盤を **運用まで含めて設計したい人**
- 設計判断を AI に委ねるための前提を整えたい人

---

## Status

This repository is a living design note.

- 完成形はありません
- 現場・案件・失敗から随時更新されます
- 「正解」ではなく **判断の痕跡**を残します

---

If you are looking for:
- **How to store** → shapes / db repositories  
- **Where to decide** → this repository  


