# daily-poster-generator

每日产品海报自动生成 Skill — RACHING 美晶茶叶柜

---

## 快速上手

### 1. 复制配置文件

```bash
cp config.example.json config.json
```

编辑 `config.json`，填入：
- `image_generation.api_key` — 生图模型 API Key
- `image_generation.endpoint` — 生图模型接口地址
- `llm.api_key` — Claude API Key（用于提示词生成）

### 2. 放置产品白底图

```
assets/products/meijing-v1-white-bg.png
```

### 3. 触发 Skill

在 Claude Code 中直接输入：

```
生成今日海报
生成节日海报 谷雨
调试今日海报
调试节日海报 中秋
```

---

## 文件结构

```
daily-poster-generator/
├── SKILL.md                   ← Skill 核心定义（触发词、流程、GoodCase/BadCase）
├── config.example.json        ← 配置样例（不含真实 key）
├── config.json                ← 真实配置（勿提交 git）
├── references/
│   ├── rules.md               ← 场景约束、黑名单、品牌规范、版式规则
│   ├── nodes.md               ← 节气/节日清单、评分规则、D类营销节点
│   ├── prompts.md             ← 提示词生成策略、反向提示词模板
│   └── output-schema.md       ← 返回结构、质检规则、文件保存规则
├── impl/
│   └── poster_generator.py   ← 执行逻辑存根（含完整类结构与伪代码注释）
├── assets/
│   └── products/
│       └── meijing-v1-white-bg.png   ← 产品白底图（需手动放置）
└── output/                    ← 自动创建，按年/月分目录
    └── 2026/
        └── 04/
            ├── 2026-04-20_谷雨_自动_01.png
            └── 2026-04-20_谷雨_自动_01.txt
```

---

## 触发词速查

| 触发词 | 模式 | 输出数量 |
|--------|------|----------|
| `生成今日海报` | 自动 | 最多 2 张（无节点命中则 1 张日常） |
| `生成节日海报 <主题>` | 手动 | 固定 3 张差异版 |
| `生成节日海报`（无主题） | 自动回退 | 同自动模式 |
| `调试今日海报` | 自动+调试 | 同自动模式，返回完整结构化信息 |
| `调试节日海报 <主题>` | 手动+调试 | 同手动模式，返回完整结构化信息 |

---

## 实现进度（第一版待完成项）

- [ ] 节气内置日期表（2025-2027）
- [ ] 农历转换实现（B 类传统节日）
- [ ] 商业节日公历匹配
- [ ] D 类营销节点区间匹配
- [ ] 主题词智能纠错（别名表 + 模糊匹配）
- [ ] LLM 调用（自由变量提示词生成）
- [ ] 生图 API 接入（SD/SDXL img2img）
- [ ] 基础质检（产品占比/位置检测）
- [ ] 文件保存与 txt 输出

---

## 注意事项

- `config.json` 含真实 API Key，**不要提交到 git**，已加入 `.gitignore` 建议
- 低质量候选图只返回给用户，**不写入 output/ 目录**
- 生图 API 失败直接报错，**第一版不自动重试**
- 所有日期判断统一使用北京时间（UTC+8）
