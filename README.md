# Codex ↔ ChatGPT Web GitHub bridge

这个仓库使用 GitHub Pull Request 作为 Codex 与 ChatGPT 网页版之间的共享上下文。

## 一次性设置

1. 在 ChatGPT 网页版打开“设置 → 应用”，连接 GitHub。
2. 在 GitHub 授权页面允许 ChatGPT 读取 `benxuben/codex-`。
3. 在 Codex 中始终从这个仓库项目开始任务。
4. 在 GitHub 仓库设置中保护 `main`，要求通过 Pull Request 合并。

ChatGPT 的 GitHub 连接负责读取和分析；Codex 负责修改、测试、提交和推送。

## 每轮工作流

1. 给 Codex 一个明确任务。
2. Codex 创建 `codex/<任务名>` 分支，修改并验证代码。
3. Codex 提交、推送并创建或更新目标为 `main` 的 Pull Request。
4. 将 Codex 报告的 PR URL、分支和 commit SHA 交给 ChatGPT 网页版。
5. 使用 [ChatGPT 审查提示词](.github/CHATGPT_REVIEW_PROMPT.md)分析 PR。
6. 把 ChatGPT 生成的“下一轮指令”复制回原 Codex 任务。
7. Codex 在同一分支修复并推送；重复审查，直到 ChatGPT 给出“可以合并”。
8. 最终由人确认 CI 和审查结果后合并，不让 AI 自动合并。

## 给 Codex 的任务模板

```text
请完成以下任务：
<描述需求和验收条件>

遵守仓库根目录 AGENTS.md。使用独立的 codex/<任务名> 分支，不要修改或合并 main。
完成后运行相关检查，提交并 push，创建或更新 PR，然后报告分支、完整 commit SHA、PR URL、测试结果和已知风险。
```

## 给 Codex 的复审修复模板

```text
继续处理现有分支 <分支名> 和现有 PR <PR URL>，不要创建新分支。

以下是 ChatGPT 网页版的审查意见：
<粘贴审查结果>

逐项核实，只修复有代码证据的问题。完成后运行相关测试，提交并 push 到同一分支，报告新的完整 commit SHA 和同一 PR URL。
```

