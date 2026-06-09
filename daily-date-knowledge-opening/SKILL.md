---
name: daily-date-knowledge-opening
description: Generate a polished Chinese daily date-and-knowledge opening with a readable book quote, calendar facts, solar terms, international days, and a real historical story for the date. Use when asked for a daily opening, knowledge daily, morning digest opening, date note, festival / solar-term note, book quote, or historical date note.
---

# Daily Date And Knowledge Opening

## Purpose

Generate a concise Chinese daily opening with two clean modules:

1. Date header and book quote
2. Today calendar facts and historical story

The report should feel like it was prepared by an information and knowledge curation editor: readable, orderly, lightly literary, and useful.

Use the exact report structure in [daily-report-template.md](references/daily-report-template.md). Load it before drafting the final report.

## Daily Workflow

1. Determine today's date and weekday in the user's timezone.
2. Read [quote-history.md](references/quote-history.md) if it exists.
3. Build the opening quote:
   - Choose a quote or paraphrased idea from a book, novel, essay, classic, or major literary work.
   - The quote must be easy to understand in everyday Chinese.
   - It must have a clear source: book title, author, and translator / chapter when available.
   - It must not repeat recent daily quotes if prior reports are available.
   - If the quote is from a modern copyrighted work, keep it short or paraphrase the idea.
   - After drafting the final report, append or recommend appending the used quote to quote history when operating in a writable environment.
4. Verify today's calendar:
   - Chinese lunar date
   - 24 solar terms
   - Chinese traditional festivals
   - International or world days
   - notable historical events that happened on this date
5. Select one historical-cultural node for "今天是什么日子":
   - Prefer a real event that happened on today's date.
   - Write it as a short story: person, event, scene, and why it still matters.
   - Avoid abstract phrases such as "适合谈记录、保存、记忆".
   - If no strong event is available, state a modest "今日可参考节点" and do not embellish.
6. Write in Chinese with a warm, intelligent, orderly tone.
7. Use clean Markdown and tasteful emoji.
8. Include source links or concise source notes when the environment supports citations.

## Quote Rules

- The "今日一句话" quote is mandatory.
- Use books, novels, essays, classical works, famous literary works, or public-domain classics.
- Prefer clear, conversational, easy-to-understand lines. Do not choose obscure philosophical sentences just because they sound elegant.
- Use only short quotes.
- Do not quote more than 25 words from any one non-lyrical source.
- For modern copyrighted books, prefer paraphrase plus source note instead of direct quotation.
- Public-domain classical Chinese poetry or prose may be used, but keep it brief and relevant.
- If unsure whether a quotation is real, omit it or write "可延展阅读" instead.
- Always provide source attribution in this pattern: 《书名》 / 作者；translator, chapter, or essay title when useful.
- If prior daily reports are available, check recent "今日一句话" and avoid repeated quotes, repeated books, and repeated authors within 7 days when possible.
- If no prior reports are available, choose a quote with broad readability and note no repetition history was supplied.

## Formatting Rules

- Use clean Markdown.
- Keep section headings exactly as the template defines them, including emoji.
- Use divider lines (`---`) exactly where the template places them.
- Use tasteful emoji sparingly and naturally.
- Keep paragraphs short.
- Only output the two template modules.
- The report should look tidy in Codex, Feishu, and WeChat drafting contexts.
