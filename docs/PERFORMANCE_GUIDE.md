# 性能优化指南

> 文档版本：v1.0  
> 更新日期：2026年6月15日  
> 维护人：AI Assistant

---

## 1. 概述

Taste Skill 提供了一套完整的性能优化指南，确保生成的前端代码具有优秀的性能表现。本文档涵盖：

- 动画性能优化
- 渲染性能优化
- 加载性能优化
- 运行时性能优化

---

## 2. 动画性能优化

### 2.1 硬件加速原则

**核心规则：** 仅使用 `transform` 和 `opacity` 进行动画

```css
/* ✅ 安全：硬件加速 */
.element {
  transform: translateY(100px);
  opacity: 0.5;
}

/* ❌ 不安全：触发重排 */
.element {
  top: 100px;
  left: 50px;
  width: 200px;
  height: 100px;
}
```

### 2.2 动画库选择

| 库 | 适用场景 | 性能等级 |
|----|----------|----------|
| GSAP | 滚动动画、固定堆叠、水平平移 | ⭐⭐⭐⭐⭐ |
| Motion (Framer Motion) | React 组件动画 | ⭐⭐⭐⭐ |
| CSS Transitions | 简单状态变化 | ⭐⭐⭐⭐ |
| CSS Animations | 循环动画 | ⭐⭐⭐ |

### 2.3 GSAP 最佳实践

#### 滚动固定堆叠 (§5.A)

```javascript
// ✅ 正确：GSAP Sticky-Stack
gsap.to(".card", {
  scrollTrigger: {
    trigger: ".container",
    start: "top top",
    pin: true,
    scrub: true,
    // 使用 NEXT 卡片的触发器驱动变换
  }
});
```

#### 水平平移 (§5.B)

```javascript
// ✅ 正确：GSAP Horizontal-Pan
gsap.to(".track", {
  scrollTrigger: {
    trigger: ".container",
    start: "top top",
    pin: true,
    end: "+=" + distance,
    scrub: 1
  }
});
```

#### 滚动显示动画 (§5.C)

```javascript
// ✅ 正确：Scroll-Reveal Stagger
import { motion } from 'motion/react';

<motion.div
  initial={{ opacity: 0, y: 50 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true }}
  transition={{ duration: 0.6 }}
>
  {/* 内容 */}
</motion.div>
```

### 2.4 禁止的动画模式

```javascript
// ❌ 禁止：自定义滚动监听
window.addEventListener('scroll', () => {
  // 性能问题
});

// ❌ 禁止：React state 中的滚动计算
const [scrollY, setScrollY] = useState(0);
useEffect(() => {
  window.addEventListener('scroll', () => {
    setScrollY(window.scrollY); // 频繁状态更新
  });
}, []);

// ❌ 禁止：requestAnimationFrame 循环
useEffect(() => {
  let animationId;
  const animate = () => {
    // 操作 DOM
    animationId = requestAnimationFrame(animate);
  };
  animate();
  return () => cancelAnimationFrame(animationId);
}, []);
```

---

## 3. 渲染性能优化

### 3.1 DOM 成本控制

**规则：** grain/noise 滤镜仅应用于 fixed, pointer-event-none 的伪元素

```css
/* ✅ 安全：固定伪元素 */
.grain::before {
  content: '';
  position: fixed;
  inset: 0;
  z-index: 50;
  pointer-events: none;
  /* 应用滤镜 */
}

/* ❌ 不安全：滚动容器 */
.scrolling-container::before {
  /* 会导致持续 GPU 重绘 */
}
```

### 3.2 Z-Index 管理

```css
/* 推荐的 Z-Index 层级 */
:root {
  --z-base: 0;
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-overlay: 300;
  --z-modal: 400;
  --z-toast: 500;
  --z-grain: 9999;
}
```

### 3.3 布局抖动预防

```css
/* ✅ 安全：预留空间 */
.image-placeholder {
  aspect-ratio: 16/9;
  background: var(--color-gray-100);
}

/* ❌ 不安全：布局抖动 */
.image {
  /* 加载前无尺寸 */
}
```

---

## 4. 加载性能优化

### 4.1 字体加载

```css
/* ✅ 安全：字体显示策略 */
@font-face {
  font-family: 'Geist';
  src: url('/fonts/Geist-Regular.woff2') format('woff2');
  font-display: swap; /* 防止 FOIT */
}
```

### 4.2 图片优化

```html
<!-- ✅ 安全：响应式图片 -->
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img 
    src="image.jpg" 
    alt="描述"
    loading="lazy"
    decoding="async"
  >
</picture>
```

### 4.3 代码分割

```javascript
// ✅ 安全：动态导入
const HeavyComponent = lazy(() => import('./HeavyComponent'));

// ✅ 安全：路由级代码分割
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));
```

---

## 5. 运行时性能优化

### 5.1 减少重绘重排

```javascript
// ✅ 安全：批量 DOM 操作
const fragment = document.createDocumentFragment();
items.forEach(item => {
  const element = document.createElement('div');
  fragment.appendChild(element);
});
container.appendChild(fragment);

// ❌ 不安全：逐个插入
items.forEach(item => {
  const element = document.createElement('div');
  container.appendChild(element); // 每次触发重排
});
```

