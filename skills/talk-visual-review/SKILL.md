---
name: talk-visual-review
version: 1.0.0
description: "演讲页/幻灯片的视觉验收——用浏览器实测每一屏是否被切、是否过空、对比度够不够、色板有没有绕过主题变量，而不是靠肉眼翻页目测。触发词：讲稿排版检查、幻灯片验收、内容溢出、投影看不全、slide 被切、演讲页视觉检查、talk 排版、每页会不会超屏、PPT 排版验收。与 talk-text-review（查姿态/文本）互补：那个管说什么，这个管看得见看不见。"
metadata:
  requires:
    bins: ["node"]
    npm: ["playwright"]
---

# 演讲页视觉验收：量出来，不是看出来

## 为什么不能靠肉眼

翻 19 屏靠眼睛看，三个必漏：

1. **屏幕不一样**：你在 2560×1440 的 Mac 上看着刚好，投影是 1280×800，内容当场被切。
2. **缩放会骗人**：talk 页常有 `--talk-scale` 之类的等比缩放，本机缩小了看着没事，投影放大就溢出。
3. **量太大**：20 屏 × 4 种分辨率 = 80 次目测，人一定会跳着看，而出事的往往是没看的那几屏。

2026-08-28 实测翻过一次车：一屏塞了表格 + 引用 + 两段正文，标题被切掉一半、底部内容跑到屏幕外，翻页也够不着——肉眼在开发机上完全看不出来。

**核心原则：分屏用估算，验收用实测，两者必须独立。** 用同一个估算模型既分屏又验收，等于自己给自己打分。

## 主检查：内容是否被切

facet 项目直接跑现成脚本：

```bash
node scripts/check-slide-overflow.mjs dist-share/<slug>/talk.html
node scripts/check-slide-overflow.mjs https://share.webkubor.online/<slug>/talk --size 1920x1080
```

非 facet 项目，核心测量逻辑（在任意 CDP 浏览器里 evaluate 即可）：

```js
() => {
  const slides = [...document.querySelectorAll('.slide')];   // 换成目标页的屏选择器
  const saved = slides.map(s => s.className);
  const vh = window.innerHeight;
  const rows = [];
  slides.forEach((s, i) => {
    slides.forEach(x => x.classList.remove('active'));       // 逐个临时激活
    s.classList.add('active');
    const body = s.querySelector('.slide-body') || s;        // 量真正的内容容器
    const r = body.getBoundingClientRect();
    rows.push({
      i: i + 1,
      fill: Math.round(body.scrollHeight / vh * 100),
      cutTop: r.top < -1,
      cutBottom: r.bottom > vh + 1
    });
  });
  slides.forEach((x, i) => x.className = saved[i]);
  return rows;
}
```

两个坑：

- **必须逐个临时激活**。靠 `.active` 控制显示的页，不激活的屏 `getBoundingClientRect` 全是 0，量出来一片正常。
- **量内容容器，不量 wrapper**。flex 布局的外层会被拉伸到视口高度，`scrollHeight` 对所有屏返回同一个数——看到一列一模一样的高度就说明量错了元素。

## 判据

| 填充率 | 判定 | 处理 |
|---|---|---|
| 越界（top<0 或 bottom>vh） | 🔴 **被切** | 必修。讲的时候内容在屏幕外，翻页够不着 |
| > 90% | 🟡 危险 | 换个分辨率就可能切，建议拆 |
| 35% – 90% | ✅ 正常 | |
| < 35% | 🟡 偏空 | 不影响可读，但翻页显碎；连续多屏偏空要调分屏阈值 |

**至少测两个分辨率**：`1280x800`（投影常见）和 `1920x1080`。只测一个等于没测。

## 附带检查（有 CDP 浏览器时顺手做）

```js
// 1. 硬编码色值：绕过主题变量的地方，换主题时会不跟着变
[...document.querySelectorAll('style')].map(s => s.textContent)
  .join('').match(/#[0-9a-f]{3,8}(?![^{]*\})/gi)

// 2. 正文对比度：投影环境比显示器暗，对比度不足后排看不清
getComputedStyle(document.querySelector('.slide-body p')).color

// 3. 代码块字号：正文与代码字号差距过大是投影上最常见的「看不清」来源
getComputedStyle(document.querySelector('.slide pre')).fontSize
```

经验阈值：投影场景正文 ≥ 18px、代码 ≥ 16px，正文与代码字号差 ≤ 4px。对比度按 WCAG AA（正文 4.5:1），投影建议做到 7:1。

## 机器测不了的，交给人

这套只回答「**看不看得见**」，回答不了「**讲不讲得顺**」。以下必须人自己翻一遍：

- 断句是否自然（拆屏可能把一个论证从中间劈开）
- 每屏的信息重心对不对（一屏该有一个主张，不是一堆并列）
- 表格/代码在这一屏出现的时机对不对
- 续屏标记是否让人误以为翻重复了

**报告时明确分开说**：哪些是实测结论（有数字），哪些需要人确认。别把「我测了没被切」说成「排版没问题」。

## 边界

- 只验渲染结果，不改内容、不调分屏策略（那是构建器的事）
- 不替代真机彩排：投影的色温、亮度、可视角度测不出来
- 报告里给出实测数字（几屏、填充率、什么分辨率），不写「看起来还行」
