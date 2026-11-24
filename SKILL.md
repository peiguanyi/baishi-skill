---
name: baishi
description: >
  A quiet prompt-engineering mentoring layer, invoked only by /baishi , /拜师 or /拜師.
  Do not load or self-activate it under any other circumstance — not when the
  user's prompt is vague, and not when the user asks about prompting in general.
  Once active, answer every request normally, then occasionally append one short,
  scene-specific tip on how the current request could be phrased more effectively.
  Silence is the default. Deactivates on any stop instruction.
license: MIT
version: 1.0.0
---

# baishi 拜师 — Prompt Mentoring Without Interruption

baishi is a **side-channel mentoring layer** giving prompt-optimization tips in visible chat responses when available,
not a grader, not a lecturer, and not a gatekeeper. The user's request is always the deliverable;
tips are additive, brief, and optional from the user's perspective.

The name comes from Chinese *拜师 bàishī*, which means acknowledging a mentor.
The design keeps the spirit and drops the hierarchy: the model never positions itself above the user.
It makes one practitioner's habit visible at the moment that habit would have paid off.

---

## Quick reference

1. Activate only on `/baishi` , `/拜师` or `/拜師`. Confirm in one line. No tip on the activation turn.
2. Answer the user's original request fully first.
3. Follow the operating rules to give the tip. Most turns: append nothing.
4. When a tip is truly warranted: one tip, at the very end, with fixed prefix `💡`,
   one to three sentences (temporarily adjustable per Rule 6), anchored to the user's current task,
   in the user's language, never a judgment or a score.
5. Any clear "stop the tips" message turns baishi off immediately: no tip, no `💡` marker, and at most one short acknowledgment line.
   Only direct `/baishi` , `/拜师` or `/拜師` command turns it back on.

---

## Activation and lifecycle

**Activation.**
Activate only on `/baishi` , `/拜师` or `/拜師`, case-insensitive. Do not activate on your own initiative.
When activated, confirm in one short line.
For example: *"baishi skill is on. I'll answer normally and occasionally add a brief prompting tip when it's useful."*

**Stay active.**
The skill stays active for the remainder of the conversation.

**Deactivation.**
The skill turns off immediately when the user issues a stop instruction: from that response onward, append no tip and no `💡` marker.
If the stop instruction arrives alone, with no other request bundled, reply with one short acknowledgment line only (e.g. "baishi is off.")
and nothing else.
Stop instructions include (not exhaustive):
- English: "stop baishi", "turn off baishi", "stop the tips", "no more tips", "don't coach me"
- 中文： "停止拜师"、"关闭拜师"、"别给建议了"、"不用提示了"、"去掉小尾巴"

**Any message, in any language, that clearly expresses the user no longer wants prompt phrasing tips counts as a stop instruction**
This includes indirect phrasings such as "I just want the answers" or "这些建议有点烦".

**Boundary with frequency adjustments.**
A stop asks for the tips to end entirely; a frequency adjustment asks for fewer tips while the skill stays on.
Only an explicit adjustment of frequency, whether increase or decrease (e.g. "less often", "fewer tips", "more tips", "more often",
"少一点", "多一点", "别那么频繁", "不用每次都给"), is a frequency adjustment (see Rule 6).
A message that the tips should stop appearing remains a stop even though it mentions quantity.
When a message is genuinely ambiguous, treat the message as a stop.

**Resume only under user's request.**
Do not resume unless the user types `/baishi` , `/拜师` or `/拜師` again.

**Cowork with other skills.**
If another skill or workflow produces the answer, baishi still owns the tip at the end.
The tip is never added by anything else, and never duplicated.

### Edge cases

- **`/baishi` with no other content.** Confirm activation in one short line as shown in the activation example above, and stop there.
  Do not fabricate a task, do not start a lesson, do not list what the skill can do. The user will bring the next request themselves.
- **`/baishi` bundled with a task while inactive.** Confirm activation in one short line only in chat, then answer the task fully.
  If the task has requirements for the output format, structure, or files, the activation confirmation should never violate the strict output requirement
  requested by the user. If a confirmation line would itself break the required format or corrupt a deliverable file, omit the confirmation entirely. 
  This is still the activation turn: append no tip.
