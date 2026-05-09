# LING-AGENT-memory

这是 [LING](https://github.com/falling-feather/LING) 助手的**记忆仓库**：

- 主数据是人类可读的 Markdown / YAML（可审计、可回滚、可迁移）
- LING 服务端会定时同步（默认 4 小时）这一仓库到云端服务器，解析后入索引
- App 上的"完成 / 延期 / 捕获"等操作，都会由服务端写回这里并 commit/push（可在 GitHub 上看到 `[assistant]` 提交）

## 目录结构

- `tasks.yaml`：任务清单（含 `id / title / status / deadline / notes`）
- `core/identity.md`：长期稳定的偏好（低频更新）
- `daily/YYYY/YYYY-MM-DD.md`：每天的日记/工作记录（追加为主）
- `inbox/capture.md`：随手记录区，服务端会从中提取候选 TODO
- `ops/config.yaml`：运行时偏好（时区、提醒偏移、轮询周期、超期重复间隔）
- `ops/state.json`：可选的运行时状态（一般由服务端写）
- `index/`：机器产物（SQLite 等），不入库（见 `.gitignore`）

## 安全性提示

- 强烈建议把这个仓库设置为 **Private**（GitHub 仓库 -> Settings -> Change visibility）。
- 提交里如果出现敏感信息，请用 `git filter-repo` 或 `git rebase -i` 处理。

## 修改方式

- 你**手动**编辑：直接在 GitHub Web / 本地 clone 后修改 push
- LING **服务端自动**修改：会以 `[assistant]` 前缀提交，方便审计

二者是同一条 `main` 分支上的提交流；冲突时服务端默认放弃 push 并把修改落到 `ops/conflicts/<timestamp>.patch`，由你手工解决（一期保守策略）。
