# All-Dry-Design

面向 Codex 的产品需求 → UI/UX 设计工作流 Skill。  
用产品经理式访谈补齐需求，用强视觉概念约束摆脱模板化后台，用 Image Generation 生成页面级 mockup，并输出可交付的 `uiux-design.md`。

语言：中文

![Skill](https://img.shields.io/badge/Codex-Skill-111827)
![Output](https://img.shields.io/badge/Output-UI%2FUX%20Design-blue)
![Image Generation](https://img.shields.io/badge/Image-Generation-7c3aed)
![Status](https://img.shields.io/badge/Status-MVP-16a34a)
![License](https://img.shields.io/badge/License-Unspecified-lightgrey)

---

## 一眼看懂

| 项目 | 内容 |
| --- | --- |
| Skill 名称 | `all-dry-design` |
| 调用方式 | `$all-dry-design` 或自然语言触发 |
| 核心目标 | 将产品想法整理为 UI/UX 设计方案 |
| 默认产物 | 设计系统图、页面 mockup、`uiux-design.md` |
| 默认平台 | 桌面端 Web |
| 适合场景 | 后台系统、SaaS 控制台、CRM/ERP/OA、数据平台、内部工具 |
| 图片策略 | 每个页面 1 张 mockup，另加 1 张设计系统图 |
| 文档策略 | 单一主文档作为精确文案、字段、状态和实现说明来源 |

---

## 这个仓库适合什么场景

你可以把 All-Dry-Design 当作一个 **Codex UI/UX Design Skill**、**产品需求访谈工作流**、**后台系统视觉方案生成器** 和 **前端实现前的设计交付模板**。

它适合处理这类请求：

- “帮我设计一个公司内部项目管理系统。”
- “我想做一个不模板化的 SaaS 后台，先问我问题再出设计。”
- “把这个业务需求整理成 UI/UX 方案，并生成页面 mockup。”
- “给这个 CRM/ERP/OA/数据平台做一套更有设计感的界面。”

> [!IMPORTANT]
> All-Dry-Design 不是单纯的图片生成器。它的重点是把模糊需求推进为可确认的产品结构、页面清单、视觉概念、设计图和实现文档。

> [!CAUTION]
> 生成图片里的小字、表格内容和字段名只作为视觉参考。精确文案、字段、状态、权限和前端实现说明以 `uiux-design.md` 为准。

---

## 安装

安装前建议先检查本地是否已经存在同名 Skill，避免覆盖已有版本。

```bash
test -e "${CODEX_HOME:-$HOME/.codex}/skills/all-dry-design" \
  && echo "all-dry-design skill already exists; stop before overwriting" \
  && exit 1
```

### Codex 手动安装

在本仓库根目录执行：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R all-dry-design "${CODEX_HOME:-$HOME/.codex}/skills/all-dry-design"
```

安装后重启 Codex，让新的 `$all-dry-design` Skill 生效。

### 开发模式安装

如果你还在本地开发这个 Skill，可以使用软链接：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "$PWD/all-dry-design" "${CODEX_HOME:-$HOME/.codex}/skills/all-dry-design"
```

这样你修改仓库里的 `all-dry-design/` 后，Codex skills 目录会同步看到变更。

### 更新

如果使用复制安装，更新时重新复制 Skill 文件夹：

```bash
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/all-dry-design"
cp -R all-dry-design "${CODEX_HOME:-$HOME/.codex}/skills/all-dry-design"
```

如果使用软链接安装，拉取或修改仓库即可。

---

## 快速使用

### 显式调用

```text
$all-dry-design 帮我设计一个公司内部项目管理系统，先从需求访谈开始，确认后生成 UI/UX 设计图和设计文档。
```

### 自然语言调用

```text
帮我把一个不模板化的 SaaS 后台系统从产品需求整理到 UI/UX 方案，先问我问题，确认页面后再出图。
```

### 带参考风格

```text
$all-dry-design 我想做一个供应链运营平台，可以参考我发的图片风格，但不要照抄。先访谈需求，再确认页面清单和视觉概念。
```

### 只生成设计，不生成前端

```text
$all-dry-design 只做产品需求澄清、UI/UX 设计图和 uiux-design.md，暂时不要生成前端代码。
```

---

## 工作流基础

All-Dry-Design 默认按 5 个阶段执行。

### 1. 产品经理式访谈

Codex 会按 3-5 个问题一轮追问，补齐：

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
- Visual Concept
- Assumptions And Risks

用户确认后才进入正式图片生成。

### 3. 设计系统图

先生成 `00-design-system.png`，用于定义：

- 色彩系统
- 字体层级
- 间距和布局栅格
- 按钮、输入框、表格、卡片、状态标签
- 导航、筛选、弹窗、空状态、错误状态

### 4. 页面级 Mockup

默认每个业务页面生成 1 张桌面端 mockup：

- 登录页
- 工作台 / Dashboard
- 列表页
- 详情页
- 表单页
- 审批 / 权限 / 设置等业务页面

默认软上限为 8 个业务页面 + 1 张设计系统图。页面更多时，Codex 会先让用户确认优先级。

### 5. UI/UX 设计文档

最终输出 `uiux-design.md`，包含：

- PRD 级产品上下文
- 用户角色与权限
- 信息架构
- 页面设计说明
- 交互与状态
- 视觉规范
- 组件规范
- 响应式说明
- 前端实现建议
- 图片生成 prompts

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
├── 03-<page-name>.png
└── uiux-design.md
```

命名规则：

| 文件 | 含义 |
| --- | --- |
| `00-design-system.png` | 全局设计系统说明图 |
| `01-login.png` | 登录页 mockup |
| `02-dashboard.png` | 工作台 / 首页 mockup |
| `03-<page-name>.png` | 其他页面 mockup |
| `uiux-design.md` | 主设计文档 |

---

## Prompt 与设计原则

All-Dry-Design 会优先使用可实现的产品界面语言，而不是只做氛围图。

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

6. **文档是来源，图片是方向**  
   图片负责视觉方向，`uiux-design.md` 负责精确实现依据。

---

## Skill 文件

| 路径 | 作用 |
| --- | --- |
| `all-dry-design/SKILL.md` | Skill 主入口，定义触发描述、核心规则和执行流程 |
| `all-dry-design/agents/openai.yaml` | Codex UI 元数据 |
| `all-dry-design/references/interview-checklist.md` | 产品需求访谈清单和确认稿格式 |
| `all-dry-design/references/image-prompt-patterns.md` | 设计系统图和页面 mockup 的 prompt 模板 |
| `all-dry-design/references/design-document-template.md` | `uiux-design.md` 文档结构模板 |
| `all-dry-design/references/frontend-preview.md` | 可选前端预览实现和验证规则 |

仓库结构：

```text
.
├── .gitignore
├── README.md
└── all-dry-design/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── design-document-template.md
        ├── frontend-preview.md
        ├── image-prompt-patterns.md
        └── interview-checklist.md
```

---

## 开发与校验

本仓库只包含 Codex Skill，不需要独立构建。

如果本地有 Codex 的 `skill-creator` 系统 Skill，可以运行：

```bash
python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./all-dry-design
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

本仓库当前未声明开源许可证。
