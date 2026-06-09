---
name: tea-cigar-wine-daily
description: Generate a Chinese tea-cigar-wine knowledge encyclopedia daily: concise, factual, reusable micro-encyclopedia entries about tea, cigars, collectible wines and spirits, storage, etiquette, craftsmanship, tasting vocabulary, regions, history, utensils, provenance, and common misconceptions. Use when asked for 茶茄酒日报, 烟酒茶日报, 茶酒茄知识, 知识小百科, daily educational content, sales-team learning cards, or encyclopedia-style content about cigars, tea, wine, spirits, cellars, humidors, tea cabinets, private collecting, and refined hospitality.
---

# Tea Cigar Wine Knowledge Daily

## Purpose

Generate a Chinese "knowledge mini-encyclopedia" for tea, cigars, and collectible wines or spirits. The output should help a sales team steadily build domain literacy and accumulate reusable knowledge cards.

Default task: produce one encyclopedia-style card for each category in this order:

1. 雪茄
2. 收藏型酒类 / 烈酒
3. 茶叶

If the user asks for one category or a specific topic, follow that scope.

Use [daily-report-template.md](references/daily-report-template.md) as the output structure.

## Audience And Voice

Write for a brand sales team serving high-end collecting and hospitality customers. The tone should be:

- Clear, factual, and memorable
- Refined but not ornamental
- Useful for learning, training, and later conversation
- Encyclopedic, not promotional
- Concrete enough that a salesperson can explain it in plain language

Prefer "把一件事讲明白" over "把一段话写漂亮".

## Content Direction

Each card should explain one compact knowledge point, not a broad lifestyle theme. Strong topics include:

- Core definitions: 茄衣 / 茄套 / 茄芯, 单一麦芽, 年份香槟, 岩茶焙火, 普洱仓储
- Craft and process: 发酵, 醇化, 转瓶, 加强酒, 蒸馏, 拼配, 杀青, 萎凋, 炭焙
- Regions and classification: 哈瓦那, 尼加拉瓜, 波尔多, 杜罗河谷, 香槟, 武夷山, 勐海
- Storage and care: 雪茄湿度, 酒窖温度, 茶叶避光防潮, 异味隔离, provenance
- Etiquette and use: 雪茄裁切点火, 醒酒, 侍酒温度, 茶席器具, 待客场景
- Common misconceptions: 年份越老越好, 所有茶都适合长期存, 雪茄越湿越好, 烈酒不用管理
- Vocabulary: body, finish, tannin, wrapper, terroir, 仓味, 山场, 回甘, 陈年潜力

Avoid making every card return to the same storage conclusion. Storage can be included when relevant, but each card must have its own knowledge center.

## Encyclopedia Card Rules

Each card must answer a real learner's question. Good card titles look like:

- "什么是雪茄的茄衣？"
- "为什么香槟会有年份与非年份之分？"
- "岩茶里的'焙火'到底在改变什么？"

Each card should include:

- A short concrete opening scene of 1-2 sentences, using an object, gesture, place, or sensory detail to pull the reader in
- A one-sentence definition
- 3-5 key points that unpack the concept
- One practical observation for collection, service, tasting, or customer explanation
- One common misconception or boundary
- Optional related terms for future cards

Keep each category around 600-900 Chinese characters unless the user asks otherwise. It should feel like a readable encyclopedia note, not a bullet outline.

## Anti-Repetition Protocol

Before drafting, load these references:

- [topic-ledger.md](references/topic-ledger.md): recent used topics and banned near-duplicates.
- [topic-rotation.md](references/topic-rotation.md): topic axes and rotation rules.

Apply this protocol every time:

1. Pick a topic ID for each category, such as `cigar-wrapper-connecticut`, `wine-champagne-vintage-nv`, or `tea-wuyi-roast`.
2. Reject any topic whose same ID appears in the recent ledger.
3. Reject near-duplicates in the last 30 days: same person, same named book, same region + same concept, same storage number, same origin anecdote, or same misconception.
4. Do not use the same knowledge axis in two consecutive daily outputs for the same category. Axes include definition, craft, region, classification, service, storage, etiquette, tasting vocabulary, history, and misconception.
5. If forced to revisit a broad theme, change the angle materially. Example: "香槟转瓶" and "年份香槟" are different; "陆羽《茶经》煮茶" and "陆羽《茶经》存茶" are too close.
6. At the end of the output, include a small hidden maintenance note only if the user asks to maintain the ledger; otherwise do not show it.

