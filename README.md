# AI Interface Studio Skill

面向 Codex 的多 Agent 产品想法 → UI/UX 设计 → 交互式前端预览工作流 Skill。

由协调 Agent 管理阶段门，分别委派产品与 UX、视觉设计、前端实施和视觉验收 Agent；用 Image Generation 生成设计系统与页面级 mockup，输出 `uiux-design.md`，并可在设计确认后构建经过截图对照验收的交互式前端原型。

语言：中文

![Skill](https://img.shields.io/badge/Codex-Skill-111827)
![Output](https://img.shields.io/badge/Output-UI%2FUX%20Design-blue)
![Image Generation](https://img.shields.io/badge/Image-Generation-7c3aed)
![Preview](https://img.shields.io/badge/Preview-Frontend%20Prototype-0f766e)
![Workflow](https://img.shields.io/badge/Workflow-Multi--Agent-ca8a04)
![Platform](https://img.shields.io/badge/Platform-Codex%20Only-111827)
![Status](https://img.shields.io/badge/Status-MVP-16a34a)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

> [!IMPORTANT]
> 本仓库提供的是 **OpenAI Codex Skill**，只能由支持 Skills 的 Codex 环境直接发现和调用。它不是 ChatGPT GPT、OpenAI API SDK、Claude Skill、Cursor Rule 或通用 Prompt 包。

---

## 一眼看懂

| 项目 | 内容 |
| --- | --- |
| Skill 名称 | `ai-interface-studio` |
| 调用方式 | `$ai-interface-studio` 或自然语言触发 |
| 核心目标 | 将产品想法推进为 UI/UX 设计，并可生成交互式前端预览 |
| 默认产物 | 设计系统图、页面 mockup、含开发交接契约的 `uiux-design.md`；前端预览按需生成 |
| 默认平台 | 桌面端 Web |
| 适合场景 | 后台系统、SaaS 控制台、CRM/ERP/OA、数据平台、内部工具 |
| 图片策略 | 单视口页面 1 张；长页面生成 1 张同尺寸全页缩略总览图 + 多张带重叠锚点的正常比例细节分段图；另加 1 张设计系统图 |
| 文档策略 | 单一主文档作为精确文案、字段、状态和前端预览规则来源 |
| 协作策略 | 协调、产品与 UX、视觉设计、前端实施、视觉验收角色分离 |
| 预览验收 | 同视口截图对照；阻断级和严重级视觉问题清零后才通过 |
| 能力边界 | 停止在前端原型，不实现后端、数据库、真实鉴权、部署和运维 |

---

## 这个仓库适合什么场景

你可以把 AI Interface Studio Skill 当作一个 **Codex UI/UX Design Skill**、**产品需求访谈工作流**、**界面方案生成器** 和 **交互式前端原型构建器**。

产品方向参考 [Google Stitch](https://stitch.withgoogle.com/) 的 idea-to-interface 体验：从自然语言或视觉参考出发，快速形成 UI，并继续得到可浏览的前端结果。AI Interface Studio Skill 在此基础上强调产品经理式访谈、生成前确认、结构化 `uiux-design.md` 和可追溯的开发交接契约。本项目为独立项目，与 Google 无隶属关系。

它适合处理这类请求：

- “帮我设计一个公司内部项目管理系统。”
- “我想做一个不模板化的 SaaS 后台，先问我问题再出设计。”
- “把这个业务需求整理成 UI/UX 方案，并生成页面 mockup。”
- “给这个 CRM/ERP/OA/数据平台做一套更有设计感的界面。”
- “设计确认后，再给我一个可以点击演示的前端预览。”

> [!IMPORTANT]
> AI Interface Studio Skill 不是单纯的图片生成器。它会通过角色分离的多 Agent 流程，把模糊需求推进为可确认的产品结构、页面清单、视觉概念、设计图、设计文档和可选交互原型。

> [!CAUTION]
> 生成图片里的小字、表格内容和字段名只作为视觉参考。精确文案、字段、状态、权限和前端预览规则以 `uiux-design.md` 为准。

> [!WARNING]
> 前端预览只用于设计评审和交互演示，使用 mock 数据与本地状态。Skill 不负责后端 API、数据库、真实鉴权、支付、外部系统集成、云资源、部署或生产运维。

---

## 兼容性与使用范围

AI Interface Studio Skill 依赖 Codex 的 Skills 加载机制，不能作为独立程序运行。

| 环境 | 支持情况 | 说明 |
| --- | --- | --- |
| Codex App | 支持 | 安装后新建会话，通过 `$ai-interface-studio` 调用 |
| Codex CLI | 支持 | 在目标工作目录启动 Codex，并在 Prompt 中调用 Skill |
| ChatGPT 网页版或桌面版 | 不直接支持 | ChatGPT 不会从本地 Codex skills 目录加载该 Skill |
| OpenAI API | 不直接支持 | 本仓库不是 API SDK，也没有独立 API 入口 |
| Claude、Cursor、Copilot 等其他 Agent | 不保证兼容 | 可以人工参考 Markdown，但不能按 Codex Skill 机制直接安装 |

Codex Skills 的具体可用性取决于当前 Codex 版本。相关概念见 [Codex Skills 官方文档](https://developers.openai.com/codex/skills)。

### 使用前提

- 已安装并登录支持 Skills 的 OpenAI Codex。
- 在需要保存设计产物的项目目录中启动 Codex。
- UI mockup 生成依赖当前 Codex 会话可用的 Image Generation 能力。
- 标准流程需要当前 Codex 会话支持子 Agent；不可用时会降级为分阶段单 Agent 执行，并明确说明视觉验收不是独立完成的。
- 可选前端预览通常需要本地提供 Node.js 与 npm、pnpm 或项目既有包管理器。

---

## 安装

### 使用 npx 安装（推荐）

macOS、Linux 和 Windows 均可使用社区通用的 Agent Skills 安装器：

```bash
npx skills add shi-YangYang/ai-interface-studio
```

按照安装器提示选择 Codex 和用户级安装范围即可。该命令会直接从 GitHub 获取仓库中的 `ai-interface-studio` Skill，不需要克隆仓库或手动复制目录。

> [!NOTE]
> `npx skills add` 由社区 Agent Skills 安装器提供，不是本仓库发布的 npm 软件包，也不是 OpenAI Codex 自带命令。使用该方式需要本地已安装 Node.js 和 npm。

### 使用 Codex Skill Installer

也可以在 Codex 会话中调用内置的 `$skill-installer`：

```text
$skill-installer 从 https://github.com/shi-YangYang/ai-interface-studio/tree/main/ai-interface-studio 安装
```

安装完成后，如果 Skill 没有立即出现在选择器中，请重启 Codex。随后可使用 `$ai-interface-studio` 调用。

---

## 使用

建议显式使用 `$ai-interface-studio` 调用。自然语言也可能触发 Skill，但显式调用更稳定，也能避免与普通前端开发请求混淆。

### Codex App

1. 在目标项目目录中打开 Codex。
2. 新建会话。
3. 在输入框中使用 `$ai-interface-studio` 开始需求访谈。

```text
$ai-interface-studio 使用多 Agent 协作帮我设计一个公司内部项目管理系统。先进行需求访谈，确认后生成 UI/UX 设计图、uiux-design.md 和开发交接契约。
```

### Codex CLI

在需要保存设计产物的目录中启动 Codex：

```bash
cd /path/to/your-project
codex '$ai-interface-studio 帮我从产品想法开始设计一个项目管理系统。'
```

PowerShell 同样可以使用单引号，避免 `$ai-interface-studio` 被当作变量展开：

```powershell
Set-Location C:\path\to\your-project
codex '$ai-interface-studio 帮我从产品想法开始设计一个项目管理系统。'
```

### 附加参考图片

在 Codex App 中可以直接附加截图、草图或参考图。在 Codex CLI 中可以使用 `-i`：

```bash
codex -i ./reference.png '$ai-interface-studio 参考这张图片的层级和密度，但不要照抄。先确认需求和页面清单。'
```

### 只生成 UI/UX，不生成前端预览

```text
$ai-interface-studio 只完成产品需求澄清、UI/UX 设计图、uiux-design.md 和开发交接契约，不生成前端预览。
```

### 包含交互式前端预览

```text
$ai-interface-studio 使用协调、视觉、前端实施和独立验收 Agent 完成需求访谈与 UI/UX 设计；设计确认后，再构建一个使用 mock 数据、可以浏览和点击演示的前端预览，不需要后端。
```

---

## 工作流基础

AI Interface Studio Skill 默认采用协调 Agent 驱动的五角色协作模式。

| 角色 | 核心职责 | 明确禁止 |
| --- | --- | --- |
| 协调 Agent | 用户沟通、阶段门、任务分派、冲突决策 | 不出最终 UI 图，不写前端代码，不自验收 |
| 产品与 UX Agent | 需求、流程、信息架构、页面与状态设计 | 不生成最终视觉图，不写前端代码 |
| 视觉设计 Agent | 设计系统、页面出图、视觉还原契约 | 不写前端代码 |
| 前端实施 Agent | 按批准图和契约实现前端预览 | 不修改设计来源，不自我验收 |
| 视觉验收 Agent | 同视口截图对照、记录 `VIS-###` 问题、通过或拒收 | 不修改前端代码 |

各 Agent 通过磁盘上的批准产物交接，而不是依赖协调 Agent 对长对话的摘要。前端实施和视觉验收 Agent 都必须查看原始 UI 图片。

### 阶段门

| 阶段门 | 通过条件 |
| --- | --- |
| G1 需求确认 | Requirement Confirmation、Page Inventory、Page Coverage Plan 已批准 |
| G2 视觉确认 | 设计系统图与全部目标页面 mockup 已批准 |
| G3 视觉契约冻结 | 每个待实现页面都有完整 Visual Fidelity Contract |
| G4 前端待验收 | 前端可运行，路由、目标视口截图和交互已准备 |
| G5 视觉验收通过 | 每页有参考图和浏览器截图证据，没有未关闭的 Blocker/Major `VIS-###` 问题 |

没有磁盘证据就不能进入下一阶段。

### 1. 产品经理式访谈

产品与 UX Agent 会按 3-5 个问题一轮追问，补齐：

- 项目名称和业务目标
- 目标用户与角色权限
- 核心业务流程
- 页面范围和信息架构
- 关键数据对象
- 视觉偏好和参考图
- 交付范围与限制条件

### 2. 需求确认

在生成图片前，Codex 会先输出确认稿：

- Requirement Confirmation
- Page Inventory
- Page Coverage Plan
- Visual Concept
- Assumptions And Risks

用户确认后才进入正式图片生成。

### 3. 视觉设计与页面出图

视觉设计 Agent 先生成 `00-design-system.png`，再生成页面 mockup，用于定义：

- 色彩系统
- 字体层级
- 间距和布局栅格
- 按钮、输入框、表格、卡片、状态标签
- 导航、筛选、弹窗、空状态、错误状态

### 4. 页面级 Mockup

Codex 会先判断页面的滚动模型：

- **单视口页面**：完整内容能在一个桌面视口中清晰展示，生成 1 张 mockup。
- **页面滚动**：页面内容超过一个视口，生成 1 张同尺寸全页缩略总览图，再按顶部、中段、底部生成多张正常比例细节 mockup。
- **内部滚动**：应用外壳保持固定，表格、画布或面板内部滚动，生成稳定工作区视图并在文档中说明滚动区域。

长页面不会被压缩进一张难以阅读的图片，也不会只生成首屏。确认阶段会先列出每个页面的完整内容顺序、覆盖策略、预计图片数量和每张图覆盖的区块。

全页缩略总览图的长宽与普通图片一致，但会把完整长页面缩小放入同一张图中，用来确认整页结构、上下衔接、区块节奏和视觉连续性。它不能单独作为前端细节实现依据。

细节分段图负责真实字号、组件、间距、表格、控件和局部视觉还原。相邻细节分段必须保留约 15-25% 的共享内容作为连续性锚点，避免图与图之间出现外壳错位、区块断裂、间距突变或组件样式漂移。如果同时构建前端预览，Codex 还会用浏览器完整页面截图检查最终页面从顶部到底部的连续性。

默认软上限改为 **8 张业务页面设计帧 + 1 张设计系统图**。长页面缩略总览图和每个细节分段都计为一帧；超过时 Codex 会先让用户确认优先级或分批生成。

### 5. UI/UX 设计文档与视觉还原契约

最终输出 `uiux-design.md`，包含：

- PRD 级产品上下文
- 用户角色与权限
- 信息架构
- 页面设计说明
- 页面滚动模型、完整内容顺序和长页覆盖策略
- 每页参考图、目标视口、外壳尺寸、区域比例和布局关系
- 字体层级、颜色、间距、圆角、边框、阴影、组件形态和内容密度
- 响应式变化与允许偏差
- 交互与状态
- 视觉规范
- 组件规范
- 响应式说明
- 前端预览规格
- 需求、流程、页面、组件、状态和验收条件的稳定 ID
- 路由与页面映射、组件清单、交互状态矩阵
- UI 数据契约和 API 能力需求
- 前端预览到生产项目的迁移说明
- 图片生成 prompts

视觉还原契约必须在编写前端代码前冻结。

### 6. 交互式前端预览（可选）

只有用户明确需要时才构建前端预览。预览用于验证：

- 页面导航和主要业务路径
- 表单、筛选、表格、标签页、弹窗和抽屉
- 加载、空状态、错误、禁用和权限受限状态
- 桌面端与移动端响应式表现

前端实施 Agent 必须先查看全部原始 UI 图，先实现并检查共享应用外壳，再分小批页面实现。预览使用 mock 数据、fixtures 和本地状态，并将 fixtures、mock services、UI types 与视觉组件分离。

### 7. 独立视觉验收

没有参与编码的视觉验收 Agent 会在与参考图相同的视口下截取浏览器页面，逐区域对照：

- 应用外壳、导航、内容边界与固定区域
- 页面结构、区域顺序、列宽比例和留白分布
- 长页面缩略总览图与细节分段锚点的滚动连续性
- 组件类型、数量、位置、尺寸与内容密度
- 字体层级、颜色、间距、圆角、边框、阴影和图标
- 响应式变化

验收结果写入 `visual-review.md`。所有 Blocker 和 Major 问题必须退回前端实施 Agent 修复并重新验收；完成后即停止，不继续开发后端或生产系统。

---

## 输出结构

默认输出目录：

```text
gpt-images/uiux/<project-slug>/
```

默认文件结构：

```text
gpt-images/uiux/<project-slug>/
├── 00-design-system.png
├── 01-login.png
├── 02-dashboard.png
├── 03-settings-overview.png
├── 03-settings-01-top.png
├── 03-settings-02-content.png
├── 03-settings-03-bottom.png
├── uiux-design.md
├── workflow-state.md
├── visual-review.md
└── review/
    └── PAGE-003-01-top.png
```

命名规则：

| 文件 | 含义 |
| --- | --- |
| `00-design-system.png` | 全局设计系统说明图 |
| `01-login.png` | 登录页 mockup |
| `02-dashboard.png` | 工作台 / 首页 mockup |
| `03-<page-name>.png` | 单视口页面 mockup |
| `03-<page-name>-overview.png` | 长页面同尺寸缩略总览图，用于整页结构和滚动连续性 |
| `03-<page-name>-01-top.png` | 长页面顶部视口 |
| `03-<page-name>-02-content.png` | 长页面中段视口，可继续顺序编号 |
| `03-<page-name>-03-bottom.png` | 长页面底部视口 |
| `uiux-design.md` | 主设计文档 |
| `workflow-state.md` | 协调 Agent 维护的阶段与产物状态，不作为设计事实来源 |
| `visual-review.md` | 包含前端预览时生成的独立视觉验收结果与 `VIS-###` 问题 |
| `review/` | 包含前端预览时保存的浏览器截图证据 |

如果用户要求前端预览，并且当前没有既有前端项目，默认创建：

```text
frontend-preview/<project-slug>/
```

该目录只包含用于设计评审的浏览器端原型。

---

## Prompt 与设计原则

AI Interface Studio Skill 会优先使用可实现的产品界面语言，而不是只做氛围图。

设计 prompt 默认强调：

1. **先结构，再视觉**  
   先明确页面目的、导航、内容区、组件和状态，再描述风格。

2. **每次必须有视觉概念名**  
   例如 `Signal Grid`、`Command Canvas`、`Quiet Control Room`，或根据业务定制的概念名。

3. **真实产品密度**  
   后台和内部工具要能支撑重复工作、扫描、比较、筛选和操作。

4. **避免模板化**  
   避免 Bootstrap/AdminLTE/Admin Dashboard 式通用后台感。

5. **避免单一色相统治**  
   避免只有紫蓝渐变、纯暗蓝科技风、单调玻璃拟态或大面积无信息装饰。

6. **按领域确定事实来源**
   `uiux-design.md` 负责文案、字段、状态和交互；批准的图片与 Visual Fidelity Contract 负责构图和视觉样式；前端预览必须经过独立截图对照验收。

7. **长页面必须连续覆盖**
   先确定页面的完整内容顺序，生成同尺寸缩略总览图，再生成带重叠锚点的正常比例细节分段图。每个确认区块都必须出现在批准图片中，细节分段之间不能出现明显接缝、重启或风格漂移。

---

## 能力边界

| 包含 | 不包含 |
| --- | --- |
| 产品需求访谈与确认 | 后端 API 和服务 |
| 信息架构与页面清单 | 数据库、迁移和持久化模型 |
| 视觉概念与设计系统 | 真实登录、账号和权限系统 |
| 页面级 UI mockup | 支付、邮件、消息和第三方系统集成 |
| `uiux-design.md` | 云资源、部署流水线和生产运维 |
| 可选交互式前端预览 | 生产级安全与完整业务逻辑 |

---

## 开发如何使用交付物

交付物按领域确定事实来源：

```text
需求、文案、字段、状态、交互：uiux-design.md
构图、层级、配色、字体、间距、组件外观：批准的 UI 图 + Visual Fidelity Contract
实现后的交互与响应式证据：通过视觉验收的前端预览
图片中的生成文字：仅作方向参考
```

`uiux-design.md` 中的开发交接契约会把需求、流程、页面、组件、状态、UI 数据需求、API 能力需求和验收条件连接起来。后续团队可以这样使用：

| 角色 | 使用方式 |
| --- | --- |
| 产品 | 用需求与流程 ID 确认范围，用验收条件判断交付结果 |
| 前端 | 复用或重写路由、组件、设计 tokens 和 UI 数据模型，并逐步替换 mock adapters |
| 后端 | 根据 API 能力需求设计正式接口，但不把 UI view model 直接当数据库结构 |
| QA | 从交互状态矩阵和 `AC-###` 验收条件生成测试用例 |
| 视觉验收 | 使用参考图、完整页面截图、同视口浏览器截图和 `VIS-###` 清单判断预览是否忠实 |

如果生产技术栈与预览一致，可以把预览作为前端起点；如果技术栈不同，则把预览作为可执行的视觉与交互规格，依据 `uiux-design.md` 重新实现。

---

## Skill 文件

| 路径 | 作用 |
| --- | --- |
| `ai-interface-studio/SKILL.md` | Skill 主入口，定义触发描述、核心规则和执行流程 |
| `ai-interface-studio/agents/openai.yaml` | Codex UI 元数据 |
| `ai-interface-studio/references/interview-checklist.md` | 产品需求访谈清单和确认稿格式 |
| `ai-interface-studio/references/image-prompt-patterns.md` | 设计系统图和页面 mockup 的 prompt 模板 |
| `ai-interface-studio/references/design-document-template.md` | `uiux-design.md` 文档结构模板 |
| `ai-interface-studio/references/frontend-preview.md` | 交互式前端预览的实现、验证和范围边界 |
| `ai-interface-studio/references/development-handoff.md` | 开发交接契约、追踪关系和验收标准 |
| `ai-interface-studio/references/multi-agent-workflow.md` | 多 Agent 角色、阶段门、上下文包和降级规则 |
| `ai-interface-studio/references/visual-fidelity-review.md` | 同视口视觉对照、严重程度、拒收与报告规则 |

仓库结构：

```text
.
├── .gitignore
├── README.md
└── ai-interface-studio/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── design-document-template.md
        ├── development-handoff.md
        ├── frontend-preview.md
        ├── image-prompt-patterns.md
        ├── interview-checklist.md
        ├── multi-agent-workflow.md
        └── visual-fidelity-review.md
```

---

## 开发与校验

本仓库只包含 Codex Skill，不需要独立构建。

如果本地有 Codex 的 `skill-creator` 系统 Skill，可以运行：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./ai-interface-studio
```

如果环境缺少 `PyYAML`：

```bash
python3 -m pip install PyYAML
```

成功时会输出：

```text
Skill is valid!
```

---

## 许可证

本项目采用 [Apache License 2.0](LICENSE) 开源许可证。
