# 安全架构文档

> 文档版本：v1.0  
> 更新日期：2026年6月15日  
> 维护人：AI Assistant

---

## 1. 概述

Taste Skill 是一个面向 AI Agent 的前端设计技能集合，其安全架构主要围绕以下几个方面：

1. **代码生成安全** - 确保生成的前端代码安全可靠
2. **AI Agent 交互安全** - 防止 AI 生成不安全的代码模式
3. **依赖管理安全** - 控制第三方依赖的安全风险
4. **部署安全** - 确保技能文件的安全分发

---

## 2. 安全原则

### 2.1 最小权限原则

- 技能文件仅包含设计规范和代码模板
- 不包含可执行代码或脚本
- 用户需自行审查生成的代码

### 2.2 输入验证

- 所有技能输入（Brief）需经过推断验证
- §0 Brief Inference 阶段进行需求验证
- 拒绝不完整或模糊的需求

### 2.3 输出审查

- §14 Final Pre-Flight Check 强制代码审查
- 检查 WCAG AA 对比度合规
- 验证组件结构完整性

---

## 3. 代码生成安全

### 3.1 禁止的代码模式

Taste Skill 明确禁止以下不安全的代码模式：

| 禁止模式 | 风险等级 | 说明 |
|----------|----------|------|
| `window.addEventListener('scroll')` | 高 | 性能问题，可能导致内存泄漏 |
| 自定义滚动计算 | 高 | 破坏原生滚动行为 |
| `requestAnimationFrame` 循环 | 中 | 可能导致性能瓶颈 |
| React `useState` 用于连续动画 | 高 | 状态更新频繁，性能下降 |
| 内联 SVG 图标 | 低 | 可维护性差，建议使用图标库 |

### 3.2 安全的动画实现

```javascript
// ✅ 安全：使用 Motion（原 Framer Motion）
import { motion } from 'motion/react';

// ✅ 安全：使用 GSAP 进行滚动动画
gsap.to(element, {
  scrollTrigger: {
    trigger: element,
    start: "top top",
    pin: true,
    scrub: true
  }
});

// ❌ 不安全：直接操作 DOM
window.addEventListener('scroll', () => {
  element.style.transform = `translateY(${scrollY}px)`;
});
```

### 3.3 性能安全护栏

- **DOM 成本控制：** grain/noise 滤镜仅应用于 fixed, pointer-event-none 的伪元素
- **硬件加速：** 仅使用 `transform` 和 `opacity` 进行动画
- **Z-Index 约束：** 避免 z-index 冲突

---

## 4. AI Agent 交互安全

### 4.1 防止 AI 生成不完整输出

`output-skill`（`full-output-enforcement`）专门解决此问题：

- 禁止占位符注释：`// ...`、`// rest of code`、`// TODO`
- 强制完整代码输出
- 在干净断点暂停时显示进度：`[PAUSED — X of Y complete]`

### 4.2 防止模板化输出

§9 "AI Tells" 禁令防止 AI 生成可识别的模板化内容：

- 禁止 em-dash（—）使用
- 禁止装饰性状态点
- 禁止滚动提示文本
- 禁止版本标签在 Hero 区域

### 4.3 需求推断验证

§0 Brief Inference 确保 AI 正确理解需求：

- 识别页面类型（落地页、作品集、重新设计等）
- 提取设计关键词
- 确定目标受众
- 声明设计约束

---

## 5. 依赖管理安全

### 5.1 推荐依赖

| 类别 | 推荐 | 不推荐 |
|------|------|--------|
| CSS 框架 | Tailwind CSS v4 | - |
| 动画库 | Motion、GSAP | 原生 CSS 动画 |
| 图标库 | Phosphor、HugeIcons、Radix、Tabler | Lucide、手写 SVG |
| 字体 | Geist 等高端字体 | 系统字体 |

### 5.2 依赖审查清单

- [ ] 验证包名拼写正确
- [ ] 检查包的维护状态
- [ ] 评估包的大小影响
- [ ] 确认许可证兼容性

### 5.3 设计系统映射

§2 Brief → Design System Map 确保使用官方设计系统：

- Material Design → `@mui/material`
- Fluent UI → `@fluentui/react`
- Carbon → `@carbon/react`
- Polaris → `@shopify/polaris`
- Atlassian → `@atlaskit/button`
- Primer → `@primer/react`
- GOV.UK → `govuk-frontend`
- USWDS → `@uswds/uswds`
- Bootstrap → `bootstrap`
- Radix → `@radix-ui/react-*`
- shadcn → `@shadcn/ui`

---

## 6. 部署安全

### 6.1 技能文件分发

- 通过 `npx skills add` CLI 工具安装
- 技能文件为纯 Markdown 格式
- 无二进制依赖

### 6.2 本地安装

```bash
# 安全的安装方式
npx skills add https://github.com/Leonxlnx/taste-skill

# 安装特定技能
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

### 6.3 手动安装

- 直接复制 SKILL.md 文件到项目
- 无需执行脚本
- 用户可完全审查内容

---

## 7. 安全检查清单

### 7.1 开发阶段

- [ ] 使用 §14 Final Pre-Flight Check
- [ ] 验证 WCAG AA 对比度
- [ ] 检查组件结构完整性
- [ ] 确认动画性能安全

### 7.2 部署阶段

- [ ] 审查生成的代码
- [ ] 验证依赖安全性
- [ ] 检查敏感信息泄露
- [ ] 测试跨浏览器兼容性

### 7.3 运行时

- [ ] 监控性能指标
- [ ] 检查内存使用
- [ ] 验证错误处理

---

## 8. 已知安全考虑

### 8.1 AI 生成代码的局限性

- AI 可能生成看似正确但存在安全隐患的代码
- 需要人工审查生成的代码
- 建议在生产环境前进行安全测试

### 8.2 依赖风险

- 第三方依赖可能存在漏洞
- 建议定期更新依赖
- 使用 `npm audit` 检查已知漏洞

### 8.3 性能安全

- 动画可能影响可访问性
- 需要提供 `prefers-reduced-motion` 支持
- 高 `MOTION_INTENSITY` 值需要额外审查

---

## 9. 安全最佳实践

### 9.1 代码审查

1. 使用 §14 Final Pre-Flight Check
2. 验证所有交互状态
3. 检查错误处理
4. 测试边界情况

### 9.2 依赖管理

1. 定期更新依赖
2. 使用 `npm audit` 检查漏洞
3. 锁定依赖版本
4. 验证包完整性

### 9.3 性能优化

1. 使用硬件加速动画
2. 避免布局抖动
3. 实现懒加载
4. 监控关键指标

---

## 10. 事件响应

### 10.1 安全问题报告

如发现安全问题，请通过以下方式报告：

- GitHub Issues: https://github.com/Leonxlnx/taste-skill/issues
- 邮件: hello@tasteskill.dev

### 10.2 响应时间

- 高危漏洞: 24小时内响应
- 中危漏洞: 72小时内响应
- 低危漏洞: 1周内响应

---

## 附录

### A. 安全相关技能

| 技能名称 | 安装名称 | 安全功能 |
|----------|----------|----------|
| output-skill | `full-output-enforcement` | 防止 AI 生成不完整输出 |
| taste-skill | `design-taste-frontend` | §9 AI Tells 禁令、§14 预检清单 |

### B. 安全文档引用

- [WCAG 2.1 对比度指南](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [MDN Web 安全最佳实践](https://developer.mozilla.org/en-US/docs/Web/Security)
- [npm 安全文档](https://docs.npmjs.com/about-security)

---

**文档结束**
