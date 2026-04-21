---
name: poster-brief-builder
description: 海报方案展开器。把上一个 poster-theme-trigger 给出的基础主题起点，扩展成一个简洁、可落地的产品海报 brief。触发条件：用户已有主题想展开成海报方案、上传参考图想整理成海报方向、从多个灵感中选一个展开。不负责生成完整生图 prompt，不负责最终审核，不负责直接出成品图。
---

# poster-brief-builder

这个 Skill 是一个**海报方案展开器**。

它只做一件事：把主题起点变成简洁、可落地的海报 brief，方便下游继续处理。

它不写完整生图 prompt，不做最终审核，不直接生成成品图。

---

## 触发条件

用以下任意一种方式触发：

- 用户已有主题，想继续展开：「根据这个主题出个海报方案」「把这个方向扩成海报内容」「按这个继续」
- 用户上传参考图，想整理成可执行方向：「按这个样式给我一版海报方案」「参考这张图给我一个海报思路」
- 用户从灵感中选一个展开：「选'东方茶仓美学'这个展开」「把其中一个做成完整方向」「给我一个可落地的方案」

不触发条件见 → [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)

---

## 输入来源类型

| 类型 | 标识 | 来源说明 |
|------|------|----------|
| 日期主题 | `date_theme` | 来自 poster-theme-trigger 的节气/节日/普通日判断结果 |
| 图片参考 | `image_reference` | 来自 poster-theme-trigger 对上传图片的风格摘要 |
| 灵感建议 | `inspiration_theme` | 来自 poster-theme-trigger 给出的多个灵感主题之一 |

---

## 执行步骤

### 第 1 步：读取输入，明确核心方向

先判断输入类型（`date_theme` / `image_reference` / `inspiration_theme`），然后确定：

- 这张海报主打什么主题
- 偏节气、偏品牌、偏场景，还是偏卖点
- 产品在画面中是什么角色

**只出一个方向，不发散，不 brainstorming。**

### 第 2 步：生成简洁海报 brief

固定输出以下 6 个字段：

```
poster_direction  // 本次海报方向，一句话
title             // 主标题
subtitle          // 副标题（可选，要克制）
visual_keywords   // 3~6 个视觉关键词
selling_points    // 2~4 个卖点短词
layout_hint       // 一句版式建议
```

字段细则 → [references/brief-structure.md](references/brief-structure.md)  
标题规则 → [references/title-rules.md](references/title-rules.md)  
卖点规则 → [references/selling-point-rules.md](references/selling-point-rules.md)

### 第 3 步：检查边界，不越界

输出前自查：

- [ ] 没有写完整生图 prompt
- [ ] 没有写 negative prompt 或模型参数
- [ ] 没有写成长篇文案
- [ ] 没有给出多套完全不同版本
- [ ] 没有堆空词

越界行为清单 → [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)

---

## 标准输出格式

```json
{
  "poster_direction": "谷雨节气下的东方茶仓产品海报",
  "title": "雨润百谷，茶藏有度",
  "subtitle": "让好茶在恰好的温湿之间静静陈放",
  "visual_keywords": ["晨雾", "新芽", "润泽", "米白", "留白"],
  "selling_points": ["智能控温湿", "隔潮防霉", "隔光抗氧", "天然等离子"],
  "layout_hint": "产品居中，标题靠右，底部一排卖点图标，整体留白干净"
}
```

完整格式说明 → [references/output-format.md](references/output-format.md)  
Good/Bad Case → [references/examples.md](references/examples.md)

---

## 这个 Skill 不做什么

- 不写完整生图 prompt
- 不写 negative prompt 或模型参数
- 不做最终审美审核
- 不写长篇品牌故事
- 不一次给多套完全不同版本
- 不直接生成成品图

完整禁忌 → [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)
