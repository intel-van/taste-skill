<p align="center">
  <img src="assets/readme-banner.png" alt="Taste Skill — 让 AI Agent 构建精品前端" width="100%" />
</p>

# Taste Skill

<p align="center">
  <em>面向 AI Agent 的反模板化前端框架</em>
</p>

<p align="center">
  <a href="https://tasteskill.dev" title="Taste Skill — tasteskill.dev">
    <img src="assets/taste-skill-logo.webp" width="80" height="80" alt="Taste Skill" />
  </a>
</p>

<p align="center">
  <a href="https://tasteskill.dev">
    <img src="https://img.shields.io/badge/OPEN-tasteskill.dev-%23a855f7?style=for-the-badge&labelColor=%230f172a" alt="打开 tasteskill.dev" />
  </a>
</p>

便携式 **Agent Skills**，提升 AI 构建界面的品质：更强的布局、排版、动效和间距，告别千篇一律的模板化 UI。本仓库同时包含**图片生成技能**，用于制作参考面板（网页、移动端、品牌套件）。将它们与 ChatGPT Images 或类似生成器配合使用，再将产出交给 Codex、Cursor 或 Claude Code 实现。

<p align="center">
<a href="https://github.com/Leonxlnx/taste-skill/stargazers"><img src="https://img.shields.io/github/stars/Leonxlnx/taste-skill?style=for-the-badge&logo=github&labelColor=1e293b&color=fbbf24" alt="GitHub stars"/></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-fbbf24?style=for-the-badge&labelColor=1e293b" alt="MIT 许可证"/></a>
<a href="#installing"><img src="https://img.shields.io/badge/Tools-Codex%20%C2%B7%20Cursor%20%C2%B7%20Claude-111827?style=for-the-badge&labelColor=1e293b" alt="支持的工具"/></a>
<a href="https://www.tasteskill.dev/changelog"><img src="https://img.shields.io/badge/Changelog-Latest-059669?style=for-the-badge&labelColor=1e293b" alt="更新日志"/></a>
</p>

## 声明

Taste Skill 没有任何官方代币、币或加密项目。任何使用我名字、头像或项目名称的代币均与我无关，且未获我认可。

<p align="center"><sub><a href="#声明">声明</a> · <a href="#安装">安装</a> · <a href="#技能列表">技能列表</a> · <a href="#设置仅-taste-skill">设置</a> · <a href="#示例">示例</a> · <a href="#赞助项目">赞助</a> · <a href="#深度阅读">研究资料</a> · <a href="#常见问题">常见问题</a> · <a href="#许可证">许可证</a></sub></p>

## 反馈与贡献

欢迎提交反馈。建议和 Bug 报告请通过以下渠道：

