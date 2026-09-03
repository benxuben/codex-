# Codex ↔ ChatGPT Web GitHub bridge

这个仓库使用 GitHub Pull Request 作为 Codex 与 ChatGPT 网页版之间的共享上下文。

## 一次性设置

1. 在 ChatGPT 网页版打开“设置 → 应用”，连接 GitHub。
2. 在 GitHub 授权页面允许 ChatGPT 读取 `benxuben/codex-`。
3. 为 Codex 配置该仓库所需的 GitHub 写权限，并确认 `origin` 指向正确的仓库。
4. 在 Codex 中验证能够 push 测试分支并创建 Pull Request，然后关闭测试 PR 或继续将其用于真实任务；不要用此验证绕过分支保护。
5. 在 Codex 中始终从这个仓库项目开始任务。
6. 在 GitHub 仓库设置中保护 `main`，要求所有变更通过 Pull Request 合并；存在 CI 后，将合并所必需的 CI 检查配置为 required checks。

ChatGPT 的 GitHub 连接负责读取和分析；Codex 负责修改、测试、提交和推送。

## 每轮工作流

1. 给 Codex 一个明确任务。
2. 对于新任务，Codex 先 fetch `origin`，再从最新 `origin/main` 创建新的 `codex/<任务名>` 分支。只有继续同一个现有 PR 时，才能在确认其当前 head 分支后复用该分支。
3. Codex 提交、推送并创建或更新目标为 `main` 的 Pull Request。
4. 将 Codex 报告的 PR URL、分支和完整 head SHA 交给 ChatGPT 网页版。
5. 使用 [ChatGPT 审查提示词](.github/CHATGPT_REVIEW_PROMPT.md)核对 PR 元数据并分析该 SHA。
6. 把 ChatGPT 生成的“下一轮指令”复制回原 Codex 任务。
7. Codex 在同一分支修复并推送。每次 push 都会使之前的 ChatGPT 审查结论立即失效，必须使用新的完整 head SHA 重新审查。
8. 重复修改和复审，直到 ChatGPT 对当前 head SHA 给出“可以合并”。这仍然不是合并授权。
9. 最终人工合并前，必须确认 PR 当前完整 head SHA、成功的必需检查及审查批准全部对应同一个 commit；只有人明确决定后才合并，不让 AI 自动合并。

## 给 Codex 的任务模板

```text
请完成以下任务：
<描述需求和验收条件>

遵守仓库根目录 AGENTS.md。先 fetch origin，从最新 origin/main 创建独立的 codex/<任务名> 分支，不要修改或合并 main。
完成后运行相关检查，提交并 push，创建或更新 PR，然后报告分支、完整 commit SHA、PR URL、测试结果和已知风险。
```

## 给 Codex 的复审修复模板

```text
继续处理现有分支 <分支名> 和现有 PR <PR URL>，不要创建新分支。

以下是 ChatGPT 网页版的审查意见：
<粘贴审查结果>

先确认该分支是指定 PR 的当前 head 分支。逐项核实，只修复有代码证据的问题。完成后运行相关测试，提交并 push 到同一分支，报告新的完整 commit SHA 和同一 PR URL。新的 commit 必须重新交给 ChatGPT Web 审查，旧审查不得作为合并依据。
```
