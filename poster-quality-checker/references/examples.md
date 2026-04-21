# 示例集

---

## Good Case

### Good Case 1：brief 检查

**用户说：** "这版标题和卖点你帮我检查一下，有没有明显问题。"

**处理方式：** 识别为 `brief_check`，检查标题长度、卖点数量、有没有重复，输出结构化结果。

**示例输出：**

```json
{
  "status": "revise",
  "score": 76,
  "main_issues": [
    "主标题有 14 个字，太长，视觉上很难一眼记住",
    "卖点 3 和卖点 5 意思重复，都是说保温效果",
    "副标题没有具体信息，只有情绪描述"
  ],
  "suggestions": [
    "主标题压缩到 8 个字以内，突出核心卖点",
    "删掉卖点 5，合并进卖点 3",
    "副标题改成一个具体数字或具体场景描述"
  ],
  "summary": "方向没问题，但标题和卖点需要先收缩再用。"
}
```

---

### Good Case 2：prompt 检查

**用户说：** "这个 prompt 会不会太乱，帮我过一遍。"

**处理方式：** 识别为 `prompt_check`，检查主体位置、风格词数量、negative prompt 完整性，输出结构化结果。

**示例输出：**

```json
{
  "status": "revise",
  "score": 71,
  "main_issues": [
    "产品主体出现在 prompt 中间位置，容易被背景压过",
    "风格词有 8 个，且部分互相矛盾（minimalist 和 rich texture）",
    "negative prompt 没有限制文字乱码和产品变形"
  ],
  "suggestions": [
    "把产品主体描述移到 prompt 最开头",
    "风格词只保留 3 个方向，删掉矛盾的",
    "negative prompt 加上：text, watermark, deformed product, blurry"
  ],
  "summary": "主体控制和风格都需要收敛，修改后再出图。"
}
```

---

### Good Case 3：图片检查

**用户说：** "这版海报能不能发？帮我看一下。"（附成图）

**处理方式：** 识别为 `image_check`，从产品主体、构图、背景、品牌感等角度判断，输出结构化结果。

**示例输出：**

```json
{
  "status": "pass",
  "score": 87,
  "main_issues": [
    "背景左上角有轻微杂乱感，分散注意力"
  ],
  "suggestions": [
    "裁切或虚化左上角背景区域"
  ],
  "summary": "整体可以发，左上角处理一下更稳。"
}
```

---

## Bad Case

### Bad Case 1：要求重新生成主题

**用户说：** "帮我直接重新生成一个谷雨主题。"

**错误做法：** 直接生成主题

**正确做法：** 说明"这属于主题生成，不是质量检查，建议用 poster-theme-trigger 来做。"

---

### Bad Case 2：要灵感

**用户说：** "给我 10 个主题灵感。"

**错误做法：** 触发本 Skill 并生成灵感列表

**正确做法：** 不触发本 Skill，这不是质量检查场景。

---

### Bad Case 3：要求整版重做

**用户说：** "直接帮我重写完整 prompt 和海报方案。"

**错误做法：** 直接重写

**正确做法：** 说明"重写 prompt 和 brief 超出质量检查范围，需要用 poster-brief-builder 和 poster-prompt-builder 来做。如果你有现有版本想先检查，可以把它发给我。"

---

### Bad Case 4：空话输出

**错误输出示例：**

```json
{
  "status": "pass",
  "main_issues": ["整体氛围很好，挺高级的"],
  "suggestions": ["可以再优化一下细节"],
  "summary": "感觉不错，基本可以用。"
}
```

**问题：** main_issues 没有指出具体问题，suggestions 没有可执行建议，summary 是空话。

**这种输出不允许出现。**
