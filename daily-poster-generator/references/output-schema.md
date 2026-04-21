# output-schema.md — 返回结构与文件保存规则

> 本文件定义正常模式返回结构、调试模式完整结构、质检规则、文件保存规则。

---

## 一、正常模式返回结构

### 1.1 节日/节气海报（每张）

```
[图片]
主题名：<节点名称>
主标题：<2-4字>
副标题：<6-10字>
```

示例：
```
[图片]
主题名：谷雨
主标题：谷雨
副标题：一柜锁住春茶香
```

### 1.2 日常品牌海报

```
[图片]
主题名：日常品牌
主标题：<2-4字品牌感短句>
副标题：<6-10字>
```

示例：
```
[图片]
主题名：日常品牌
主标题：时光醒茶
副标题：守护每一克珍藏
```

### 1.3 低质量候选图返回格式

```
[图片]
⚠️ 低质量候选图（未保存）
主题名：<节点名称>
主标题：<主标题>
副标题：<副标题>
质检原因：<具体描述，例：产品主体占比过小 / 产品疑似被遮挡>
```

---

## 二、调试模式完整返回结构

调试模式每张图返回以下完整结构化信息：

```json
{
  "debug_output": {
    "trigger_mode": "auto | manual | debug_auto | debug_manual",
    "date_beijing": "2026-04-20",
    "input_topic": null,
    "corrected_topic": null,

    "node_detection": {
      "detected_nodes": [
        {
          "name": "谷雨",
          "type": "A",
          "score": 93,
          "score_breakdown": {
            "base": 80,
            "tea_relevance": 10,
            "visual_atmosphere": 3
          }
        },
        {
          "name": "春茶季",
          "type": "D",
          "score": 65,
          "score_breakdown": {
            "base": 50,
            "tea_relevance": 10,
            "multi_node_bonus": 5
          }
        }
      ],
      "selected_nodes": ["谷雨"],
      "fallback_to_daily": false
    },

    "plan": {
      "node_name": "谷雨",
      "headline": "谷雨",
      "subheadline": "一柜锁住春茶香",
      "features": ["智能控温湿"],
      "visual_summary": "细雨纹理背景，青石板地台，嫩芽点缀，柔和漫射光，产品居中",
      "scene_type": "semi-outdoor",
      "lighting": "soft diffused daylight, misty green tone",
      "composition": "center symmetry"
    },

    "prompts": {
      "positive": "<完整正向提示词>",
      "negative": "<完整反向提示词>"
    },

    "assets": {
      "reference_image": "assets/products/meijing-v1-white-bg.png",
      "reference_image_role": "product base image for img2img"
    },

    "api_execution": {
      "model": "stable-diffusion-xl | midjourney-api | <配置中指定的模型>",
      "endpoint": "<config 中配置的 endpoint，不暴露 key>",
      "params": {
        "width": 1080,
        "height": 1920,
        "steps": 30,
        "cfg_scale": 7.5,
        "denoising_strength": 0.75
      },
      "status": "success | failed",
      "error": null
    },

    "quality_check": {
      "passed": true,
      "checks": {
        "product_size_ok": true,
        "product_not_occluded": true,
        "product_position_ok": true
      },
      "flags": []
    },

    "output": {
      "saved": true,
      "file_path": "output/2026/04/2026-04-20_谷雨_自动_01.png",
      "prompt_file": "output/2026/04/2026-04-20_谷雨_自动_01.txt",
      "quality_label": "normal | low_quality_candidate"
    }
  }
}
```

---

## 三、基础质检规则

### 3.1 质检触发时机

- 每张图生成完成后立即执行
- 质检失败**不阻断返回**，但影响保存行为

### 3.2 质检项（第一版，仅基础判断）

| 质检项 | 检查方式 | 判定标准 |
|--------|----------|----------|
| 产品主体占比 | 图像分析（预计算或视觉 API） | 产品占画面面积 ≥ 25%（估算） |
| 产品是否被遮挡 | 视觉判断或前景检测 | 产品主要轮廓清晰可见 |
| 产品位置是否离谱 | 重心/位置检测 | 产品主体不在画面边缘 10% 以内 |

> 第一版质检为基础判断，不做精细语义审核（如光影准确性、文字内容等）。

### 3.3 质检结果处理

| 质检结果 | 处理行为 |
|----------|----------|
| 通过（all checks pass） | 正常返回 + 正常保存 + 生成 txt |
| 未通过（any check fail） | 返回图片 + 标记「低质量候选图」+ **不保存** + **不生成 txt** |

---

## 四、文件保存规则

### 4.1 目录结构

```
output/
└── 2026/
    └── 04/
        ├── 2026-04-20_谷雨_自动_01.png
        ├── 2026-04-20_谷雨_自动_01.txt
        ├── 2026-04-20_谷雨_自动_02.png   ← 如有第2张
        ├── 2026-04-20_谷雨_自动_02.txt
        ├── 2026-04-21_清明_手动_01.png
        ├── 2026-04-21_清明_手动_01.txt
        ├── 2026-04-21_清明_手动_02.png
        ├── 2026-04-21_清明_手动_03.png
        └── 2026-04-21_日常品牌_自动_01.png
```

### 4.2 文件命名规则

```
<日期>_<主题>_<模式>_<序号>.png / .txt
```

| 字段 | 格式 | 示例 |
|------|------|------|
| 日期 | YYYY-MM-DD | 2026-04-20 |
| 主题 | 节点名称中文，日常海报用「日常品牌」 | 谷雨 / 中秋 / 日常品牌 |
| 模式 | 自动 / 手动 | 自动 / 手动 |
| 序号 | 两位数字，从 01 开始 | 01 / 02 / 03 |

### 4.3 txt 文件内容格式

```
POSITIVE PROMPT:
<完整正向提示词>

NEGATIVE PROMPT:
<完整反向提示词>
```

- txt 文件**只保存提示词**，不保存其他元数据
- 调试信息不写入 txt 文件

### 4.4 保存与不保存判断

| 条件 | 保存 PNG | 保存 TXT |
|------|----------|----------|
| 质检通过 | ✅ 保存到 output/年/月/ | ✅ 保存同名 txt |
| 质检未通过（低质量候选图） | ❌ 不保存 | ❌ 不保存 |
| API 调用失败（无图） | ❌ 无图可保存 | ❌ 不保存 |

---

## 五、错误返回结构

```
[ERROR] <错误类型>: <错误描述>

错误类型对照：
- INPUT_ERROR     : 输入参数不合法（主题词非节日/节气类等）
- DATE_ERROR      : 日期读取失败
- NODE_ERROR      : 节点识别逻辑异常
- API_ERROR       : 生图 API 调用失败
- SAVE_ERROR      : 文件保存失败（不影响返回图片）
```

示例：
```
[ERROR] API_ERROR: 生图 API 调用失败 — HTTP 503 Service Unavailable
执行已终止。请检查 API 配置后重试。
```

```
[ERROR] INPUT_ERROR: 主题词不合法 — 「智能控温」不是节日或节气类主题词
合法主题词示例：谷雨、清明、中秋、春节、端午、冬至、母亲节
请重新输入，或使用「生成今日海报」触发自动模式。
```
