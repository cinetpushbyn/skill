# output-format.md — 标准输出格式

这个 Skill 的输出是一个 JSON 对象，包含 6 个字段。

---

## 完整格式

```json
{
  "poster_direction": "string",
  "title": "string",
  "subtitle": "string（可选）",
  "visual_keywords": ["string", "string", "..."],
  "selling_points": ["string", "string", "..."],
  "layout_hint": "string"
}
```

---

## 字段说明

| 字段 | 类型 | 长度建议 | 是否必填 |
|------|------|----------|----------|
| `poster_direction` | string | 15 字以内 | 必填 |
| `title` | string | 8~14 字 | 必填 |
| `subtitle` | string | 16~24 字 | 可选 |
| `visual_keywords` | array | 3~6 个词，每词 1~3 字 | 必填 |
| `selling_points` | array | 2~4 个词，每词 4~8 字 | 必填 |
| `layout_hint` | string | 20~35 字 | 必填 |

---

## 示例一：日期主题输入（谷雨）

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

---

## 示例二：图片参考输入（高端极简春日风）

```json
{
  "poster_direction": "参考高端极简风格的春日茶仓产品海报",
  "title": "春藏一柜，静养好茶",
  "subtitle": "以东方留白呈现茶仓与春日空间的平衡感",
  "visual_keywords": ["极简", "木质", "浅金", "米白", "春日光感"],
  "selling_points": ["恒温恒湿", "静音存储", "隔光养护"],
  "layout_hint": "单品居中，标题靠右竖向排布，底部保留简洁功能信息"
}
```

---

## 示例三：灵感主题输入（东方茶仓美学）

```json
{
  "poster_direction": "东方茶仓美学主题产品海报",
  "title": "以时藏茶，以度护香",
  "subtitle": "在东方空间美学里，好茶值得一个恰当的居所",
  "visual_keywords": ["禅意", "原木", "茶汤色", "留白", "光影"],
  "selling_points": ["智能控湿", "隔光防氧", "静音运行"],
  "layout_hint": "产品侧置偏左，标题居右竖排，整体色调偏暖，留白多"
}
```

---

## 格式注意事项

- 输出 JSON，不要加多余解释
- 如果 `subtitle` 不合适可以不填，但字段保留，值设为 `null` 或 `""`
- `visual_keywords` 和 `selling_points` 都是数组，不要写成一整个字符串
- 不在 JSON 外面写额外的长段落分析
