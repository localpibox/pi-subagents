<div align="center">

# LocalPibox Pi-Subagents Fork

**Centralized subagent model registry for [Pi](https://pi.dev)**

[![Upstream: tintinweb/pi-subagents](https://img.shields.io/badge/upstream-tintinweb/pi--subagents-blue)](https://github.com/tintinweb/pi-subagents)
[![Fork branch: master](https://img.shields.io/badge/fork-master-green)](https://github.com/localpibox/pi-subagents)

</div>

> **⚡ [← Back to LocalPibox](https://github.com/localpibox/localpibox)** — project overview, architecture, and the full stack.

---

## What this fork adds

This fork of [`tintinweb/pi-subagents`](https://github.com/tintinweb/pi-subagents)
adds a **centralized subagent model registry** — it removes Anthropic-heavy
defaults and makes all subagents inherit the session's model by default.

This is critical for stacks that run entirely on local models (like LocalPibox):
without this change, subagents would default to `anthropic/claude-sonnet-4-20250514`
and fail when no Anthropic API key is configured.

**All LocalPibox work is kept as a single squashed commit** on top of upstream.

### Changes

| Change | What it does | Files |
|---|---|---|
| **Centralized model registry** | All subagents inherit the session model (`model: null` / `parent`) instead of hardcoding Anthropic defaults | `src/index.ts`, `src/settings.ts`, `src/agent-runner.ts`, `src/default-agents.ts` |
| **Workflow removal** | Removed a workflow file due to OAuth scope limitation | `.github/workflows/` |

### Upstream mapping

| LocalPibox | → | Upstream |
|---|---|---|
| `localpibox/pi-subagents` (fork) | ← | `tintinweb/pi-subagents` (master) |

- **Upstream latest:** v0.14.3
- **Update policy:** follow **master** releases; submit upstream if clean
- **Branch strategy:** `master` branch carries LocalPibox changes on top of upstream

## Features (inherited from upstream)

See the [upstream README](https://github.com/tintinweb/pi-subagents/blob/master/README.md)
for the full feature set:

- Claude Code-style autonomous sub-agents
- Parallel background agents with concurrency limits
- Live widget UI with token counts and status icons
- FleetView — navigable list of running subagents
- Custom agent types via `.pi/agents/<name>.md`
- Nested subagents with depth capping
- Mid-run steering, session resume, scheduled agents
- Git worktree isolation, skill preloading, tool denylists

## Install

```bash
# Via Pi (LocalPibox fork)
pi install git:github.com/localpibox/pi-subagents@master
```

## Configuring for local models

The LocalPibox fork makes all subagents inherit the parent session's model by
default. Configure the parent model in `pi-defaults.json`:

```json
{
  "extensions": {
    "@tintinweb/pi-subagents": {
      "globalDefaultModel": null,
      "disableDefaultAgents": true
    }
  }
}
```

`globalDefaultModel: null` means subagents use whatever model the parent session
is using — no Anthropic dependency.

## Upstreaming

The centralized model registry patch is **a candidate upstream contribution**.
If it proves generally useful for non-Anthropic stacks, it will be submitted to
`tintinweb/pi-subagents`.

## License

See the [upstream license](https://github.com/tintinweb/pi-subagents/blob/master/LICENSE).
LocalPibox patches inherit the same license.
