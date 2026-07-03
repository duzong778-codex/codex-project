# Codex 视觉与业务验收工作流

## 当前配置结论

本项目已配置为“老爹只验收最终视觉和业务结果”的工作方式。后续任务默认由 Codex 自行处理技术实现、子代理审查、质量复核和修复循环；只有最终结果达标，或遇到真实阻塞/高风险边界，才向老爹汇报。

## 最终验收标准

- 视觉审美：构图、色彩、质感、清晰度、比例、边缘、光影协调。
- 真实可信：不能有明显 AI 痕迹、商品变形、材质失真、虚假承诺或不合理场景。
- 消费者打动力：主体突出、卖点明确，能提升点击、信任或成交意愿。
- 业务适配：符合当前平台、商品、受众、价格带和使用场景。
- 合规安全：不绕过平台审核、验证码、登录限制、风控或反爬机制。
- 可交付性：文件命名清楚、路径明确、能直接查看或继续使用。

## 后续任务默认流程

1. 先读取项目 `AGENTS.md` 和 `MEMORY.md`。
2. 设置或沿用明确 `/goal`：最终交付物必须通过视觉和业务验收。
3. 中间技术步骤由 Codex 自行推进，不打扰老爹确认。
4. 需要时调用子代理：
   - `visual-business-reviewer`：检查最终视觉和业务效果。
   - `technical-quality-gate`：检查实现质量、文件完整性和验证证据。
5. 未达标时自动修复，同类问题最多循环 3 轮。
6. 最终只汇报成品、业务影响、验证结果、剩余风险和文件位置。

## 多项目隔离

- 当前项目不是 Git 仓库，因此不能直接使用 Git Worktree。
- 现阶段采用项目目录隔离、`.planning/` 任务隔离、`work/` 中间文件隔离、`outputs/` 最终交付隔离。
- 项目进入 Git 仓库后，可在 Codex App 新线程中选择 `Worktree`，让不同任务在独立工作树中并行运行。
- Codex 官方说明：Worktree 依赖 Git 仓库；Codex 管理的 worktrees 默认放在 `$CODEX_HOME/worktrees`，可通过 Handoff 在 Local 和 Worktree 间移动线程。

## Cloud Mode 使用方式

Cloud Mode 不能仅靠本地文件自动开启。按官方说明，需要在 Codex Web / settings 中配置：

1. 打开 [Codex Web](https://chatgpt.com/codex)。
2. 连接 GitHub account，让 Codex 能访问目标仓库并创建 PR。
3. 打开 [Codex environment settings](https://chatgpt.com/codex/settings/environments)。
4. 为目标仓库配置 cloud environment：
   - setup script：安装依赖、测试工具、格式化工具。
   - environment variables：任务全程可用的环境变量。
   - secrets：只用于 setup 阶段，不进入 agent 阶段。
   - internet access：setup 阶段可联网；agent 阶段默认关闭，确有需要再开启有限或非受限访问。
   - cache：环境缓存最长约 12 小时，修改 setup、variables 或 secrets 会自动失效。
5. 发起 cloud task 时选择对应仓库、分支或 commit。
6. Codex 会在容器中 checkout repo、运行 setup、读取 `AGENTS.md`、执行任务、运行检查，并在结束时展示结果和 diff。

## 关键限制

- 当前本地目录不是 Git 仓库，所以不能直接把这个目录变成 Codex Cloud 任务。
- 要实现“合上电脑后继续后台推进”，需要先把项目放入 GitHub 仓库，再从 Codex Web 发起 cloud task。
- 若项目依赖本地未提交文件、浏览器登录态、桌面应用状态或私有缓存，Cloud Mode 默认拿不到；需要通过仓库文件、环境变量或 secrets 合规提供。

## 官方依据

- [Cloud environments](https://developers.openai.com/codex/cloud/environments)
- [Codex web](https://developers.openai.com/codex/cloud)
- [Worktrees](https://developers.openai.com/codex/app/worktrees)
- [AGENTS.md](https://developers.openai.com/codex/guides/agents-md)
- [Subagents](https://developers.openai.com/codex/subagents)
