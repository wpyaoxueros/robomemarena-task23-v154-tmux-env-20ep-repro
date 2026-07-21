# 版本历史

| 版本 | 继承 | 唯一改动 | prompt 权限 | 评分 | 结果 |
| --- | --- | --- | --- | --- | --- |
| v154 | v153 (`4138d7f`) | tmux 内显式传递 `NUM_TRIALS`/`SEED`，使分片 20ep 使用指定 seed；评测策略不变 | VLM 自主，oracle=0 | RoboMemArena `62214036103ee8d5fef9b475dd8b344b6e2cfc03` | 4/20 required-stage 全完成，平均 stage=46.67% |

本仓库只表示 v154。下一次配置、模型或评分代码改动必须进入新的仓库，并在该表的
后继仓库中记录 v154 的 commit 作为继承来源。
