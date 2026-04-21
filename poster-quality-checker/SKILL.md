# poster-quality-checker

## 这是什么

海报质量检查器。

承接已经生成好的 brief、prompt 或成图，快速判断有没有关键问题，决定能不能继续用、要改哪里。

**它是检查器，不是生成器。** 只做发现问题、指出问题、给修改建议这三件事。

---

## 触发条件

用户说出以下类型的话时触发本 Skill：

- "帮我检查一下这版行不行"
- "看看这张海报有没有问题"
- "审核一下这版海报"
- "这版 prompt 会不会太乱"
- "发之前帮我过一遍"
- "这版哪里要改"
- "值不值得继续用这版"
- "有没有哪里不对"

**不触发的情况（直接边界）：**

- 用户要求重新生成主题 → 交给 poster-theme-trigger
- 用户要求重写完整 brief → 交给 poster-brief-builder
- 用户要求重写完整 prompt → 交给 poster-prompt-builder
- 用户要灵感、要头脑风暴 → 不属于检查场景

---

## 执行步骤

### Step 1：识别检查对象

先判断用户给的是哪类输入：

| 类型 | 说明 |
|------|------|
| `brief_check` | 用户有海报方向、标题、副标题、卖点、版式建议 |
| `prompt_check` | 用户有 image_prompt 或 negative_prompt |
| `image_check` | 用户上传了成图，或者描述了生成结果 |

**只按这一类的规则检查，不要混着评。**

详细检查规则 → [references/check-rules.md](references/check-rules.md)

---

### Step 2：找关键问题，不做长篇大论

只抓最影响结果的问题，最多 3～5 个。

优先检查什么 → [references/issue-priority.md](references/issue-priority.md)

---

### Step 3：输出结构化结果

固定输出以下字段：

```json
{
  "status": "pass 或 revise",
  "score": 0-100,
  "main_issues": ["问题1", "问题2", "问题3"],
  "suggestions": ["建议1", "建议2", "建议3"],
  "summary": "一句总判断"
}
```

怎么写建议 → [references/suggestion-rules.md](references/suggestion-rules.md)

完整格式说明 → [references/output-format.md](references/output-format.md)

---

## Good Case / Bad Case

详见 [references/examples.md](references/examples.md)

---

## 禁忌行为与禁忌词

详见 [references/boundaries-and-forbidden.md](references/boundaries-and-forbidden.md)

---

## 文档排版规则

详见 [references/layout-style.md](references/layout-style.md)
