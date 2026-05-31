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

### 文档处理

#### `/docx` — Word 文档处理 ⭐

创建、读取、编辑和操作 Word 文档（.docx）。

- **功能**：创建新文档、编辑现有文档、添加目录/页眉页脚/表格、图片替换、批注
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：报告、模板、专业文档

#### `/xlsx` — Excel 电子表格 ⭐

创建、读取、编辑 Excel 文件。

- **功能**：数据处理、公式计算、图表生成、格式化、数据清洗
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：数据报表、财务模型、数据分析

#### `/pptx` — PowerPoint 演示文稿 ⭐

创建和编辑幻灯片。

- **功能**：创建幻灯片、编辑模板、添加演讲备注、图表动画
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：演示文稿、汇报、路演

#### `/pdf` — PDF 处理 ⭐

读取、创建、编辑 PDF 文件。

- **功能**：文本提取、合并拆分、旋转页面、水印、表单填写、OCR
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：文档处理、表单填写、PDF 合并

#### `/word-doc` — Word 文档生成器

生成格式化的 Word 文档，支持表格、标题、段落。

- **输入**：描述文档需求（标题、表格结构、内容）
- **输出**：.docx 文件，默认微软雅黑字体，蓝色表头隔行变色
- **场景**：报告、数据表格文档

#### `/course-paper` — 课程论文自动生成

自动生成完整课程论文，含文献检索、DOI 验证、图表生成。

- **流程**：需求收集 → 文献检索（三轮） → 文献验证 → 内容生成 → 图表 → Word 输出
- **依赖**：Semantic Scholar API、matplotlib、python-docx
- **场景**：课程论文、综述论文、学术文献整理

---

### 前端与设计

#### `/frontend-design` — 前端设计 ⭐

创建高质量前端界面，避免"AI审美"。

- **特点**：强调独特风格、大胆创意、精致细节
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：网站、Web 应用、React 组件

#### `/canvas-design` — 视觉设计 ⭐

创建静态视觉设计（海报、艺术品、设计）。

- **输出**：.png / .pdf 文件
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：海报、Logo、平面设计

#### `/algorithmic-art` — 生成艺术 ⭐

使用 p5.js 创建算法艺术。

- **特点**：流场、粒子系统、计算美学、种子随机
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：生成艺术、数据可视化、交互作品

#### `/theme-factory` — 主题工厂 ⭐

10 种预设主题，一键应用到任何文档/网页/幻灯片。

- **主题**：Arctic Frost、Botanical Garden、Desert Rose、Golden Hour 等
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：统一视觉风格、品牌一致性

#### `/web-artifacts-builder` — Web 组件构建器 ⭐

构建 claude.ai HTML 组件（React + Tailwind + shadcn/ui）。

- **技术栈**：React 18、TypeScript、Vite、Tailwind CSS、shadcn/ui
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：复杂交互组件、单页应用

#### `/gpt-image-2` — GPT 图片生成

使用 GPT 模型生成图片。