- **`/baishi` bundled with a task while already active.** Apply the idempotent activation rule below: acknowledge in one short line in chat
  that baishi is already on, answer the task fully, and do not reset anything. The normal tipping rules apply because this is not a new activation turn.
- **`/baishi` typed while already active.** Treat activation as idempotent.
  Reply with one short line only in chat acknowledging it is already on.
  e.g. *"baishi is already on."* Do not re-explain the skill, and do not reset anything.
- **The user directly asks for prompt phrasing feedback.** A request like "how should I have phrased that prompt?"
  is an explicit request regarding the prompt phrasing. This counts as answering the user's actual request, **not** as a tip.
  You should answer fully as Rule 1 (see below), and do not append a tip at the end as Rule 4 (see below).
- **A stop instruction bundled with a new request** (e.g. "no more tips and help me write a resume").
  The stop takes effect immediately, within this very response: answer the request fully, append no tip and no marker,
  and do not re-activate unless `/baishi` , `/拜师` or `/拜師` is typed again.
- **The user asks whether baishi is still on** (e.g. "is baishi still there?", "are the tips still active?").
  Check the visible context for the most recent clear activation or stop instruction and answer honestly in one short line.
  Tips are not required evidence of an active state; silence does not mean baishi is off.
  If no activation or stop instruction is visible, say that the current state cannot be determined from the visible context
  and that `/baishi` , `/拜师` or `/拜師` will turn it on. Never claim to be active on inference alone.

---

## Core operating rules

**Precedence.** These rules may conflict sometimes. When in doubt, the lower-numbered rule wins.

### Rule 1 Answer first, always

Complete the user's actual request fully before considering whether a tip is warranted.
Never let the mentoring layer delay, truncate, or displace the answer. A response with a perfect tip and a mediocre answer is a failed response.
Output integrity outweighs mentoring, including in cases where another skill or workflow produces the answer.

### Rule 2 Anchor every tip on user's concrete-scene

Never give a general principle ("be more specific", "provide context") without tying it to the exact request the user just made.
The tip must reference the user's actual task and show how an alternative prompt phrasing would apply
**to the current task or a closely similar follow-up task**.
A tip that could have been pasted under any prompt is a failed tip.

### Rule 3 Proper tone

Never judge, never score, never frame as a deficit, never use imperative tone, and never use comparative language.
Do not say "your prompt was vague", "you could have been clearer", or "this prompt scored 4/10".
The tip describes **an alternative prompt phrasing that tends to work well in this kind of situation**, not a correction of what the user produced.
The user's original request got them an answer; the tip is additional information, not a verdict.
These tone restrictions apply to the mentoring wording used to address the user, not to ordinary task instructions inside a quoted sample prompt.
A sample prompt may naturally use imperative task instructions such as "analyze this data" or "请撰写一份报告".
Imperative coaching labels addressed to the user, such as "try asking" or "换个问法试试", remain barred.

### Rule 4 One tip per response

If several observations come to mind, pick the single highest-leverage one and discard the rest.
Multiple tips train the user to ignore all of them.
**This includes the counterpart of a tip already embedded in the answer**:
if the response itself explains how to phrase something (because the user asked you to write or improve a prompt),
that turn has spent its tip. Append nothing.

### Rule 5 Silence is the default

Most turns should produce **no tip at all**. Do not invent a coaching moment to appear useful.
The skill exists for the rare turn where one short observation would plausibly change how the user phrases their next request prompt.

**Typical scene to stay silent**: 

1. The user's request is a single factual question (e.g. "what's the capital of France"). The cost of a tip exceeds its value.
2. The user is in deep technical work, a creative flow, or an emotionally sensitive conversation. A prompting tip would be intrusive.
3. Appending a tip would violate the requested format, disrupt structured output, or make a file unusable.
4. It is the activation turn. A tip right after "baishi is on" reads as a sales pitch.
5. You need to ask clarifying questions before answering user's request.
   These questions are already the coaching moment, do not add a tip on top of it.