- 在 GitHub 上提交 Pull Request 或 Issue
- 私信 [@lexnlin](https://x.com/lexnlin) 或 [@blueemi99](https://x.com/blueemi99)
- 发送邮件至 [hello@tasteskill.dev](mailto:hello@tasteskill.dev)

## 安装

[`npx skills add`](https://github.com/vercel-labs/agent-skills) CLI 会自动扫描本仓库的 `skills/` 文件夹，**以下所有技能（代码类和图片生成类）安装方式一致。**

```bash
npx skills add https://github.com/Leonxlnx/taste-skill
```

按**安装名称**（SKILL 文件 frontmatter 中的 `name` 字段，而非文件夹名称）安装单个技能：

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

你也可以将任意 `SKILL.md` 直接复制到你的项目中，或粘贴到 ChatGPT / Codex 对话中使用。

### 从旧版本升级

默认的 `taste-skill`（安装名 `design-taste-frontend`）目前为 **v2（实验版）**，是对原始 v1 的重大重写。如果你已安装 v1，只需重新运行安装命令即可升级：

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

安装名称未变，因此无需更新脚本。新版 SKILL.md 会原地替换旧版。

如需锁定 v1 的确切行为：

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend-v1"
```

详见 [CHANGELOG.md](CHANGELOG.md) 中 v1 到 v2 的完整变更说明。

## 技能列表

每个技能专注一个任务，无需同时使用全部。**实现类技能**输出代码。**图片生成类技能**仅输出参考图片。

`安装名称` 列即为 `--skill` 参数所需的值。

| 技能（文件夹） | 安装名称 | 说明 |
| --- | --- | --- |
| **taste-skill** | `design-taste-frontend` | 🆕 **v2（实验版）** — 默认技能的重大重写。读取需求、推断设计语言、调节三个旋钮（VARIANCE / MOTION / DENSITY）。包含需求推断、设计系统映射、em-dash 禁令、GSAP 标准代码骨架、重设计审核协议、严格预检清单。正迭代至 v2.0.0 稳定版。 |
| **taste-skill-v1** | `design-taste-frontend-v1` | 原始 v1 版本，为依赖其确切行为的项目保留。仅当 v2 默认版本在你的工作流中导致问题时使用。 |
| **gpt-tasteskill** | `gpt-taste` | 面向 GPT/Codex 的严格变体：更高的布局方差、更强的 GSAP 指导、激进的反模板化。 |
| **image-to-code-skill** | `image-to-code` | 图片优先工作流：生成网站参考图 → 分析 → 实现前端代码。 |
| **redesign-skill** | `redesign-existing-projects` | 现有项目改造：先审计 UI，再修复布局、间距、层级、样式。 |
| **soft-skill** | `high-end-visual-design` | 精致、沉稳、高档的 UI，采用柔和对比、留白、 premium 字体、弹性动效。 |
| **output-skill** | `full-output-enforcement` | 当模型产出半成品时：强制完整输出，禁止占位注释。 |
| **minimalist-skill** | `minimalist-ui` | 编辑式产品 UI（Notion / Linear 风格），克制的调色板，清晰的结构。 |
| **brutalist-skill** | `industrial-brutalist-ui` | 硬朗的机械风格：瑞士字体、锐利对比、实验性布局。 |
| **stitch-skill** | `stitch-design-taste` | Google Stitch 兼容规则，附带可选的 `DESIGN.md` 导出格式。 |

### 图片生成技能

此类技能仅生成设计图片（不含代码）。配合 ChatGPT Images、Codex 图片模式或任何支持图片生成的 Agent 使用。

| 技能（文件夹） | 安装名称 | 说明 |
| --- | --- | --- |
| **imagegen-frontend-web** | `imagegen-frontend-web` | 网站构图：首页、落地页、多区块页面，强调排版、间距、反模板化艺术指导。 |
| **imagegen-frontend-mobile** | `imagegen-frontend-mobile` | 移动端屏幕与流程：iOS / Android / 跨平台、原型图、清晰字体、连贯成套。 |
| **brandkit** | `brandkit` | 品牌套件面板：Logo 方向、调色板、字体、各类别的品牌应用。 |

### 我该用哪个？

- 从 **taste-skill** 开始，作为最安全的通用默认项（目前为 v2 实验版，详见 [CHANGELOG](CHANGELOG.md)）。
- 如果你依赖原始 taste-skill 的确切行为，安装 **taste-skill-v1**。
- 需要更严格的 GPT/Codex 规则和动效/布局强制时，使用 **gpt-taste**。
- 需要图片 → 分析 → 代码的网站工作流，使用 **image-to-code-skill**。
- 需要改进现有代码库而非从头设计，使用 **redesign-skill**。
- 视觉方向已确定时，叠加 **soft-skill**、**minimalist-skill** 或 **brutalist-skill**。
- Agent 不断截断输出时，添加 **output-skill**。
- 交付物是**图片**（构图、流程、品牌面板）时，使用 **imagegen-frontend-web**、**imagegen-frontend-mobile** 或 **brandkit**，再将结果交给编码 Agent。

### 图片优先技巧

使用 **image-to-code-skill** 时，在提示词中声明工作流，例如：`follow the skill: generate images, then analyze, then code`。

### ChatGPT Images 与 Codex

将 **`imagegen-frontend-web`**、**`imagegen-frontend-mobile`** 或 **`brandkit`** 附上或粘贴到对话中，请求所需画面，然后将渲染结果交给 Codex、Cursor 或 Claude Code。如需一个工作流同时完成参考图生成和代码实现，使用 **image-to-code-skill**。

## 设置（仅 taste-skill）

文件顶部的数字为 1-10 档旋钮：

- **DESIGN_VARIANCE**：布局实验性（低值：居中/清爽 · 高值：不对称/现代）
- **MOTION_INTENSITY**：动效深度（低值：悬停 · 高值：滚动/磁吸）
- **VISUAL_DENSITY**：每屏信息密度（低值：宽敞 · 高值：密集仪表盘）

## 示例

使用 taste-skill 创建的示例：

<p>
  <img src="examples/floria-top.webp" width="400" />
  <img src="examples/floria-bottom.webp" width="400" />
</p>

## 赞助项目

如果 Taste Skill 对你有所帮助，请考虑赞助：

[在 GitHub 上赞助](https://github.com/sponsors/Leonxlnx)

### 当前赞助者

<a href="https://github.com/dnakov"><img src="https://github.com/dnakov.png" width="40" height="40" style="border-radius:50%" alt="dnakov" title="dnakov" /></a>
<a href="https://github.com/AkramReshad"><img src="https://github.com/AkramReshad.png" width="40" height="40" style="border-radius:50%" alt="AkramReshad" title="AkramReshad" /></a>
<a href="https://github.com/ajmalaksar25"><img src="https://github.com/ajmalaksar25.png" width="40" height="40" style="border-radius:50%" alt="ajmalaksar25" title="ajmalaksar25" /></a>
<a href="https://github.com/krikkkk"><img src="https://github.com/krikkkk.png" width="40" height="40" style="border-radius:50%" alt="krikkkk" title="krikkkk" /></a>
<a href="https://github.com/navanchauhan"><img src="https://github.com/navanchauhan.png" width="40" height="40" style="border-radius:50%" alt="navanchauhan" title="navanchauhan" /></a>
<a href="https://github.com/robinebers"><img src="https://github.com/robinebers.png" width="40" height="40" style="border-radius:50%" alt="robinebers" title="robinebers" /></a>
<a href="https://github.com/JKc66"><img src="https://github.com/JKc66.png" width="40" height="40" style="border-radius:50%" alt="JKc66" title="JKc66" /></a>
<a href="https://github.com/u2393696078-rgb"><img src="https://github.com/u2393696078-rgb.png" width="40" height="40" style="border-radius:50%" alt="u2393696078-rgb" title="u2393696078-rgb" /></a>
<a href="https://github.com/a-human-created-this"><img src="https://github.com/a-human-created-this.png" width="40" height="40" style="border-radius:50%" alt="a-human-created-this" title="a-human-created-this" /></a>
<a href="https://github.com/AtharvaJaiswal005"><img src="https://github.com/AtharvaJaiswal005.png" width="40" height="40" style="border-radius:50%" alt="AtharvaJaiswal005" title="AtharvaJaiswal005" /></a>
<a href="https://github.com/ghughes7"><img src="https://github.com/ghughes7.png" width="40" height="40" style="border-radius:50%" alt="ghughes7" title="ghughes7" /></a>
<a href="https://github.com/mccun934"><img src="https://github.com/mccun934.png" width="40" height="40" style="border-radius:50%" alt="mccun934" title="mccun934" /></a>

<p align="center">
 <a href="https://www.star-history.com/leonxlnx/taste-skill">
  <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/badge?repo=Leonxlnx/taste-skill&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/badge?repo=Leonxlnx/taste-skill" />
   <img alt="Star History 排名" src="https://api.star-history.com/badge?repo=Leonxlnx/taste-skill" />
  </picture>
 </a>
</p>

## 深度阅读

影响本技能设计的背景研究资料存放在 [`research/`](research/) 目录下：

- **[LLM 输出截断研究](research/laziness/README.md)** — 分析 LLM 产生不完整输出的原因及修复方法
  - [RLHF 与计算经济学](research/laziness/root-causes/rlhf-and-compute.md) — 强化学习如何引入简洁性偏好
  - [训练数据偏差](research/laziness/root-causes/training-data-bias.md) — 占位符模式从代码传播到模型输出
  - [认知捷径](research/laziness/root-causes/cognitive-shortcuts.md) — 模型在复杂任务上走捷径的经验证据
  - [输出限制](research/laziness/root-causes/output-limits.md) — 上下文窗口不对称与消费级截断机制
  - [参数调优](research/laziness/remediation/parameter-tuning.md) — Temperature、Top-p 等参数配置
  - [提示词工程](research/laziness/remediation/prompt-engineering.md) — 结构化的提示词技术
  - [架构模式](research/laziness/remediation/architectural-patterns.md) — MCP 集成与懒加载技能
  - [参考提示词](research/laziness/remediation/reference-prompts.md) — 强制完整输出的现成提示词模板
  - [实验结果](research/laziness/findings/empirical-results.md) — 2025 年受控实验数据
  - [参考文献](research/laziness/findings/references.md) — 引用研究及扩展阅读

## 常见问题

**与其他 AI 设计技能有何不同？**  
多种专用变体、关键技能中的可调旋钮、基于专门研究的反重复规则。所有技能均框架无关，适用于主流编码 Agent。

**是否支持 React、Vue、Svelte？**  
支持。规则针对设计意图，而非特定框架 API。

**什么是 SKILL.md？**  
一种便携式指令文件，Agent 可自动加载；通过 `npx skills add` 安装，或直接复制到仓库或对话中。

**图片生成技能是否也能通过 `npx skills add` 安装？**  
可以。它们与代码技能一同位于 `skills/` 目录下，同一 CLI 即可发现。

## 许可证

[MIT License](LICENSE) · Copyright (c) 2026 Leonxlnx

---

[← 返回顶部](#taste-skill) · [📋 更新日志](CHANGELOG.md) · [📚 研究资料](research/)
