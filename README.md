# random-number

> A skill for AI agents that generates random numbers in a **procedural**, **deterministic** and **reproducible** way.
>
> Yes. All of that. In a single skill.

---

## What is this

A skill that teaches your AI agent (Claude, GPT, Gemini, whatever reads `SKILL.md`) how to generate random integers on Linux, macOS and Windows.

No external dependencies. Nothing to install. No GPUs. No trillions of dollars.

**Try it:** install it and ask your agent to roll the dice.

```
You: roll a dice
Agent: 4
```

**What it does:**

- 🎲 Generates a random number in a range `[min, max]` (optional)
- 🌱 Accepts an optional seed for **reproducible** results
- 🐧 Works on Linux and macOS
- 🪟 Works on Windows

**What it doesn't do:**

- It's not cryptographically secure
- It doesn't generate decimals
- It doesn't replace `openssl rand` or `RandomNumberGenerator`
- It won't get you a job at OpenAI

---

## Why it exists

Because someone had to do it.

While the entire industry chases AGI by burning down datacenters, here we are: solving the smallest problem in the world with the most boring tool in the world.

And it works.

---

## How to use it

Ask your agent things like:

- *"Give me a random number between 1 and 100"*
- *"Roll a dice"*
- *"Generate a number from 1 to 10 with seed 42"*
- *"I need a reproducible number for a test"*

That's it. The agent does the rest.

---

## Parameters

| Parameter | Required | Default        | Description                     |
|-----------|----------|----------------|---------------------------------|
| `min`     | No       | `0`            | Lower bound (**inclusive**)     |
| `max`     | No       | `2147483647`   | Upper bound (**inclusive**)     |
| `seed`    | No       | (entropy)      | Integer seed for reproducibility|

- If you only pass `max`, the range is `[0, max]`.
- If `min > max`, they get swapped.
- The result is **inclusive** on both ends.

---

## Installation

```bash
git clone <repo-url> ~/.claude/skills/random-number
```

Or copy the folder wherever your agent reads skills from. If your agent doesn't read skills, this repo is useless to you. Sorry.

---

## Repo structure

```
random-number/
├── README.md     ← you are here (for humans)
└── SKILL.md      ← the skill itself (for the agent)
```

No `scripts/`, no `package.json`, no `node_modules`, no Docker, no Kubernetes, no YAML.

One skill. One file. One anonymous hero.

---

## Honest limitations

- Integers only. For floats, use something else.
- Not cryptographically secure. Don't use it for tokens or passwords.
- Seed reproducibility is **not identical** across different `awk` implementations, nor between `awk` and PowerShell. Same seed on a different machine may yield a different number. If you need strict cross-platform reproducibility, be aware.
- Huge ranges with a seed may fail depending on your system's `awk`.

---

## Contributing

PRs welcome. Especially if you add:

- Float support
- Sampling without replacement (multiple numbers at once)
- WSL / Git Bash support

But please: **don't turn it into a framework**.

---

## License

MIT. Do whatever you want. It's a random number generator, not an international treaty.

---

⭐ If this made you smile for even half a second, give it a star. It's free. And unlike your ChatGPT subscription, you'll actually use this one.
