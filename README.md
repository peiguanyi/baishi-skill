# baishi 拜师

**A little tail on the end of your AI's answers containing prompt tips, when they'll actually help.**

English · [简体中文](README.zh-CN.md) · [繁体中文（香港）](README.zh-HK.md)

The baishi is from Chinese 拜师 (bàishī), which literally means "to acknowledge a mentor." This skill keeps that core idea and drops the ceremony: in the form of a Skill, at the right moment, you get a small tip on how to write a better prompt.

---

## Who is this skill for?

**If you** use AI to look stuff up, write something, clean up a document, or plan a trip — the everyday stuff — and you've never read a thing about "prompt engineering," this skill was written for you.

**If you** write prompts for a living, or you already think about context, examples, and output formats, you'll probably find what this skill offers pretty basic.

## Has this happened to you?

You ask AI for help. It answers, but it's not quite what you wanted. So you add a line, then another. A few rounds later, you finally get there.

A better prompt from the start would've gotten you there faster.

That's what baishi is: a small skill that hands you prompt tips along the way.

## What it looks like

You talk to AI the way you always do. Every so often it puts a little tail at the end of the answer, and in passing shows you how the prompt could be improved for the situation you're in.

**Writing copy**

> **You:** help me write a product launch announcement
>
> **AI:** *(the full draft you asked for)*
>
> 💡 A prompt phrasing tip: For a launch announcement like this one, naming the audience, channel, and tone usually gets the first draft much closer to usable — something like "Write a 120-word launch post for freelance designers, on LinkedIn, in a warm but understated tone" tends to land better.

**Same request, asked in other languages such as Chinese** — whatever language you use, that's the language the tail comes back in

> **你：** 帮我查一下新能源车的补贴政策
>
> **AI：** *（完整的查询结果）*
>
> 💡 提示词技巧参考：这类政策查询如果写明城市、购车时间和用途（代步、营运、置换），通常能直接拿到适用条款，比如"查一下 2026 年上海个人购买纯电车的补贴标准和申请条件"。

**When there's nothing to teach**

> **You:** what's the capital of France?
>
> **AI:** Paris.

Nothing to teach means nothing to add — the AI finishes its normal answer and that's it.

## Most of the time it stays quiet

It won't chatter. In cases like these, baishi doesn't have good advice to give, so it says nothing at all:

- You asked a simple factual question. There's no point polishing the prompt for that.
- You're using AI for something complex, or talking through an emotional issue. You don't want a stray tip cutting in.
- The answer has to be a specific format (JSON, a file, a table). Better to stay quiet than risk a tip landing inside it.
- The AI asked you a clarifying question. Your explanation is already doing the work of a better prompt, so the skill doesn't need to repeat it.
- Your original prompt already solved the problem and got you what you needed. Nothing more to say.
- The answer fell short because of the AI's own limits, not because of how you worded the prompt. The skill won't react to that.

## Install

Copy this line to your AI. It'll handle the rest.

```
Please install this skill for me: https://github.com/peiguanyi/baishi-skill
```

If you'd rather do it yourself:

1. Download: on this page, click Code → Download ZIP, then unzip.
2. Place: put the folder in the directory your agent reads skills from.
3. Reload: restart the agent or start a new session, then type `/baishi`.

To uninstall, just delete the `baishi` folder.

## Turn it on

Once it's installed, turn baishi on by typing any one of these:

```
/baishi
/拜师
/拜師
```

If you start a new session and still want keep the baishi on, you'll need to type the command again in that new session.

Nothing happened? Take a look at [Troubleshooting](#troubleshooting).

## Adjust

You may want to change how often the tail shows up, or how long it runs. Just tell the agent what you want — but these adjustments only apply to the current session and the current skill invocation.

## Turn it off

Tell the agent clearly that you want to stop baishi, and it turns off. For example:

`stop baishi` · `no more tips` · `I just want the answers`

## Turn it back on

After you turn baishi off, type `/baishi` again to switch the skill back on.

## What it's actually teaching

The baishi gives you a rewrite of your prompt, never a lecture on theory.

| What's usually missing | What the tip adds |
| --- | --- |
| Who it's for | reader, audience, persona |
| Where it's going | channel, format, medium |
| How long | words, items, sections |
| What tone | tone, level of formality |
| What "good" looks like | a short example of the finished thing |
| What to leave out | constraints, exclusions |

## FAQ

**Will it change my answer?**
No. The AI's full original answer always comes first. The skill itself doesn't touch it.

**Is it a prompt grading system?**
No. It doesn't grade your prompts. It just offers suggestions in some situations.

**Does it upload my content anywhere?**
No. This skill is, at heart, one Markdown file. No code runs, and your conversation isn't uploaded anywhere.

**Does it work in Chinese or other languages?**
Yes. The tail uses whatever language you're using in the conversation.

**Can I use it alongside other skills?**
Yes. The baishi only adds a tail to the end of the AI's answer. Whether the answer itself came from another skill makes no difference to baishi.

**I turned it on, but I've gone several rounds without seeing a tail.**
That's normal and it means your prompt was already good enough. See [Most of the time it stays quiet](#most-of-the-time-it-stays-quiet).

## Troubleshooting

**I typed `/baishi` and nothing happened.**
Start a new session and try again. If it still doesn't recognize the command, your agent probably doesn't pass slash commands through to skills — this skill can only be turned on by command, so it won't work in that setup for now.

**A tip ended up inside a file, or messed up my output.**
That's a bug: by design, the skill is forbidden from writing tips into deliverables. If you'd like to help improve it, open an issue and paste the conversation in.

**I want to turn the tail off, but it won't turn off.**
Send `stop baishi` on its own, as a separate message. Still going? Open an issue so we can fix it.

## What's in the skill

One file: [`SKILL.md`](SKILL.md). It contains five operating rules, 10 silence conditions, and one rule about user-initiated adjustments.

## License

MIT.

## Credits

The baishi Skill V1.0.0 was made and published by [peiguanyi](https://github.com/peiguanyi). Issues and PRs welcome.
