# Remolt 🦀

**Shed your shell. Grow it back better.**

Remolt is a blueprint-first starter for building your own AI **mission control** — a lightweight Next.js gateway that your agents operate, extend, and rebuild. Crabs molt: they shed their entire shell and regrow it from a blueprint. Remolt gives your system the same power — delete everything, regrow from prompts.

> **Status: pre-alpha.** This repo is being grown in public from an architecture blueprint. Watch/star to follow along.

## The idea

Most starter templates are dead ends: the moment you customize them, you can never pull upstream changes again. Remolt inverts this.

- A **small deterministic core** — a runnable Next.js gateway skeleton (dashboard shell, cron tick, SQLite, env/secrets status) that boots the moment you clone it.
- A **prompt library** — the architecture lives as executable specs. Your agent (Claude Code, Codex, Cursor — any of them) reads the prompts and grows the system *into your environment*: your services, your keys, your desks.
- The **`remolt` CLI** — the molt cycle as commands:

| Command | What it does |
|---|---|
| `remolt init` | Bootstrap a new mission control from the blueprint |
| `remolt plan` | Diff your system against the blueprint; show what's changed upstream |
| `remolt grow` | Emit growth prompts for your agent to extend the system |
| `remolt shed` | Tear down generated code (state survives — it lives outside the shell) |
| `remolt update` | Prompt-mediated self-update: your agent reconciles upstream changes into *your* customized system |

Because updates are **prompt-mediated instead of git-merged**, they survive divergence. Your mission control and the blueprint can evolve independently — your agent is the reconciler.

## Principles

1. **Code is what must be exact. Prompts are what should adapt.**
2. **Clone-and-run** — the core boots before any agent touches it.
3. **State outside the shell** — the database and env live outside the regenerable code, so `shed` is always safe.
4. **Agent-framework-agnostic** — prompts follow the [AGENTS.md](https://agents.md) convention; no lock-in to one harness.
5. **Lightweight forever** — the core stays small enough to read in one sitting. Everything else is grown, not shipped.

## Layout (planned)

```
remolt/
├── core/          # the runnable Next.js gateway skeleton
├── blueprint/     # architecture specs + growth prompts (the DNA)
├── cli/           # the remolt CLI
├── examples/      # .env.example and config examples
└── AGENTS.md      # how agents should work in a remolt system
```

## License

MIT
