# 代码资产盘点文档

> 盘点日期：2026年6月15日  
> 盘点人：AI Assistant  
> 版本：v1.0

---

## 1. 项目概览

**项目名称：** Taste Skill  
**项目定位：** 面向 AI Agent 的反模板化前端框架  
**许可证：** MIT License  
**主要功能：** 提供便携式 Agent Skills，提升 AI 构建界面的品质

### 1.1 核心价值主张

- 更强的布局、排版、动效和间距
- 告别千篇一律的模板化 UI
- 框架无关，适用于主流编码 Agent（Codex、Cursor、Claude Code）

---

## 2. 目录结构

```
/root/code/taste-skill/
├── _config.yml              # GitHub Pages 配置（Jekyll）
├── .git/                    # Git 仓库
├── .github/                 # GitHub 配置
│   ├── copilot-instructions.md
│   └── FUNDING.yml
├── assets/                  # 静态资源
│   ├── readme-banner.png
│   └── taste-skill-logo.webp
├── CHANGELOG.md             # 版本更新日志
├── examples/                # 示例文件
├── LICENSE                  # MIT 许可证
├── README.md                # 项目主文档
├── research/                # 研究资料
│   ├── laziness/            # LLM 输出截断研究
│   └── README.md
├── skill.sh                 # 本地技能注册表脚本
└── skills/                  # 核心技能模块（14个子目录）
    ├── brandkit/            # 品牌套件图片生成
    ├── brutalist-skill/     # 工业粗野主义UI
    ├── gpt-tasteskill/      # GPT/Codex 专用变体
    ├── image-to-code-skill/ # 图片转代码工作流
    ├── imagegen-frontend-mobile/ # 移动端图片生成
    ├── imagegen-frontend-web/    # 网站图片生成
    ├── llms.txt             # 技能描述文件
    ├── minimalist-skill/    # 极简主义UI
    ├── output-skill/        # 强制完整输出
    ├── redesign-skill/      # 现有项目改造
    ├── soft-skill/          # 高端柔和UI
    ├── stitch-skill/        # Google Stitch 兼容
    ├── taste-skill-v1/      # 原始 v1 版本
    └── taste-skill/         # 核心技能（v2实验版）
```

---

## 3. 技能模块清单

### 3.1 设计规范类技能（6个）

| 技能名称 | 安装名称 | 文件数 | 代码行数 | 核心功能 |
|---------|---------|--------|----------|----------|
| taste-skill | `design-taste-frontend` | 1 | 1206 | v2实验版，默认技能，包含需求推断、设计系统映射、三个可调旋钮 |
| taste-skill-v1 | `design-taste-frontend-v1` | 1 | 226 | 原始v1版本，为兼容性保留 |
| gpt-tasteskill | `gpt-taste` | 1 | 74 | 面向 GPT/Codex 的严格变体 |
| minimalist-skill | `minimalist-ui` | 1 | 85 | 编辑式产品 UI（Notion/Linear 风格） |
| brutalist-skill | `industrial-brutalist-ui` | 1 | 92 | 工业粗野主义 UI |
| soft-skill | `high-end-visual-design` | 1 | 98 | 高端柔和 UI |

### 3.2 图像生成类技能（3个）

| 技能名称 | 安装名称 | 文件数 | 代码行数 | 核心功能 |
|---------|---------|--------|----------|----------|
| imagegen-frontend-web | `imagegen-frontend-web` | 1 | 987 | 网站构图图片生成 |
| imagegen-frontend-mobile | `imagegen-frontend-mobile` | 1 | 1465 | 移动端屏幕与流程生成 |
| brandkit | `brandkit` | 1 | 798 | 品牌套件面板生成 |

### 3.3 功能扩展类技能（4个）

| 技能名称 | 安装名称 | 文件数 | 代码行数 | 核心功能 |
|---------|---------|--------|----------|----------|
| image-to-code-skill | `image-to-code` | 1 | 1228 | 图片优先工作流（生成→分析→实现） |
| redesign-skill | `redesign-existing-projects` | 1 | 178 | 现有项目改造（审计→修复） |
| output-skill | `full-output-enforcement` | 1 | 49 | 强制完整输出，禁止占位符 |
| stitch-skill | `stitch-design-taste` | 2 | 305 | Google Stitch 兼容规则 |

### 3.4 索引文件

| 文件名 | 行数 | 用途 |
|--------|------|------|
| llms.txt | 13 | 所有技能的简要描述索引 |

---

## 4. 代码统计

### 4.1 文件数量统计