- **来源**：[agentspace-so/agent-skills](https://github.com/agentspace-so/agent-skills)
- **场景**：AI 图片生成、创意设计

#### `/image-edit` — 图片编辑

AI 驱动的图片编辑。

- **来源**：[agentspace-so/runcomfy-agent-skills](https://github.com/agentspace-so/runcomfy-agent-skills)
- **场景**：图片修改、风格转换

#### `/image-to-video` — 图片转视频

将静态图片转换为动态视频。

- **来源**：[agentspace-so/runcomfy-agent-skills](https://github.com/agentspace-so/runcomfy-agent-skills)
- **场景**：动画制作、短视频

#### `/image-inpainting` — 图片修复

AI 图片修复和补全。

- **来源**：[agentspace-so/runcomfy-agent-skills](https://github.com/agentspace-so/runcomfy-agent-skills)
- **场景**：图片修复、去除水印、补全缺失部分

#### `/typeui-fundamentals` — UI/UX 设计基础原则

通用 UI/UX 设计原则，涵盖视觉层次、交互定律、排版和 WCAG 无障碍。

- **模块**：UI 原则、UX 原则、排版原则、无障碍规范
- **定位**：设计系统未覆盖时的原则参考层
- **场景**：设计决策、无障碍合规检查

---

### 开发工具

#### `/claude-api` — Claude API 开发 ⭐

构建、调试和优化 Claude API / Anthropic SDK 应用。

- **支持语言**：Python、TypeScript、Go、Java、Ruby、PHP、C#
- **特点**：自动添加 prompt caching、模型迁移指南
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：Claude API 开发、SDK 集成

#### `/mcp-builder` — MCP 服务器开发 ⭐

创建高质量 MCP（Model Context Protocol）服务器。

- **支持**：Python（FastMCP）/ Node（TypeScript MCP SDK）
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：API 集成、工具开发

#### `/webapp-testing` — Web 应用测试 ⭐

使用 Playwright 测试本地 Web 应用。

- **功能**：前端功能验证、UI 调试、截图、浏览器日志
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：E2E 测试、UI 验证

#### `/skill-creator` — 技能创建器 ⭐

创建、修改和优化 Claude Code 自定义技能。

- **功能**：创建新 Skill、编辑已有 Skill、运行评估测试
- **来源**：[anthropics/skills](https://github.com/anthropics/skills)
- **场景**：扩展 Claude Code 能力

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

### 系统工具

#### `/find-skills` — Skill 发现与安装

从开放 agent skills 生态系统中发现和安装技能。

- **触发**：用户问"怎么做 X"、"找一个 X 的 skill"、"有没有能做 X 的 skill"
- **命令**：`npx skills find [query]` 搜索、`npx skills add <package>` 安装
- **来源**：[vercel-labs/skills](https://github.com/vercel-labs/skills)
- **场景**：扩展能力、搜索工具和工作流

#### `/doc-writer` — 文档生成器

为代码和项目生成 README、API 文档或用户指南。

- **输入**：文件或项目路径
- **输出**：根据受众自动生成对应格式文档（README / API 文档 / 用户指南）
- **场景**：项目文档、API 说明、用户手册

#### `/start-weixin` — 启动微信 Claude Bridge

后台启动微信 Claude Bridge，实现微信与 Claude 的桥接通信。

- **流程**：停止旧进程 → 启动 cc-connect → 验证就绪 → 启动 typing-companion
- **要求**：必须先启动 cc-connect 再启动 companion
- **场景**：启动/恢复微信桥接服务

---

## 目录结构

```
~/.claude/skills/
├── # Anthropic 官方 Skills
├── docx/                    # Word 文档处理
├── xlsx/                    # Excel 电子表格
├── pptx/                    # PowerPoint 演示文稿
├── pdf/                     # PDF 处理
├── frontend-design/         # 前端设计
├── canvas-design/           # 视觉设计
├── algorithmic-art/         # 生成艺术
├── theme-factory/           # 主题工厂
├── web-artifacts-builder/   # Web 组件构建器
├── claude-api/              # Claude API 开发
├── mcp-builder/             # MCP 服务器开发
├── webapp-testing/          # Web 应用测试
├── skill-creator/           # 技能创建器
│
├── # Agentspace 图片 Skills
├── gpt-image-2/             # GPT 图片生成
├── image-edit/              # 图片编辑
├── image-to-video/          # 图片转视频
├── image-inpainting/        # 图片修复
│
├── # 个人 Skills
├── code-review/             # 代码审查
├── create-project/          # 项目脚手架
├── doc-writer/              # 文档生成器
├── word-doc/                # Word 文档生成器
├── course-paper/            # 课程论文
├── stock-analysis/          # 股票分析
├── typeui-fundamentals/     # UI/UX 设计原则
├── mimo-fix/                # MiMo 修复
├── claude-update/           # Claude 更新指南
├── find-skills/             # Skill 发现
├── start-weixin.md          # 微信桥接
└── README.md                # 本文件
```

## Skill 来源

| 来源 | 数量 | 说明 |
|------|------|------|
| [anthropics/skills](https://github.com/anthropics/skills) | 13 | Anthropic 官方 Skills |
| [agentspace-so](https://github.com/agentspace-so) | 4 | 图片/视频处理 |
| [vercel-labs/skills](https://github.com/vercel-labs/skills) | 1 | Skill 发现工具 |
| 个人开发 | 11 | 自定义 Skills |

## 依赖

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — AI 编程助手
- [python-docx](https://python-docx.readthedocs.io/) — Word 文档生成（word-doc、course-paper）
- [AkShare](https://akshare.akfamily.xyz/) — 股票数据接口（stock-analysis）
- [Semantic Scholar API](https://www.semanticscholar.org/product/api) — 学术文献检索（course-paper）

## 许可

各 Skill 许可见其目录下的 LICENSE.txt 文件。
