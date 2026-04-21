# poster-prompt-builder

## 这个 Skill 是什么

把已有的海报 brief，整理成可以直接交给生图模型使用的 prompt。

它是一个**转换器**，不是主题触发器，不是海报策划器，也不是审核器。

---

## 触发条件

在以下情况下触发：

- 用户已经有一版海报 brief，想继续往下走，比如"根据这个方案生成生图提示词""把这版方案转成 prompt""给我最终生图文案"
- 用户已经确定标题、视觉方向、卖点和版式，想要一段适合生图模型的完整描述
- 用户希望把参考风格、主题方向和产品信息整理成"一段能直接拿去生图的提示词"

**不触发的情况：**

- 用户在问主题灵感（交给 poster-theme-trigger）
- 用户在做完整海报策划（交给 poster-brief-builder）
- 用户在评估最终出图效果（不属于本 Skill 范围）

---

## 处理的 3 类输入

### 输入 1：标准海报 brief

用户已经有完整 brief，包括海报方向、主标题、副标题、视觉关键词、卖点、版式建议。

→ 直接整合成 `image_prompt` + `negative_prompt`，不需要补全。

### 输入 2：图片参考 + brief 混合

用户给了参考图的风格描述，同时有当前产品 brief。

→ 融合参考风格和产品 brief，生成新 prompt。不能照抄参考图描述，不能直接复制参考图风格词。

### 输入 3：简略方案

用户只给了主题、产品、大概方向，内容不完整。

→ 做适度补全，但补全只能围绕"生图表达"展开，不能重新做完整策划。

---

## 执行步骤

### 第 1 步：读取 brief，提炼画面核心信息

从输入中识别以下关键信息：

- 产品主体是什么
- 海报主题是什么
- 画面风格是什么
- 色调是什么
- 构图是什么
- 标题文案是否需要在 prompt 中体现
- 卖点是否以信息块形式出现在画面中

目标：把 brief 里"散的内容"整理成生图模型容易理解的一组画面信息。

### 第 2 步：生成主 prompt

固定输出两个字段：

- `image_prompt`：包含产品主体、画面场景、视觉风格、光线氛围、构图建议、品牌感、海报感、排版意图
- `negative_prompt`：覆盖常见风险项，比如杂乱背景、产品变形、文字乱码、廉价感等

详细结构规则见 → [references/prompt-structure.md](references/prompt-structure.md)

negative prompt 规则见 → [references/negative-prompt-rules.md](references/negative-prompt-rules.md)

### 第 3 步：输出可直接使用的结果

输出格式参考 → [references/output-format.md](references/output-format.md)

结果要能直接交给生图模型，不需要用户再做二次整理。

---

## brief 字段如何映射成 prompt

详细映射规则见 → [references/brief-to-prompt-rules.md](references/brief-to-prompt-rules.md)

---

## 禁忌行为 / 禁忌词

详细清单见 → [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)

---

## Good Case / Bad Case

见 → [references/examples.md](references/examples.md)

---

## 输出版式规则

见 → [references/layout-style.md](references/layout-style.md)
