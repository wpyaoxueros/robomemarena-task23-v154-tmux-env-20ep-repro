# RoboMemArena Task23 v154 Reproduction

这是 Task23 的一个不可变评测版本仓库。每个版本一个仓库；不覆盖之前版本。

## 版本结论

- 继承版本：Task23 v153 commit `4138d7f`，其评测基线是 v145 seed105 的运行方法。
- 继承 v152 的 `place popcorn` 无 end-pose target / consecutive hold 配置。
- 唯一新增评测行为修改：删除 `pick popcorn -> place popcorn` 的 robot-only frame-165
  release anchor。VLM 仍自主输出 `place popcorn`，但 release 后机器人保持真实当前状态，
  不会被 reset 到训练轨迹。
- v154 相对 v153 的唯一提交器修复：将已传给 `submit_zzhang510.sh` 的 `NUM_TRIALS` 和
  `SEED` 显式传入 tmux 内的 `srun` 命令。没有该修复时 tmux server 会回落到 launcher 的
  默认 `1/105`，使分片 20ep 实际重复同一个 episode。
- 保持 v145 的短 VLA primitive prompt：VLA 接收 `open microwave`、`pick cream` 等 VLM
  子任务名，不使用 v149/v150 的完整长训练 prompt 模板。
- 默认 seed 固定为视频对应的 `105`。
- VLM 负责输出所有子任务 prompt；没有 oracle next-prompt 注入。
- 没有 object anchor 或物体瞬移。
- 评分固定到 RoboMemArena `62214036103ee8d5fef9b475dd8b344b6e2cfc03`。
- `Close Microwave` 是审计项；Task23 的成功按最新远端必需 stage 全完成判定。

运行结果、视频名和外部产物哈希记录在 `history/RESULT.md`；不要根据仓库名推断成功或失败，
必须以该文件、`summary.tsv` 和视频为准。

正式 20ep（seed `105..124`）已完成：required-stage 全完成 `4/20`，平均 stage 分数
`46.67%`。完整逐条结果、视频相对路径和所有 summary/manifest 哈希见
`history/RESULT.md`。

## 内容

- `run_task23_v154.sh`：固定本版本开关的入口。
- `inputs.env.example`：外部模型、数据、环境路径接口。仓库不写入 checkpoint
  的内部绝对路径。
- `config/`：本版本所有 hold target、passage、tolerance 和 release-anchor 配置。
- `evaluators/` 与 `scripts/`：本次运行使用的评测包装代码快照。
- `history/`：继承关系、假设、提交记录和最终结果。

## 复现

1. 将 `inputs.env.example` 复制为 `inputs.env`，填入本机路径。
2. 确认 `ROBOMEMARENA_REMOTE_ROOT` 是 commit
   `62214036103ee8d5fef9b475dd8b344b6e2cfc03`。
3. 从 GPU Slurm allocation 内执行：

```bash
bash run_task23_v154.sh
```

启动前脚本会校验远端 commit、必要的 VLM/VLA/checkpoint、评测代码和配置。每次
运行都会把实际代码和评分脚本快照复制到输出目录并生成 SHA256 清单。

## 版本纪律

发现新假设时，创建一个新的 GitHub 仓库和新的版本号；不要在本仓库修改配置后
冒充 v154。该规则避免历史成功代码和后续尝试混淆。