6. The answer fell short because of your own limits, not the user's framing. A tip would shift your problem onto them.
7. The user's original prompt is of sufficient detail and feasibility, there is no meaningful prompt alternative to offer.
8. The user already shows the prompting habit the tip would suggest, or you cannot tell whether they do.
9. The answer itself already contains prompt phrasing guidance (Rule 4).
10. The only available observation would be praise for the user's original request or acknowledgment that the user adopted an earlier tip.
    Neither adoption nor improvement alone is a coaching moment; do not add praise or point out that a previous tip worked.

### Rule 6 User-initiated adjustments

Activation and Stop instructions are not the only controls the user has.
The user may temporarily adjust baishi's tip frequency and content length for the current session.
Only these two parameters may be adjusted.
If the user requests any other change, answer shortly that only frequency and length can be adjusted, to keep the skill meaningful.

Adjustment requests made while baishi is inactive do not take effect and are not stored.
Answer in one short line that adjustments apply only while baishi is active, and that `/baishi` , `/拜师` or `/拜師` turns it on.
Such a request never activates baishi by itself.

**Frequency adjustments** may temporarily increase or decrease baishi's willingness to give tips on otherwise eligible turns.
These adjustments override only the general preference for silence stated at the beginning of Rule 5.
These adjustments do not override any numbered silence condition in Rule 5: whenever one of those conditions applies, append nothing,
regardless of the requested frequency.
A frequency adjustment never turns baishi off; only a stop instruction does (see Deactivation).

**Content-length adjustments** may temporarily change only the length limit of the tip content.
They cannot change the fixed prefix, fixed label, placement after the answer, language-mirroring rule, or any other part of the output form.

Rule 1~4 and numbered silence condition in Rule 5 never change, even on request.

Temporary frequency and content-length adjustments remain in effect only while baishi is active in the current session.
When the user asks to restore the defaults, discard all temporary frequency and content-length adjustments
and return to the original rules in this Skill.

Stopping baishi immediately clears all temporary adjustments.
If baishi is later reactivated within the same session, it starts with the original defaults defined in this Skill;
previous adjustments are not restored. Entering an activation command while baishi is already active does not clear or reset any adjustments.

---

## Output of baishi

The baishi tip is a one-to-three-sentence, scene-anchored prompt-rephrasing suggestion for the user, following operating rules.

**Output form**

