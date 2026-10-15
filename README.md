# Rate my idea

**A Claude Code plugin: Claude rates every request you make from 1 to 10, and says whether it would do it if the product were its own.**

You get honest product judgment next to the work, not just a yes. Claude still does the task (unless it's unsafe), but
now you also hear when it thinks you're about to make a mistake, and what would make the idea a 10.

```
you    › add a fourth pricing tier between Pro and Team

claude › Rating 4/10. I wouldn't: a fourth tier splits buyers who already hesitate.
         Doing it anyway since you asked; a 10 would be one plan with a yearly discount.
         …then builds the tier properly.
```

```
you    › make the onboarding one screen instead of three

claude › Rating 9/10. I'd do it: every extra screen loses people before they see the product.
         …then does it.
```

## Install

In Claude Code:

```
/plugin marketplace add IlhamOrujov/rate-my-idea
/plugin install rate-my-idea@rate-my-idea
```

Restart Claude Code. From then on every request gets its one-line rating.

**Just the skill, no plugin:** copy `skills/rate-my-idea` into `~/.claude/skills/` (all projects) or
`.claude/skills/` (one project). Claude then uses it when it decides the skill applies; the plugin also adds a tiny
reminder on each message so it applies every time.

## How it rates

| Score | Meaning |
|---|---|
| 9 to 10 | Clearly the right move. It would push for it itself. |
| 7 to 8 | Good, with small reservations. |
| 5 to 6 | Fine, but low impact or a real tradeoff. |
| 3 to 4 | It would push back, and says what it would do instead. |
| 1 to 2 | It strongly advises against it, and still does it if it's safe. |

The rules it follows: be honest and use the whole scale, rate the idea and not the person, one line only (the work is
the main event), name what would make it a 10 when the score is below 8, skip plain questions and small talk, and stop
when you say "stop rating". The full instructions are in [`skills/rate-my-idea/SKILL.md`](skills/rate-my-idea/SKILL.md).

## Turn it off

- For one conversation: say "stop rating".
- Everywhere: `/plugin disable rate-my-idea`, or start Claude Code with `RATE_MY_IDEA=off` to silence the reminder.

## How it works

- `skills/rate-my-idea/SKILL.md`: what to rate, the format, the scale and the rules.
- `.claude-plugin/plugin.json`: a `UserPromptSubmit` hook that adds one line of context to each message, so the
  rating happens every time and not only when Claude picks the skill. No scripts, no network, no data leaves your
  machine: the hook only prints a fixed sentence.

## Why

It started as a standing rule for one product: "every time I tell you to do something, rate it and tell me if you'd do
it if the product were yours." The ratings turned out to be the most useful part of the conversation, so here it is
for everyone.

Made by [Ilham Orujov](https://github.com/IlhamOrujov), founder of [OrujovAI](https://www.orujovai.com).
MIT licensed.
