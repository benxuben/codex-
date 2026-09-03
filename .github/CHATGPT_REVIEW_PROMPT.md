# ChatGPT Web review prompt

Copy the template below into ChatGPT Web after connecting this repository through the GitHub app.

```text
请通过 GitHub 检查下面这个 Pull Request：

仓库：benxuben/codex-
PR：<粘贴 PR URL>
目标分支：main
Codex 分支：<粘贴分支名>
最新 commit：<粘贴完整 SHA>

请读取 PR diff、相关代码、测试及 PR 描述，然后检查：
1. 是否完整实现 PR 中声明的目标；
2. 是否存在逻辑错误、回归、安全问题或意外副作用；
3. 测试是否覆盖主要成功路径和失败路径；
4. 是否包含无关改动；
5. 是否适合合并。

请先按严重程度列出有代码证据的问题，并标明文件路径和代码位置。
如果没有阻塞问题，请明确写“可以合并”，不要为了给建议而虚构问题。

最后输出“给 Codex 的下一轮指令”，要求可以直接复制给 Codex；指令应包含：
- 继续使用当前分支，不创建新分支；
- 需要修改的具体问题和文件；
- 验收条件；
- 必须运行的测试；
- 完成后提交、push 到同一分支，并报告新 commit SHA 和同一 PR URL。
```

