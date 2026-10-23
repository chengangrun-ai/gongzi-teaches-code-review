# 公子教代码做事 · 改动审查

【过度设计审查】只看「哪些可以删」，一行一条：位置 + 该砍什么 + 用什么替代， 结尾给出 net: -N 行（能省多少行）。只管复杂度，正确性 bug、安全、性能不在 范围内；只列清单，不改代码。触发词：/ponytail-review、审查过度设计、 这段代码能不能删、是不是过度设计了、简化评审。

## 📺 看看效果

![ponytail-review](screenshots/hero.png)

> 把 `screenshots/hero.png` 换成真实效果图（建议 1200px 宽、不超过 400KB）

## What This Does

【过度设计审查】只看「哪些可以删」，一行一条：位置 + 该砍什么 + 用什么替代， 结尾给出 net: -N 行（能省多少行）。只管复杂度，正确性 bug、安全、性能不在 范围内；只列清单，不改代码。触发词：/ponytail-review、审查过度设计、 这段代码能不能删、是不是过度设计了、简化评审。

### Key Features

- Format
- Examples
- Scoring
- Boundaries

## Installation

### WorkBuddy

```bash
git clone https://github.com/<you>/ponytail-review.git ~/.workbuddy-ai/skills/ponytail-review
pip install -r ~/.workbuddy-ai/skills/ponytail-review/requirements.txt
```

### Claude Code / 其他 Agent

```bash
mkdir -p ~/.claude/skills/ponytail-review
cp -R SKILL.md README.md requirements.txt scripts references \
      ~/.claude/skills/ponytail-review/
```

把仓库链接丢给 agent，它会按 `SKILL.md` 加载所需文件。

## Usage

触发词：**/ponytail-review、审查过度设计**

## Architecture

| 文件 | 作用 |
|---|---|
| `SKILL.md` | 触发条件与流程 |

## Requirements

- Python 3.9+
- `pip install -r requirements.txt`

## Credits

基于 [Ponytail](https://github.com/DietrichGebert/ponytail)（MIT，作者 DietrichGebert）改写

Created by 公子 · [@你的GitHub](https://github.com/).

## License

MIT — Use it, modify it, share it.
