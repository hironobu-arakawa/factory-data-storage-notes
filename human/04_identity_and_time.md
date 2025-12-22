# 形より先に Identity と Time

shapeを議論する前に、必ずこれを決める。

## Identity（同定）
- tag_id は “名前” ではない
- tag_id は “同一性” のキー
- 表示名・設備名・場所は変わる
- 変わっても tag_id は同一性を保つ（または改版する）

## Time（時刻）
- timezone と精度は契約
- 欠損や遅延を “埋める” のは別責務
- まず観測時刻と収集時刻を区別する

結論：Identity と Time の契約がない shape は、運用で燃える。
