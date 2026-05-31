# Claude Skills

个人 Claude Code 自定义技能集合，涵盖开发、设计、文档、分析等多个领域。

## 使用方式

将 skill 目录复制到 `~/.claude/skills/` 下，在 Claude Code 中输入对应的 slash command 即可触发。

```
# 示例
/code-review          # 代码审查
/create-project       # 创建项目
/stock-analysis       # 股票分析
```

---

## 技能列表

### 开发工具

#### `/code-review` — 代码审查

对代码进行全面审查，涵盖 bug、安全性、性能和可维护性。

- **输入**：文件路径或粘贴代码；未指定时自动执行 `git diff` 检查最近更改
- **输出**：按严重程度分级报告（Critical / Important / Suggestions）
- **场景**：PR 审查、安全审计、代码质量检查

#### `/create-project` — 项目脚手架

从零构建完整可运行的项目，遵循最佳实践和合理结构。

- **输入**：描述项目类型（Web 应用、游戏、工具、API 等）
- **输出**：完整的文件结构和所有代码文件，附运行命令
- **场景**：新建项目、快速原型开发

#### `/mimo-fix` — MiMo 模型修复

诊断和修复小米 MiMo 模型报错（401、model not found、微信无响应等）。

- **流程**：API Key 检测 → 配置一致性检查 → Session 错误检查
- **功能**：更换 Key / 清除 Session / 切换 1M 上下文模式
- **场景**：MiMo 连接故障排除、上下文模式切换

#### `/claude-update` — Claude Code 更新指南

Claude Code 更新最佳方案，含完整流程和常见问题处理。

- **流程**：更新前准备 → 执行更新 → 更新后验证 → 收尾
- **支持**：npm / winget / brew 三种安装方式
- **场景**：版本升级、更新故障排除

---

### 文档与写作

#### `/doc-writer` — 文档生成器

为代码和项目生成 README、API 文档或用户指南。

- **输入**：文件或项目路径
- **输出**：根据受众自动生成对应格式文档（README / API 文档 / 用户指南）
- **场景**：项目文档、API 说明、用户手册

#### `/word-doc` — Word 文档生成器

生成格式化的 Word 文档（.docx），支持表格、标题、段落。

- **输入**：描述文档需求（标题、表格结构、内容）
- **输出**：.docx 文件，默认微软雅黑字体，蓝色表头隔行变色
- **场景**：报告、数据表格文档

#### `/course-paper` — 课程论文自动生成

自动生成完整课程论文，含文献检索、DOI 验证、图表生成。

- **流程**：需求收集 → 文献检索（三轮） → 文献验证 → 内容生成 → 图表 → Word 输出
- **依赖**：Semantic Scholar API、matplotlib、python-docx
- **场景**：课程论文、综述论文、学术文献整理

---

### 设计与分析

#### `/frontend-design` — 前端设计

为 Web UI 和交互式项目提供设计原则和组件模式指导。

- **覆盖**：布局间距、排版、颜色、组件设计、交互动画、响应式
- **支持**：单文件项目、游戏/交互项目
- **场景**：网站开发、Web 应用、浏览器游戏

#### `/typeui-fundamentals` — UI/UX 设计基础原则

通用 UI/UX 设计原则，涵盖视觉层次、交互定律、排版和 WCAG 无障碍。

- **模块**：UI 原则、UX 原则、排版原则、无障碍规范
- **定位**：设计系统未覆盖时的原则参考层
- **场景**：设计决策、无障碍合规检查

#### `/stock-analysis` — 个股深度研究系统

基于三层架构的个股深度研究，生成专业 HTML 报告。

- **架构**：Python 数据采集（AkShare）→ AI 深度分析 → HTML 报告生成
- **输出**：K 线图、财务分析、五维评分、投资建议
- **耗时**：约 30-60 分钟
- **场景**：个股基本面分析、投资研究

---

### 系统工具

#### `/find-skills` — Skill 发现与安装

从开放 agent skills 生态系统中发现和安装技能。

- **触发**：用户问"怎么做 X"、"找一个 X 的 skill"、"有没有能做 X 的 skill"
- **命令**：`npx skills find [query]` 搜索、`npx skills add <package>` 安装
- **来源**：[vercel-labs/skills](https://github.com/vercel-labs/skills)
- **场景**：扩展能力、搜索工具和工作流

#### `/skill-creator` — 技能创建器

创建、修改和改进 Claude Code 自定义技能。

- **流程**：引导式对话 → 编写 SKILL.md → 保存至 `~/.claude/skills/`
- **功能**：新建 Skill、编辑已有 Skill 的触发描述或指令
- **场景**：扩展 Claude Code 能力

#### `/start-weixin` — 启动微信 Claude Bridge

后台启动微信 Claude Bridge，实现微信与 Claude 的桥接通信。

- **流程**：停止旧进程 → 启动 cc-connect → 验证就绪 → 启动 typing-companion
- **要求**：必须先启动 cc-connect 再启动 companion
- **场景**：启动/恢复微信桥接服务

---

## 目录结构

```
~/.claude/skills/
├── code-review/
│   └── SKILL.md
├── create-project/
│   └── SKILL.md
├── doc-writer/
│   └── SKILL.md
├── frontend-design/
│   └── SKILL.md
├── skill-creator/
│   ├── SKILL.md
│   ├── agents/          # 子代理配置
│   └── references/      # 参考文档
├── stock-analysis/
│   ├── SKILL.md
│   ├── README.md
│   └── output/          # 分析报告输出
├── mimo-fix/
│   └── SKILL.md
├── word-doc/
│   └── SKILL.md
├── course-paper/
│   ├── SKILL.md
│   ├── README.md
│   └── TASK_CHECKLIST.md
├── claude-update/
│   └── SKILL.md
├── typeui-fundamentals/
│   ├── SKILL.md
│   ├── ui-principles.md
│   ├── ux-principles.md
│   ├── typography-principles.md
│   └── accessibility.md
├── find-skills/
│   └── SKILL.md
├── start-weixin.md
└── README.md            # 本文件
```

## 依赖

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — AI 编程助手
- [python-docx](https://python-docx.readthedocs.io/) — Word 文档生成（word-doc、course-paper）
- [AkShare](https://akshare.akfamily.xyz/) — 股票数据接口（stock-analysis）
- [Semantic Scholar API](https://www.semanticscholar.org/product/api) — 学术文献检索（course-paper）

## 许可

仅供个人使用。
