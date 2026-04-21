# poster-theme-trigger

**定位：** 海报主题入口触发 Skill。只负责识别触发来源，返回基础主题起点信息。不生成完整海报、不写文案、不出图。

---

## 触发时机

当用户请求符合以下任一情况时触发本 Skill：

1. 用户希望系统自动判断今天是否为节气或节日，并据此给出当天海报主题起点
2. 用户上传图片，并表达想要类似样式、风格、主题、构图的产品海报
3. 用户直接索要主题灵感、主题建议、创意方向

**不触发情况：** 用户只是让你看图评价、让你写完整海报方案、让你设计完整工作流。详见 [references/trigger-rules.md](references/trigger-rules.md)。

---

## 执行步骤

### Step 1：识别触发类型

判断本次请求属于哪一类：

| 类型 | 标识 | 判断依据 |
|------|------|----------|
| 日期触发 | `date` | 提到今天、节气、节日、自动判断日期 |
| 图片参考触发 | `image_reference` | 上传图片 + 表达想要类似风格/主题 |
| 灵感建议触发 | `inspiration` | 索要创意、主题建议、灵感方向 |

详细判断规则见 [references/trigger-rules.md](references/trigger-rules.md)。

---

### Step 2：按类型返回基础结果

#### 如果是 `date`

根据今天的实际日期判断：
- 是否为二十四节气
- 是否为常见节日（春节、中秋、端午等）
- 还是普通日

返回字段：`is_special_day` / `day_type` / `theme`

**节气或节日时：** 返回主题名，输出结束。

```json
{
  "trigger_type": "date",
  "is_special_day": true,
  "day_type": "solar_term",
  "theme": "谷雨"
}
```

**普通日时：** 不返回空结果，直接附带 3～5 个创意方向，供用户直接使用。

```json
{
  "trigger_type": "date",
  "is_special_day": false,
  "day_type": "ordinary",
  "theme": "普通日",
  "theme_ideas": [
    "日常精选好物",
    "品质生活提案",
    "一杯好茶的理由",
    "静物美学日常",
    "家居茶空间"
  ]
}
```

---

#### 如果是 `image_reference`

提取图片里的基础参考信息：

- `style`：整体风格（如"高端极简""国风水墨"）
- `theme`：主题感（如"春日东方茶仓"）
- `composition`：构图方式（如"单品居中，右侧标题"）
- `tone`：色调（如"米白、浅金、留白"）

只做"参考摘要"，不写生图 prompt。

```json
{
  "trigger_type": "image_reference",
  "reference_summary": {
    "style": "高端极简产品海报",
    "theme": "春日东方茶仓",
    "composition": "单品居中，右侧竖排标题，底部卖点图标",
    "tone": "米白、浅金、干净、留白"
  }
}
```

---

#### 如果是 `inspiration`

输出 3～5 个简洁主题方向，作为后续 Skill 的输入起点。不写完整标题、副标题、卖点文案。

```json
{
  "trigger_type": "inspiration",
  "theme_ideas": [
    "春茶焕新",
    "雨润万物",
    "东方茶仓美学",
    "静养陈化",
    "高端家居茶空间"
  ]
}
```

---

### Step 3：输出轻量、清晰、可供下游处理

本 Skill 输出的是"基础起点信息"，不是最终方案。

**本 Skill 不做的事：**
- 不写完整海报标题和副标题
- 不写卖点文案
- 不生成完整生图 prompt
- 不做图片审核
- 不做复杂主题优先级评分
- 不冒充后续策划 Skill

详细边界和禁忌见 [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)。

---

## 输出格式

结构化 JSON + 必要的一两句说明。保持简洁，不堆砌废话。详见 [references/output-format.md](references/output-format.md)。

---

## 案例参考

Good Case 和 Bad Case 见 [references/examples.md](references/examples.md)。

---

## 文档排版规则

见 [references/layout-style.md](references/layout-style.md)。
