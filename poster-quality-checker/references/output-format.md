# 输出格式

---

## 标准 JSON 结构

```json
{
  "status": "pass 或 revise",
  "score": 0-100,
  "main_issues": [
    "问题描述，一句话"
  ],
  "suggestions": [
    "修改建议，一句话，可执行"
  ],
  "summary": "一句总判断"
}
```

---

## 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| status | string | `pass` = 可以用；`revise` = 需要修改 |
| score | number | 0-100，整数，参考 issue-priority.md 中的打分说明 |
| main_issues | array | 关键问题，1～5 条，每条一句话，不超过 30 字 |
| suggestions | array | 修改建议，条数和 main_issues 对应 |
| summary | string | 总判断，一句话，不超过 40 字 |

---

## brief 检查示例

```json
{
  "status": "revise",
  "score": 78,
  "main_issues": [
    "标题偏长，视觉记忆点不够集中",
    "背景元素略多，削弱了产品主体",
    "底部卖点信息稍多，画面有点拥挤"
  ],
  "suggestions": [
    "把标题压缩到 8 个字以内",
    "减少背景装饰，提升产品主体存在感",
    "底部卖点保留 3 个核心点，删掉重复项"
  ],
  "summary": "方向基本对，但需要先收缩再发布。"
}
```

---

## prompt 检查示例

```json
{
  "status": "revise",
  "score": 74,
  "main_issues": [
    "背景描述过多，产品主体不够突出",
    "风格词堆叠偏杂，容易导致生成结果不稳定",
    "negative prompt 缺少文字乱码和产品变形约束"
  ],
  "suggestions": [
    "把产品主体描述放到 prompt 最靠前的位置",
    "风格词只保留 3 个核心方向，删掉重复和矛盾的",
    "negative prompt 补上：text, watermark, deformed product, distorted"
  ],
  "summary": "可以继续用，但需要先收敛风格并加强主体控制。"
}
```

---

## 图片检查示例

```json
{
  "status": "pass",
  "score": 88,
  "main_issues": [
    "背景右侧有轻微杂乱感",
    "底部文字区域预留空间略紧"
  ],
  "suggestions": [
    "裁切或模糊右侧背景边缘",
    "底部留白多 10% 给文字区域"
  ],
  "summary": "整体可以用，做两个小调整后直接发。"
}
```

---

## 输出语言

- 默认用中文输出
- 字段名保持英文（status, score, main_issues, suggestions, summary）
- 内容简洁直接，不要在 JSON 之外加大段解释

---

## 什么情况下 status = pass

- 没有 P0 问题
- P1 问题不超过 1 个
- 整体 score ≥ 85

其他情况一律输出 `revise`。
