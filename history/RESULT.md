# Task23 v154 结果

## 正式 20ep

- 状态：完成。
- 输出目录：`/data/user/zzhang510/hlei573_borrow_outputs/microwave_task23_continuations/task23_v154_20ep_seed105_124_20260721_230800`
- 分片：5 个独立 4ep 分片，seed `105..124`，共 20 条；每个 `run_manifest.json` 均记录
  `num_trials=4` 和该分片的正确起始 seed。
- 评分：RoboMemArena `62214036103ee8d5fef9b475dd8b344b6e2cfc03` 的
  `task2_26_reference_stage.py`；required stage 为 Open Microwave、Place Cream、
  Place Popcorn；Close Microwave 是 optional 审计项。
- prompt：VLM 自主输出；oracle prompt 注入为 0。没有 object anchor。保持 v153 的两个
  早期 robot-only release anchor，但没有 `pick popcorn -> place popcorn` 的最终 anchor。

| 指标 | 结果 |
| --- | --- |
| required-stage 全完成 | 4/20 = 20.0% |
| 平均 stage 分数 | 46.67% |
| 平均 goal progress（审计字段） | 0.4668 |
| 成功 seed | 105、111、112、119 |

逐条 stage 分数：`105:100.0, 106:66.7, 107:0.0, 108:66.7, 109:66.7, 110:66.7, 111:100.0,
112:100.0, 113:33.3, 114:0.0, 115:0.0, 116:66.7, 117:0.0, 118:66.7, 119:100.0, 120:66.7,
121:33.3, 122:0.0, 123:0.0, 124:0.0`。

成功主视角视频：

- `shard0_seed105/videos/task23/task23_success_ep0_seed105.mp4`
- `shard1_seed109/videos/task23/task23_success_ep2_seed111.mp4`
- `shard1_seed109/videos/task23/task23_success_ep3_seed112.mp4`
- `shard3_seed117/videos/task23/task23_success_ep2_seed119.mp4`

## 证据哈希

| 产物 | SHA256 |
| --- | --- |
| `aggregate_20ep.tsv` | `da93b2caf64628097f9567863031430b18d4d7f39eb09671ef4bfcf7d5681810` |
| `shard0_seed105/summary.tsv` | `79e0950a3721958072cad4a270d419b10a10426a58fd9709c97fb135429106a6` |
| `shard1_seed109/summary.tsv` | `4ca4d8778fcbcf439fa371720c2709d47d7d25b1112162607c9e08e44e97b8c5` |
| `shard2_seed113/summary.tsv` | `203d73c48fbe7904dc0c48b02f4d1636deaeab953555593cdd628012f2ca4293` |
| `shard3_seed117/summary.tsv` | `7a51e8969888d91d7eb63ac8d94b2a7e0777606b1fc794405cfbc0e6d118d502` |
| `shard4_seed121/summary.tsv` | `3326910d8986b148acc138bd13774f440a690ce6424609d099ee104b7c018e63` |
| `shard0_seed105/run_manifest.json` | `62fa386708f0da3d5d256deb73d955923d63c3968ea80b7be2c767d8d5e07d07` |
| `shard1_seed109/run_manifest.json` | `872e08a018dfe499deb192d36a8752ec302d3dbe8099e295033b5bceb6222038` |
| `shard2_seed113/run_manifest.json` | `5d3197ef411df3250f3b22b1708dd555d4d28bbb8da9790f64130b389a37cb3f` |
| `shard3_seed117/run_manifest.json` | `1a2486064fb60b7e8b1dd5839f951de2a19831322e7a0ba400b68efb0a7fe1d1` |
| `shard4_seed121/run_manifest.json` | `cfcd67aebe3623ea638cb421551906ddab93557462ff44db2a03f141dcc903b8` |

此前 v153 的 Attempt 003 因 tmux 未继承分片环境变量，实际重复运行了 seed105 单条 episode；
它不计入本次 20ep 指标。v154 已通过显式注入 `NUM_TRIALS`、`SEED` 修复该问题。
