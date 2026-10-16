---
name: random-number
description: Generates cross-platform random integers. On Linux/macOS it uses awk (native on any distro and on macOS). On Windows it uses PowerShell's Get-Random. Supports an optional range [min, max] and an optional seed for reproducible results. Use it when the user asks for a random number, rolling dice, picking at random, raffles, or deterministic results via seed.
---

# Random Number Generator

Generates an **inclusive** random integer in `[min, max]` with no external dependencies: `awk` is already present on Linux/macOS, and `Get-Random` ships with PowerShell.

## When to use

- "Give me a random number between X and Y"
- Rolling dice, raffles, picking an index at random
- Reproducible result for tests (same seed → same number)

## When NOT to use

- Decimals/floats → use `awk 'BEGIN{srand(); print rand()}'` or `Get-Random -Minimum 0.0 -Maximum 1.0`
- Cryptography → `openssl rand` or `[System.Security.Cryptography.RandomNumberGenerator]`
- Ranges > 2^31 in awk with seed (limitation of `srand`)

## Parameters

| Parameter | Required | Default        | Description                     |
|-----------|----------|----------------|---------------------------------|
| `min`     | No       | `0`            | Lower bound (**inclusive**)     |
| `max`     | No       | `2147483647`   | Upper bound (**inclusive**)     |
| `seed`    | No       | (entropy)      | Integer seed for reproducibility|

Rules:
- If only `max` is passed, the range is `[0, max]`.
- If `min > max`, they are swapped.
- The result is **inclusive** on both ends.

---

## Linux / macOS → awk

### Without seed (truly random)
```bash
awk -v min=MIN -v max=MAX 'BEGIN{srand(); print int(rand()*(max-min+1))+min}'
