English | [中文](README.md)

# gongzi-teaches-code-review

An agent skill that reviews a diff for **over-engineering**: which lines can be deleted. One line per finding — location, what to cut, what replaces it — ending with a single number: how many lines shorter this diff can get.

It does not touch correctness bugs, security, or performance. That's a normal review. This one answers a single question: **how much of this code shouldn't exist at all.**

![改动审查：一行一条，只说哪些可以删](screenshots/hero.png)

## Why it exists

The problem with AI-written code isn't that it's wrong. It's that there's too much of it. One extra abstraction, one extra wrapper, one interface with a single implementation — each looks reasonable on its own. Together they become maintenance cost.

A normal code review says "isn't this a bit complex?", you say "we might need to extend it later", and that's the end of it. This skill doesn't leave room for "might": every finding has to name **what replaces it**. If you can't name a replacement, don't raise it.

## What it does

1. Reads the diff
2. Tags each finding: `delete:` / `stdlib:` / `native:` / `yagni:` / `shrink:`
3. One line per finding, in the form `<line>: <tag> <what to cut>. <replacement>.`
4. Ends with `net: -N lines possible.`

Nothing to cut? It says `Lean already. Ship.` and stops.

## The five tags

| Tag | Targets | Replacement |
|---|---|---|
| `delete:` | Dead code, unused flexibility, speculative features | Nothing. Just delete it |
| `stdlib:` | Hand-rolled versions of something the standard library ships | Name the function |
| `native:` | Dependencies or code doing what the platform already does | Name the feature |
| `yagni:` | Abstractions with one implementation, config nobody sets, layers with one caller | Inline it until a second one exists |
| `shrink:` | Same logic, fewer lines | Show the shorter form |

## What it looks like

```
❌ "This EmailValidator class might be more complex than necessary.
   Have you considered whether all these validation rules are
   needed at this stage?"

✅ L12-38: stdlib: 27-line validator class. "@" in email, 1 line,
   real validation is the confirmation mail.

✅ L4: native: moment.js imported for one format call.
   Intl.DateTimeFormat, 0 deps.

✅ repo.py:L88: yagni: AbstractRepository with one implementation.
   Inline it until a second one exists.

✅ L30-44: shrink: manual loop builds a dict.
   dict(zip(keys, values)), 1 line.
```

## Install

```bash
git clone https://github.com/chengangrun-ai/gongzi-teaches-code-review.git \
  ~/.workbuddy-ai/skills/gongzi-teaches-code-review
```

Claude Code users: drop the folder into `~/.claude/skills/`. **No dependencies, no pip install** — one `SKILL.md` is the whole skill.

## Usage

After you finish a change, say:

```
/ponytail-review
```

Or just ask: "is there any over-engineering in this diff?" / "can this code be shorter?"

## Boundaries

- Complexity only. Correctness bugs, security holes, and performance are out of scope — route them to a normal review.
- Lists findings, applies nothing. Your code stays untouched.
- A single smoke test or `assert` self-check is the minimum, not bloat. It won't ask you to delete your tests.
- To exit: say "normal mode" or `stop ponytail-review`.

## Credits

Rewritten from [Ponytail](https://github.com/DietrichGebert/ponytail) (MIT, by DietrichGebert). The original copyright notice is preserved in `LICENSE`.

## License

MIT. See [LICENSE](LICENSE).

Made by [Gongzi](https://github.com/chengangrun-ai).
