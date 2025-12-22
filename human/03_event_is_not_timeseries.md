# event は timeseries の省略ではない

イベントは「点の欠落」ではない。
イベントは「変化点だけが重要」というデータの性質。

- 連続値：timeseries（long/wide）
- 状態値：event（変化点）
- “ある時点の状態”：snapshot（配布）

event を無理に timeseries に変換すると、
変化の意味（いつ・なぜ変わったか）が薄れる。
