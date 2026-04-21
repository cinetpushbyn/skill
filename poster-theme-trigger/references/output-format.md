# 输出格式规范

## 总原则

- 输出结构化 JSON
- JSON 后可附一两句说明，解释判断依据，不要超过两句
- 不堆砌废话，不用空泛形容词
- 输出是"基础起点信息"，不是最终方案

---

## date 类型

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `trigger_type` | string | 固定值 `"date"` |
| `is_special_day` | boolean | 今天是否为节气或节日 |
| `day_type` | string | `"solar_term"` / `"festival"` / `"ordinary"` |
| `theme` | string | 主题名（节气名、节日名，或"普通日"） |
| `theme_ideas` | array | 仅普通日时附带，3～5 个创意方向，每条 2～8 个字 |

### 示例：节气日

```json
{
  "trigger_type": "date",
  "is_special_day": true,
  "day_type": "solar_term",
  "theme": "谷雨"
}
```

说明（可选，不超过两句）：今天是谷雨，二十四节气之一。可作为茶叶、养生、春耕类产品海报的主题起点。

### 示例：节日

```json
{
  "trigger_type": "date",
  "is_special_day": true,
  "day_type": "festival",
  "theme": "端午节"
}
```

### 示例：普通日（附创意方向）

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

说明（可选）：今天为普通日，已附 5 个通用创意方向，可按产品类型从中选取。

---

## image_reference 类型

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `trigger_type` | string | 固定值 `"image_reference"` |
| `reference_summary.style` | string | 整体风格，1～5 个字为宜 |
| `reference_summary.theme` | string | 主题感，1～8 个字为宜 |
| `reference_summary.composition` | string | 构图方式，用短语描述 |
| `reference_summary.tone` | string | 色调，列举 2～4 个颜色或质感词 |

### 示例

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

说明（可选）：图片呈现东方极简风格，以留白和竖排文字为主要视觉语言。

---

## inspiration 类型

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `trigger_type` | string | 固定值 `"inspiration"` |
| `theme_ideas` | array | 3～5 个简洁主题方向，每条 2～8 个字 |

### 示例

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

## 通用格式禁止事项

- 不在 JSON 里写完整海报标题
- 不在 JSON 里写卖点文案
- 不在 `theme_ideas` 里写完整广告语
- `style` / `theme` 字段不要超过 10 个字
- 说明文字不超过两句，不用"高级感拉满""氛围感十足"这类空话