| 类别 | 文件数量 |
|------|----------|
| 技能模块文件 | 14 |
| 文档文件 | 15 |
| 配置文件 | 3 |
| 资源文件 | 2 |
| **总计** | **34** |

### 4.2 代码行数统计

| 技能类别 | 代码行数 | 占比 |
|----------|----------|------|
| 设计规范类 | 1781 | 26.2% |
| 图像生成类 | 3250 | 47.8% |
| 功能扩展类 | 1760 | 25.9% |
| 索引文件 | 13 | 0.2% |
| **总计** | **6804** | 100% |

### 4.3 核心技能详细分析

#### taste-skill（v2实验版）
- **文件路径：** `skills/taste-skill/SKILL.md`
- **代码行数：** 1206行
- **核心特性：**
  - §0 Brief Inference（需求推断）
  - §2 设计系统映射
  - §5 动画规范（GSAP/Motion）
  - §8 暗黑模式协议
  - §9 AI Tells 禁令（含 em-dash 禁令）
  - §11 重设计协议
  - §12 Block Library 契约
  - §13 明确排除范围
  - §14 最终预检清单

#### image-to-code-skill
- **文件路径：** `skills/image-to-code-skill/SKILL.md`
- **代码行数：** 1228行
- **工作流程：**
  1. 图像生成
  2. 图像分析
  3. 前端实现

---

## 5. 技术栈

### 5.1 前端框架支持
- React
- Vue
- Svelte
- 框架无关设计

### 5.2 CSS 工具
- Tailwind CSS v4（默认）
- Tailwind CSS v3（兼容）

### 5.3 动画库
- GSAP（高级滚动动画）
- Motion（原 Framer Motion）

### 5.4 图标库（优先级顺序）
1. Phosphor
2. HugeIcons
3. Radix
4. Tabler

### 5.5 字体
- Geist 等高端字体

---

## 6. 核心特性

### 6.1 三个可调旋钮

| 旋钮名称 | 功能 | 范围 |
|----------|------|------|
| DESIGN_VARIANCE | 布局实验性 | 低值：居中/清爽 · 高值：不对称/现代 |
| MOTION_INTENSITY | 动效深度 | 低值：悬停 · 高值：滚动/磁吸 |
| VISUAL_DENSITY | 每屏信息密度 | 低值：宽敞 · 高值：密集仪表盘 |

### 6.2 反模板化设计
- 强制打破 AI 默认输出模式
- 严格禁止 em-dash（—）
- 禁止装饰性状态点
- 禁止滚动提示

### 6.3 严格预检清单
- 每个 CTA 必须通过 WCAG AA 对比度检查
- Hero 区域标题 ≤ 2 行
- 导航栏单行显示，高度 ≤ 80px

---

## 7. 文档清单

### 7.1 主要文档

| 文档名称 | 路径 | 用途 |
|----------|------|------|
| README.md | `/root/code/taste-skill/README.md` | 项目主文档 |
| CHANGELOG.md | `/root/code/taste-skill/CHANGELOG.md` | 版本更新日志 |
| LICENSE | `/root/code/taste-skill/LICENSE` | MIT 许可证 |
| CODE_ASSETS_INVENTORY.md | `/root/code/taste-skill/CODE_ASSETS_INVENTORY.md` | 本文档 |

### 7.2 技能文档

| 文档名称 | 路径 | 用途 |
|----------|------|------|
| SKILL.md（各技能） | `skills/*/SKILL.md` | 技能详细说明 |
| DESIGN.md | `skills/stitch-skill/DESIGN.md` | 设计系统示例 |
| llms.txt | `skills/llms.txt` | 技能索引 |

### 7.3 研究文档

| 文档名称 | 路径 | 用途 |
|----------|------|------|
| README.md | `research/README.md` | 研究资料索引 |
| LLM 输出截断研究 | `research/laziness/README.md` | 核心研究报告 |
| 根因分析 | `research/laziness/root-causes/*.md` | 4篇根因分析 |
| 修复方案 | `research/laziness/remediation/*.md` | 4篇修复方案 |
| 实验结果 | `research/laziness/findings/*.md` | 2篇实验报告 |

---

## 8. Git 提交历史

### 8.1 提交记录

| 提交哈希 | 提交信息 | 类型 |
|----------|----------|------|
| b0903a8 | docs: 文档规范化整改 | 文档 |
| 3c7017d | feat(skill): round-5 hardening from test-13/14/15 + test-16/17/18 (all Opus 4.7) | 功能 |

