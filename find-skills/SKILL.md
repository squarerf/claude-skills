---
name: find-skills
description: 帮助用户发现和安装 agent skills，当用户问"怎么做 X"、"找一个 X 的 skill"、"有没有能做 X 的 skill"或表达扩展能力的兴趣时触发。
---

# Find Skills

从开放 agent skills 生态系统中发现和安装技能。

## 触发场景

当用户出现以下情况时使用此 skill：

- 问"怎么做 X"，而 X 可能已有现成的 skill
- 说"找一个 X 的 skill"或"有没有 X 的 skill"
- 问"你能做 X 吗"，X 是某种专业能力
- 表达扩展 agent 能力的兴趣
- 想搜索工具、模板或工作流
- 提到希望在某个领域获得帮助（设计、测试、部署等）

## Skills CLI 命令

Skills CLI (`npx skills`) 是开放 agent skills 生态的包管理器。

**核心命令：**

```bash
npx skills find [query]     # 按关键词搜索 skill
npx skills add <package>    # 从 GitHub 或其他来源安装 skill
npx skills check            # 检查 skill 更新
npx skills update           # 更新所有已安装的 skill
```

**浏览 skills：** https://skills.sh/

## 使用流程

### 第一步：理解需求

识别用户需要什么：
1. **领域**（如 React、测试、设计、部署）
2. **具体任务**（如写测试、创建动画、审查 PR）
3. **是否常见任务**（判断是否可能有现成 skill）

### 第二步：先查看排行榜

在运行 CLI 搜索之前，先查看 [skills.sh 排行榜](https://skills.sh/)，看看是否有知名 skill。

热门 skill 来源：
- `vercel-labs/agent-skills` — React、Next.js、Web 设计（100K+ 安装）
- `anthropics/skills` — 前端设计、文档处理（100K+ 安装）

### 第三步：搜索 Skill

```bash
npx skills find [query]
```

示例：
- 用户问"怎么让 React 应用更快？" → `npx skills find react performance`
- 用户问"能帮我审查 PR 吗？" → `npx skills find pr review`
- 用户问"我需要创建 changelog" → `npx skills find changelog`

### 第四步：验证质量

**不要仅凭搜索结果推荐 skill。** 需要验证：

1. **安装量** — 优先选择 1K+ 安装的 skill，低于 100 的要谨慎
2. **来源信誉** — 官方来源（`vercel-labs`、`anthropics`、`microsoft`）更可靠
3. **GitHub stars** — 检查源仓库，<100 stars 的 skill 需要谨慎对待

### 第五步：向用户展示选项

展示找到的 skill 时包含：
1. skill 名称和功能说明
2. 安装量和来源
3. 安装命令
4. skills.sh 链接

示例回复：

```
找到了一个可能有帮助的 skill！"react-best-practices" 提供来自 Vercel 工程团队的
React 和 Next.js 性能优化指南。（185K 安装）

安装命令：
npx skills add vercel-labs/agent-skills@react-best-practices

了解更多：https://skills.sh/vercel-labs/agent-skills/react-best-practices
```

### 第六步：安装

```bash
npx skills add <owner/repo@skill> -g -y
```

- `-g` — 全局安装（用户级）
- `-y` — 跳过确认提示

## 常见 Skill 分类

| 分类 | 搜索关键词示例 |
|------|---------------|
| Web 开发 | react, nextjs, typescript, css, tailwind |
| 测试 | testing, jest, playwright, e2e |
| DevOps | deploy, docker, kubernetes, ci-cd |
| 文档 | docs, readme, changelog, api-docs |
| 代码质量 | review, lint, refactor, best-practices |
| 设计 | ui, ux, design-system, accessibility |
| 效率工具 | workflow, automation, git |

## 搜索技巧

1. **使用具体关键词**："react testing" 比 "testing" 更好
2. **尝试同义词**：如果 "deploy" 没结果，试试 "deployment" 或 "ci-cd"
3. **检查热门来源**：许多 skill 来自 `vercel-labs/agent-skills` 或 `ComposioHQ/awesome-claude-skills`

## 未找到 Skill 时

1. 告知用户没有找到现有 skill
2. 提供直接帮助完成任务
3. 建议用户可以创建自己的 skill：

```bash
npx skills init my-xyz-skill
```

示例回复：

```
搜索了 "xyz" 相关的 skill，没有找到匹配项。
我可以直接帮你完成这个任务！需要我继续吗？

如果这是你经常做的事情，可以创建自己的 skill：
npx skills init my-xyz-skill
```
