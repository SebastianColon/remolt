# Remolt Mission Control 🦀

**Shed your shell. Grow it back better.**

Build your own AI mission control — a lightweight Next.js gateway your agents operate, extend, and completely regrow from prompts.

Crabs molt: the whole shell is shed and regrown from a blueprint. Remolt gives a software system the same ability. Delete everything, run one command, and your agent rebuilds it — customized to your environment, not to someone else's.

> **Status: pre-alpha, built in public.** The blueprint is public before the code is. Watch or star to follow the build.

## Why this exists

Every starter template dies the same death. You clone it, you customize it, and the moment you do, upstream is unreachable forever — a `git merge` against a diverged fork is a conflict storm nobody wins. So templates rot, and everyone rebuilds from scratch.

Remolt inverts this.

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

## Who it's for

You're running agents that do real work — scheduled jobs, research, monitoring, publishing — and you've outgrown a folder of scripts. You want a dashboard and a job runner you actually control, on your own machine, without adopting a platform that owns your data or a framework that owns your architecture.

Remolt gives you the frame. Your agent builds the rest, into your environment. When the frame improves, you take the improvement without losing your work.

## Running it

Remolt's core is a plain Next.js app. No ops CLI, no process supervisor, no deploy pipeline — those are *your* operational choices, and the blueprint has growth prompts for adding the one that fits your environment.

```bash
npm install && npm run dev     # http://localhost:3000
npm run build && npm start     # production
```

Port 3000 is the default so a clone never collides with whatever you already run. Set `PORT` to move it.

**Scheduled jobs run in-process.** A tick loop lives inside the Next.js server — one process, zero setup, running the moment you clone. The trade-off is deliberate and worth stating plainly: an in-process scheduler cannot exist on serverless platforms, so a Remolt system wants an always-on host.

The tick is written as a thin *driver* that invokes job handlers, and handlers never know what triggered them. Swapping to an external trigger (system cron, GitHub Actions, a platform scheduler hitting an authenticated route) means replacing the driver, not rewriting the jobs.

**State lives outside the shell.** The database path and env file are configured to sit outside the repo directory, which is what makes `remolt shed` safe — delete the entire application tree and your data survives to be regrown around.

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