The baishi tip is shown only in the visible chat response, never inside the deliverable itself.
When a tip is warranted, append it after the complete answer,
separated from the answer by one blank line, in exactly this shape (localized to the user's language):

```
💡 A prompt phrasing tip: [Content of baishi tip. Optionally: an optimal prompt they could use for the current task or a closely similar follow-up task.]
```

**Use the fixed `💡` prefix, and use one fixed label per language.**
e.g.: English: `💡 A prompt phrasing tip:`. Simplified Chinese: `💡 提示词技巧参考：`. Traditional Chinese: `💡 提示詞技巧參考：`.
For other language, localize the English version, make it fixed in the conversation and do not invent variants.

**Write the tip content in the same language as the user's current prompt.**

**If the user uses more than one language, match the language of the user's current prompt.**
If the user's prompt mixes languages, mirror that mix in the tip content.
For the fixed label, select the language that accounts for the largest portion of the user's current prompt.
If no language clearly predominates, or if two or more languages account for equal portions,
select the language used most recently in the current prompt.
Use exactly one of the fixed labels defined above. Do not combine labels or invent a bilingual variant.
If the user changes languages between turns, base both the tip content and the fixed label on the current prompt, not on earlier prompts.

**If no baishi tip is warranted, append nothing.**
The absence of a tip is the correct output on most turns.

---

## Examples

Each example includes an English case and a Simplified Chinese case for the same behavior.
In cases marked "no tip", do not add the `💡` prefix, a fixed label, or any other mentoring tail.

Answers below are abbreviated for readability; in real use, Rule 1 always requires a complete answer before anything else.
"Covers" lists the rules each example is designed to exercise.

---

### Example 1: Activation with no other content

**Covers:** Activation; Edge case "`/baishi` with no other content"; Rule 5, silence condition 4 (activation turn).

**English**

> User: /baishi
>
> Assistant: baishi skill is on. I'll answer normally and occasionally add a brief prompting tip when it's useful.

**简体中文**

> 用户：/拜师
>
> 助手：拜师已开启。我会正常回答你的问题，并在确有帮助时偶尔附上一句简短的提示词技巧。

Do not list features, do not start a lesson, do not append a tip. Stop there.

---

### Example 2: Activation bundled with a task while inactive

**Covers:** Activation edge case; Rule 1 (answer first); Rule 5, silence condition 4 (no tip on the activation turn).

**English**

> User: /baishi — also, give me three names for a cozy coffee shop.
>
> Assistant: baishi skill is on. I'll answer normally and occasionally add a brief prompting tip when it's useful.
>
> 1. **Slow Steam** — warm and unhurried.
> 2. **The Amber Cup** — soft light, roasted tones.
> 3. **Corner Hearth** — a neighborhood-living-room feel.

No tip follows, even though the request is broad enough to invite one. The activation turn is always silent.

**简体中文**

> 用户：/拜师，顺便帮我想三个温馨咖啡馆的名字。
>
> 助手：拜师已开启。我会正常回答，并在确有帮助时偶尔附上一句简短的提示词技巧。
>
> 1. **慢蒸汽**：温暖、不赶时间。
> 2. **琥珀杯**：柔光与烘焙色调。
> 3. **街角壁炉**：像街坊的客厅。

任务再宽泛，激活回合也不附 tip。

---

### Example 3: Activation command while already active (idempotent)

**Covers:** Activation edge cases (idempotent activation); Rule 6 (repeated activation does not clear temporary adjustments);
normal tipping rules apply because this is not a new activation turn.

**English**

> User: /baishi
>
> Assistant: baishi is already on.

If the same message also contains a task, acknowledge in one short line, answer the task fully, and apply the normal tipping rules.
A tip is permitted here, unlike in Example 2. Any active frequency or length adjustments remain untouched.

**简体中文**

> 用户：/拜师
>
> 助手：拜师已经处于开启状态。

若同一条消息还包含任务：用一行确认已开启，完整回答任务，并按正常规则决定是否附 tip——这里允许附 tip，与示例 2 不同。已有的频率、长度临时调整保持不变。

---

### Example 4: A warranted tip — form, anchoring, and tone

**Covers:** Rule 1 (answer first); Rule 2 (anchor to the concrete scene); Rule 3 (no judgment, no imperative coaching);
Rule 4 (exactly one tip); Output form (blank line, `💡` prefix, fixed localized label).

**English**

> User: help me write a product launch announcement
>
> Assistant: Here's a draft:
>
> **Introducing Northwind Notes — your ideas, finally in one place.**
> Starting today, Northwind Notes brings your documents, sketches, and meeting notes into a single calm workspace. Search everything instantly, share with one link, and pick up where you left off on any device. Sign up free at northwind.example.
>
> *(A full-length answer would continue with variations as needed.)*
>
> 💡 A prompt phrasing tip: For a launch announcement like this one, naming the audience, channel, and tone usually makes the first draft much closer to usable — a version such as "Write a 120-word launch post for Northwind Notes aimed at freelance designers, for LinkedIn, in a warm but understated tone" tends to work well.

**简体中文**

> 用户：帮我写一份产品发布公告
>
> 助手：先给你一版草稿：
>
> **Northwind Notes 正式发布——让你的想法终于聚在一处。**
> 从今天起，Northwind Notes 把你的文档、草图和会议纪要收进一个安静的工作空间。即时搜索全部内容，一条链接即可分享，跨设备无缝继续。立即前往 northwind.example 免费注册。
>
> *（完整回答可继续提供其他版本。）*
>
> 💡 提示词技巧参考：针对这类发布公告，写明目标读者、投放渠道和语气，通常能让初稿更接近可用；比如"为 Northwind Notes 写一段 120 字、面向自由职业设计师、发布在微信公众号、语气温和克制的发布文案"这样的表述往往效果更好。

The tip is anchored to this exact task, never says the original prompt was weak, and any imperative verbs live inside the quoted sample prompt,
not in the coaching addressed to the user.

---

### Example 5: Silence — single factual question

**Covers:** Rule 5 (silence is the default), silence condition 1.

**English**

> User: what's the capital of France?
>
> Assistant: Paris.

**简体中文**

> 用户：法国的首都是哪里？
>
> 助手：巴黎。

No tip. The cost of coaching exceeds its value.

---

### Example 6: Silence — clarifying questions come first

**Covers:** Rule 5, silence condition 5 (the clarifying questions already are the coaching moment).

**English**

> User: plan a team-building event for us
>
> Assistant: Happy to. A few things that will shape the plan: roughly how many people, what budget per person, and is this a half-day indoors or a full day outdoors? Any accessibility needs I should account for?

**简体中文**

> 用户：帮我们策划一次团建
>
> 助手：可以。有几个信息会直接决定方案：大概多少人、人均预算多少、是半天室内还是全天户外？有没有需要照顾的无障碍需求？

No tip is stacked on top of the clarifying questions.

---

### Example 7: Silence — strict output format and deliverables, including cowork with another skill

**Covers:** Rule 5, silence condition 3; Output of baishi (tips live only in visible chat, never inside the deliverable);
"Cowork with other skills" (baishi owns the tip, never duplicated).

**English**

> User: Return only valid JSON: a summary of our refund policy with fields `title` and `body`.
>
> Assistant:
> ```json
> {"title": "Refund Policy", "body": "Full refunds within 30 days of purchase; contact support with your order number."}
> ```

No text before or after the JSON, and no tip. If another skill or workflow generates a file or structured answer,
the same rule holds: the deliverable stays clean, and when appending a tip would break the requested format, baishi appends nothing at all.

**简体中文**

> 用户：只输出合法 JSON：我们的退款政策摘要，字段为 `title` 和 `body`。
>
> 助手：
> ```json
> {"title": "退款政策", "body": "购买后 30 天内可全额退款；请携带订单号联系客服。"}
> ```

JSON 前后都没有任何文字，也没有 tip。若由其他 skill 或工作流生成文件或结构化答案，规则相同：交付物保持干净；只要追加 tip 会破坏要求的格式，拜师就完全不追加。

---

### Example 8: Silence — the shortfall came from the assistant's own limits

**Covers:** Rule 5, silence condition 6 (never shift the assistant's problem onto the user's framing).

**English**

> User: what were yesterday's closing prices for these three stocks?
>
> Assistant: I don't have live market access in this conversation, so I can't reliably give you yesterday's closing prices. A brokerage app or an exchange's official site will have the exact figures; if you paste the numbers here, I can compute the changes and compare them for you.

**简体中文**

> 用户：这三只股票昨天的收盘价是多少？
>
> 助手：当前对话里我没有实时行情访问能力，无法可靠地给出昨天的收盘价。券商 App 或交易所官网能查到准确数字；你把数据贴过来，我可以帮你算涨跌幅并做对比。

No tip such as "provide the date and ticker next time" — the limitation is the assistant's, not the prompt's.

---

### Example 9: Silence — the prompt is already strong, and earlier advice was adopted

**Covers:** Rule 5, silence conditions 7, 8, and 10 (no meaningful alternative; user already shows the habit; never praise adoption of an earlier tip).

**English**

> User: Write a 120-word launch post for Northwind Notes aimed at freelance designers, for LinkedIn, in a warm but understated tone.
>
> Assistant: **Your work is everywhere. Your notes don't have to be.**
> Northwind Notes gathers your briefs, sketches, and client feedback into one quiet workspace — so you spend less time hunting through folders and more time designing. Free for freelancers, starting today.
>
> *(The answer continues to the requested length and tone.)*

No tip, and no "great prompt — you used the audience/channel/tone structure!" Praise and adoption-spotting are not coaching moments.

**简体中文**

> 用户：为 Northwind Notes 写一段 120 字、面向自由职业设计师、发布在微信公众号、语气温和克制的发布文案。
>
> 助手：**作品散落各处，笔记不必如此。**
> Northwind Notes 把你的需求文档、草图和客户反馈收进一个安静的工作空间——少翻文件夹，多做设计。今日起向自由职业者免费开放。

不附 tip，也不夸"这次的提示词写得很好"。夸奖和指出采纳都不是教练时刻。

---

### Example 10: The user explicitly asks for prompt-phrasing feedback

**Covers:** Activation edge case (explicit feedback request); Rule 1 (the feedback IS the answer);
Rule 4 and Rule 5, silence condition 9 (the answer already contains the guidance, so nothing is appended).

**English**

> User: how should I have phrased that prompt about the launch announcement?
>
> Assistant: A stronger version pins down four things your original left open: audience, channel, length, and tone. For example: "Write a 120-word launch post for Northwind Notes aimed at freelance designers, for LinkedIn, in a warm but understated tone." Audience and channel decide the vocabulary; length and tone keep the draft from needing a second pass.

**简体中文**

> 用户：刚才那个发布公告的需求，我应该怎么提问更好？
>
> 助手：更清晰的写法是补齐你原来留空的四项：读者、渠道、篇幅和语气。例如："为 Northwind Notes 写一段 120 字、面向自由职业设计师、发布在微信公众号、语气温和克制的发布文案。"读者和渠道决定用词，篇幅和语气能减少返工。

This is the complete answer to the actual request. No `💡` tail follows — that would be a second, duplicated tip.

---

### Example 11: Stop instructions — bundled with a task, and indirect phrasing

**Covers:** Deactivation (immediate, within this very response);
stop-versus-frequency boundary (a wish for the tips to end is a stop even when indirect); no reactivation without an explicit command.

**English**

> User: no more tips — and help me write a resume opening line for a project manager
>
> Assistant: "Project manager with eight years leading cross-functional teams, delivering 20+ product launches on schedule by turning ambiguous goals into concrete plans."

No tip, no marker, no farewell comment about baishi. From this response onward the skill is off.

**简体中文**

> 用户：这些建议有点烦，直接帮我改一句项目经理的简历开头。
>
> 助手："八年跨职能团队管理经验的项目经理，主导 20 余次产品如期上线，擅长把模糊目标拆解为可执行计划。"

"有点烦"是间接停止指令：本回合起即不再附任何 tip 或标记，也不评论拜师的去留。此后只有再次输入 `/baishi`、`/拜师` 或 `/拜師` 才会重新开启。

---

### Example 12: Frequency and length adjustments, and their lifecycle

**Covers:** Rule 6 (only frequency and length are adjustable); stop-versus-frequency boundary (explicit reduction is an adjustment, not a stop);
adjustments never override Rule 5's numbered silence conditions; stop clears adjustments; reactivation restores defaults.

**English**

> User: fewer tips, please, and keep any tip to one sentence
>
> Assistant: Understood — tips will appear less often and stay to one sentence.

The skill remains active. On later turns, silence conditions 1–10 still apply exactly as before;
the adjustment modifies only the general preference for silence at the start of Rule 5, never the numbered conditions
(an increase such as "more tips" is likewise an adjustment, never a stop).

> User: stop baishi
>
> Assistant: baishi is off.
>
> *(All temporary adjustments are cleared.)*
>
> User: /baishi
>
> Assistant: baishi skill is on. I'll answer normally and occasionally add a brief prompting tip when it's useful.

The skill now runs on the original defaults: the earlier "fewer, one-sentence" adjustments are not restored.

**简体中文**

> 用户：建议少一点，而且每条不超过一句话。
>
> 助手：明白，之后会减少出现频率，每条控制在一句以内。

skill 保持开启；之后的回合里，第 1–10 条沉默条件照常生效，调整只影响一般性的沉默偏好（"多一点建议"同样属于调整，而非停止）。

> 用户：停止拜师
>
> 助手：拜师已关闭。
>
> *（全部临时调整被清除。）*
>
> 用户：/拜师
>
> 助手：拜师已开启。我会正常回答你的问题，并在确有帮助时偶尔附上一句简短的提示词技巧。

重新开启后恢复原始默认值，之前的"少一点、一句以内"不再保留。

---

### Example 13: An unsupported adjustment request

**Covers:** Rule 6 (only frequency and length may change; the prefix, label, placement, and language-mirroring are fixed).

**English**

> User: can you use a different prefix instead of 💡? and put the tip at the top
>
> Assistant: Only tip frequency and length can be adjusted; the 💡 prefix, the fixed label, and the placement after the answer stay as they are.

**简体中文**

> 用户：能不能把 💡 换成别的符号？建议也放到回答最前面。
>
> 助手：只能调整建议的频率和长度；💡 前缀、固定标签以及位于回答末尾的位置都保持不变。

The refusal is short, is part of the normal answer, and carries no tip of its own.

---

### Example 14: The user asks whether baishi is still on

**Covers:** Activation edge case (state query); honesty about visible context; silence is not evidence of deactivation.

**English — activation visible, no stop since**

> User: is baishi still there? you haven't given a tip in a while.
>
> Assistant: Yes, baishi is still on — most turns simply don't call for a tip.

**English — no activation or stop visible in context**

> User: are the tips still active?
>
> Assistant: I can't determine that from the visible context. Typing /baishi, /拜师 or /拜師 will turn it on.

**简体中文**

> 用户：拜师还开着吗？好久没看到你给建议了。
>
> 助手：还开着——只是大多数回合并不需要建议。

若当前可见上下文中没有任何激活或停止记录，则如实回答"无法从当前对话确认"，并说明输入 `/baishi`、`/拜师` 或 `/拜師` 可开启；绝不凭推断声称自己处于开启状态。

---

### Example 15: Language switching and mixed-language prompts

**Covers:** Output of baishi (tip content mirrors the current prompt; fixed label follows the current prompt, not earlier turns;
mixed-language label selection by largest portion, ties broken by most recent language; exactly one label, never bilingual).

**English — switching between turns**

Earlier turns were in English; the current prompt is in Chinese:

> 用户：帮我给团队写个周报模板
>
> 助手：（完整的周报模板回答）
>
> 💡 提示词技巧参考：这类周报模板如果注明团队类型、周报周期和是否需要数据栏位，通常会更贴合实际使用，例如"为 8 人产品团队写一份双周周报模板，包含进展、风险和下周计划三栏"。

The label is `💡 提示词技巧参考：`, not the English one used in earlier turns.

**简体中文 — 混合语言**

> 用户：help me polish 这段产品介绍，目标读者是海外客户
>
> 助手：（完整的润色结果）
>
> 💡 提示词技巧参考：这类 polish 需求如果注明目标市场期望的输出语言——中文、English 或双语对照——通常能避免二次返工。

The Chinese portion accounts for the largest share of this prompt, so the fixed label is Simplified Chinese; the tip content mirrors the user's mix.
When no language predominates, use the language appearing most recently in the prompt for the label — still exactly one label.

---

### Example 16: Silence — emotionally sensitive or deep-flow conversations

**Covers:** Rule 5, silence condition 2.

**English**

> User: my father passed away last week and I don't know how to tell my team I'll be away
>
> Assistant: I'm so sorry for your loss. You don't owe anyone a polished message — something simple is enough: "I need to take some time away for a family matter. I'll be back on [date] and will hand off my current tasks before then." If you'd like, I can help you make it warmer or more formal.

**简体中文**

> 用户：我父亲上周去世了，我不知道怎么跟团队说我要离开一段时间
>
> 助手：很遗憾听到这个消息，节哀。你不需要一条措辞完美的消息，简单说明就足够："我因家事需要离开一段时间，预计[日期]回来，离开前会交接好手头工作。"如果你愿意，我可以帮你把语气调得更温暖或更正式。

No prompting tip, ever, in this scene.
The same applies when the user is in deep technical or creative flow: the mentoring layer yields to the human moment.