### 5.2 事件委托

```javascript
// ✅ 安全：事件委托
document.querySelector('.list').addEventListener('click', (e) => {
  if (e.target.closest('.item')) {
    // 处理点击
  }
});

// ❌ 不安全：为每个项目绑定事件
document.querySelectorAll('.item').forEach(item => {
  item.addEventListener('click', () => {
    // 内存占用高
  });
});
```

### 5.3 节流和防抖

```javascript
// ✅ 安全：防抖
function debounce(fn, delay) {
  let timeoutId;
  return (...args) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn(...args), delay);
  };
}

// ✅ 安全：节流
function throttle(fn, limit) {
  let inThrottle;
  return (...args) => {
    if (!inThrottle) {
      fn(...args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

---

## 6. 可访问性性能

### 6.1 减少动画偏好

```css
/* ✅ 安全：尊重用户偏好 */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### 6.2 React 中的实现

```javascript
import { useReducedMotion } from 'motion/react';

function AnimatedComponent() {
  const shouldReduceMotion = useReducedMotion();
  
  return (
    <motion.div
      animate={shouldReduceMotion ? {} : { opacity: 1, y: 0 }}
      transition={{ duration: 0.6 }}
    >
      {/* 内容 */}
    </motion.div>
  );
}
```

---

## 7. 性能监控

### 7.1 关键指标

| 指标 | 目标值 | 说明 |
|------|--------|------|
| FCP | < 1.5s | 首次内容绘制 |
| LCP | < 2.5s | 最大内容绘制 |
| FID | < 100ms | 首次输入延迟 |
| CLS | < 0.1 | 累积布局偏移 |
| TTI | < 3.5s | 可交互时间 |

### 7.2 监控工具

```javascript
// 性能观察器
const observer = new PerformanceObserver((list) => {
  list.getEntries().forEach((entry) => {
    console.log(entry.name, entry.startTime);
  });
});

observer.observe({ entryTypes: ['paint', 'largest-contentful-paint'] });
```

### 7.3 性能预算

```json
{
  "budgets": [
    {
      "type": "initial",
      "maximumWarning": "200kb",
      "maximumError": "300kb"
    },
    {
      "type": "bundle",
      "name": "main",
      "maximumWarning": "100kb",
      "maximumError": "150kb"
    }
  ]
}
```

---

## 8. 性能检查清单

### 8.1 开发阶段

- [ ] 使用硬件加速动画（transform/opacity）
- [ ] 实现减少动画偏好支持
- [ ] 优化图片加载（lazy loading）
- [ ] 实现代码分割
- [ ] 避免布局抖动

### 8.2 测试阶段

- [ ] 运行 Lighthouse 性能测试
- [ ] 检查 CLS 分数
- [ ] 验证 FCP 和 LCP
- [ ] 测试移动端性能
- [ ] 检查内存使用

### 8.3 部署阶段

- [ ] 启用 Gzip/Brotli 压缩
- [ ] 配置 CDN
- [ ] 设置缓存策略
- [ ] 监控性能指标

---

## 9. 性能问题排查

### 9.1 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 动画卡顿 | 使用非硬件加速属性 | 改用 transform/opacity |
| 布局偏移 | 图片无尺寸 | 设置 aspect-ratio |
| 内存泄漏 | 未清理事件监听 | 使用 cleanup 函数 |
| 加载慢 | 未代码分割 | 使用 dynamic import |

### 9.2 调试工具

- Chrome DevTools Performance 面板
- Lighthouse 性能报告
- React DevTools Profiler
- Web Vitals 扩展

---

## 10. 总结

### 10.1 核心原则

1. **硬件加速：** 仅使用 transform 和 opacity
2. **减少重排：** 批量 DOM 操作
3. **懒加载：** 图片和代码分割
4. **可访问性：** 尊重用户动画偏好

### 10.2 性能优化优先级

1. **高优先级：** 动画性能、图片优化
2. **中优先级：** 代码分割、字体优化
3. **低优先级：** 高级优化技巧

### 10.3 建议行动

1. 立即：审查现有动画实现
2. 本周：实施图片懒加载
3. 本月：建立性能监控

---

## 附录

### A. 性能相关技能

| 技能名称 | 安装名称 | 性能功能 |
|----------|----------|----------|
| taste-skill | `design-taste-frontend` | §5 动画规范、性能护栏 |
| soft-skill | `high-end-visual-design` | 性能优化建议 |

### B. 相关文档

- [安全架构](./SECURITY_ARCHITECTURE.md)
- [存储占用分析](./STORAGE_ANALYSIS.md)
- [代码资产盘点](../CODE_ASSETS_INVENTORY.md)

### C. 参考资源

- [Web.dev 性能指南](https://web.dev/performance/)
- [MDN 性能文档](https://developer.mozilla.org/en-US/docs/Web/Performance)
- [GSAP 性能优化](https://greensock.com/docs/GSAP/gsap.matchMedia())

---

**文档结束**