### 8.2 最近变更内容

**文档规范化整改（b0903a8）：**
- 更新 README.md（186行变更）
- 添加 _config.yml（GitHub Pages 配置）
- 更新 CHANGELOG.md
- 更新研究文档结构

**技能功能强化（3c7017d）：**
- 基于测试结果进行第5轮强化
- 使用 Opus 4.7 模型进行优化

---

## 9. 差异分析

### 9.1 现有文档与实际代码的差异

经过对比分析，发现以下差异：

1. **文档完整性：**
   - ✅ README.md 完整描述了项目功能和技能列表
   - ✅ CHANGELOG.md 记录了版本更新历史
   - ✅ 各技能 SKILL.md 提供了详细说明
   - ❌ 缺少专门的代码资产盘点文档（本文档填补此空白）

2. **技能模块完整性：**
   - ✅ 所有技能模块均有对应的 SKILL.md 文件
   - ✅ 技能索引文件 llms.txt 完整
   - ✅ 代码行数与文档描述相符

3. **文档一致性：**
   - ✅ README.md 中的技能列表与实际目录结构一致
   - ✅ 安装名称与 SKILL.md 中的 name 字段一致
   - ✅ 版本信息（v1/v2）准确反映

### 9.2 建议改进项

1. **添加版本号管理：**
   - 建议为项目添加统一的版本号管理
   - 当前版本信息分散在各处

2. **完善示例文档：**
   - 建议为每个技能添加使用示例
   - 当前仅 README.md 中有简单示例

3. **添加贡献指南：**
   - 建议添加 CONTRIBUTING.md 文件
   - 明确贡献流程和代码规范

---

## 10. 总结

### 10.1 资产概况

- **总文件数：** 34个
- **总代码行数：** 6804行
- **技能模块数：** 14个
- **文档文件数：** 15个

### 10.2 资产质量评估

| 评估维度 | 评分 | 说明 |
|----------|------|------|
| 文档完整性 | ⭐⭐⭐⭐ | 主要文档齐全，缺少资产盘点 |
| 代码质量 | ⭐⭐⭐⭐⭐ | 技能模块结构清晰，功能明确 |
| 模块化程度 | ⭐⭐⭐⭐⭐ | 高度模块化，每个技能独立 |
| 可维护性 | ⭐⭐⭐⭐ | 文档完善，易于理解 |

### 10.3 下一步建议

1. **定期更新本文档：** 建议每次重大变更后更新资产盘点
2. **添加自动化检查：** 考虑添加脚本自动统计代码行数
3. **完善测试覆盖：** 为技能模块添加测试用例

---

## 附录

### A. 文件清单

```
/root/code/taste-skill/
├── _config.yml
├── .github/
│   ├── copilot-instructions.md
│   └── FUNDING.yml
├── assets/
│   ├── readme-banner.png
│   └── taste-skill-logo.webp
├── CHANGELOG.md
├── CODE_ASSETS_INVENTORY.md
├── examples/
├── LICENSE
├── README.md
├── research/
│   ├── laziness/
│   │   ├── findings/
│   │   │   ├── empirical-results.md
│   │   │   └── references.md
│   │   ├── README.md
│   │   ├── remediation/
│   │   │   ├── architectural-patterns.md
│   │   │   ├── parameter-tuning.md
│   │   │   ├── prompt-engineering.md
│   │   │   └── reference-prompts.md
│   │   └── root-causes/
│   │       ├── cognitive-shortcuts.md
│   │       ├── output-limits.md
│   │       ├── rlhf-and-compute.md
│   │       └── training-data-bias.md
│   └── README.md
├── skill.sh
└── skills/
    ├── brandkit/
    │   └── SKILL.md
    ├── brutalist-skill/
    │   └── SKILL.md
    ├── gpt-tasteskill/
    │   └── SKILL.md
    ├── image-to-code-skill/
    │   └── SKILL.md
    ├── imagegen-frontend-mobile/
    │   └── SKILL.md
    ├── imagegen-frontend-web/
    │   └── SKILL.md
    ├── llms.txt
    ├── minimalist-skill/
    │   └── SKILL.md
    ├── output-skill/
    │   └── SKILL.md
    ├── redesign-skill/
    │   └── SKILL.md
    ├── soft-skill/
    │   └── SKILL.md
    ├── stitch-skill/
    │   ├── DESIGN.md
    │   └── SKILL.md
    ├── taste-skill/
    │   └── SKILL.md
    └── taste-skill-v1/
        └── SKILL.md
```

---

**文档结束**