After generating a recurring daily output, update `topic-ledger.md` with date, category, topic ID, title, axis, and blocked near-duplicates when file editing is available. Keep the ledger concise.

## Fact Rules

- Verify names, dates, origin claims, production facts, classification systems, storage numbers, and quotes before using them.
- Prefer official appellation bodies, producer education pages, museums, institutions, textbooks, academic references, and reliable encyclopedic sources.
- If a detail cannot be verified, omit it or phrase it cautiously.
- Do not invent historical anecdotes, celebrity habits, poems, vintage claims, provenance, brands, or rankings.
- Use short quotations only when necessary, and identify the source or author.

## Anti-Slop Rules

Do not write soft lifestyle filler. Avoid repeated phrases such as:

- "不只是...而是..."
- "真正讲究"
- "高端生活方式"
- "东方雅致"
- "美学"
- "秩序"
- "价值"
- "安静等待"
- "时间留下的痕迹"
- "收藏已经开始"

Avoid these failure modes:

- Three different stories all ending in 恒温恒湿 / 避光 / 防潮
- Calendar labels with no date-specific relevance
- Overuse of 陆羽, 丘吉尔, 雪松木盒, 1855分级
- Pretty but unverifiable "scene writing"
- Sales slogans disguised as knowledge
- Excessive emoji, poster language, or WeChat formatting

## Category Scope

Tea topics may include tea history, tea taxonomy, famous tea regions, tea processing, tea utensils, brewing, tasting vocabulary, storage by tea type, Tea Horse Road, tea poetry, puer, white tea, rock tea, green tea, black tea, oolong, yellow tea, dark tea, and tea hospitality.

Cigar topics may include origin, growing regions, wrapper / binder / filler, fermentation, aging, vitolas, humidity, cutting, lighting, pairing, cigar cabinets, cigar rooms, cigar etiquette, factory terms, ring gauges, box codes, provenance, and responsible appreciation.

Wine and spirits topics may include wine, champagne, port, sherry, whisky, cognac, armagnac, rum, baijiu, huangjiu, sake, old bottles, limited releases, vintages, provenance, cellaring, decanting, serving temperature, light protection, humidity, cork, oxidation, distillation, cask aging, and classification systems.

## Output Rules

- Default output title: "茶茄酒知识小百科｜YYYY年M月D日".
- Output three complete cards in order: 雪茄, 收藏型酒类 / 烈酒, 茶叶.
- Use a fresh topic ID and fresh knowledge axis for each card according to the Anti-Repetition Protocol.
- Do not include poster titles, "今日切入", long story hooks, or forced WeChat Moments copy unless the user explicitly asks.
- Do not include product selling sections by default.
- Use simple Markdown headings, short paragraphs, and compact bullets. Avoid making the card look like a bare outline.
- Use 3-5 tasteful emoji per full daily output, mainly in section headings or small visual cues. Use category-relevant emoji such as 🚬, 🍷, 🥃, 🍵, 🌿, 🧭, 🪵, 🫖. Do not use emoji after every sentence.
- End with "明日可延展词条" listing 3-6 future encyclopedia topics.

## Optional Sales Use

If the user asks for sales enablement, add a short "销售转述" line under each card:

- Keep it factual and conversational.
- Do not hard-sell.
- Explain what kind of customer this knowledge helps with.

## Compliance Boundaries

- Do not claim health benefits for tea, alcohol, or cigars.
- Do not encourage smoking, drinking, overconsumption, or underage use.
- For cigars and alcohol, focus on culture, collection, storage, etiquette, craftsmanship, provenance, and responsible appreciation.
- Avoid medical, therapeutic, investment-return, or guaranteed appreciation claims.
