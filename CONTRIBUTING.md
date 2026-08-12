# Contributing to LocalPibox Pi-Subagents Fork

This fork adds a centralized subagent model registry to `pi-subagents`. This
document explains how to contribute — whether by improving the LocalPibox patch,
forking for your own stack, or feeding changes back upstream.

## The Patch Model

All LocalPibox changes are kept as a **single squashed commit** on top of
upstream `master`. This keeps the delta clean and makes rebasing straightforward.

```
upstream master ──→ [v0.14.3] ──┐
                                 │
lpb master       ──→ [lpb patch]──┘
```

### Working on a patch

1. Fork or clone `localpibox/pi-subagents`
2. Make your changes in a feature branch
3. Squash into one commit: `git commit -S -s --squash`
4. Push and open a PR against `master`

### Rebasing onto new upstream changes

```bash
# Fetch latest upstream
git fetch https://github.com/tintinweb/pi-subagents.git master:upstream-master

# Rebase the lpb patch
git checkout master
git rebase upstream-master

# Resolve conflicts, force-push
git push --force-with-lease origin master
```

## Forking for Your Own Stack

If you want to personalize this extension:

1. **Fork** `localpibox/pi-subagents` to your own GitHub account
2. **Customize** — adjust default agents, add custom model selections, or tweak
   the registry behavior
3. **Install** from your fork:
   ```bash
   pi install git:github.com/<you>/pi-subagents@<your-branch>
   ```
4. **Repoint** any existing installations:
   ```bash
   pi remove git:github.com/localpibox/pi-subagents
   pi install git:github.com/<you>/pi-subagents@<your-branch>
   ```

See the
[Forking & Repointing guide](https://github.com/localpibox/devstack#forking--repointing)
for the full stack procedure.

## Feeding Back Upstream

The LocalPibox patch (centralized model registry) is intended as a **candidate
upstream contribution**.

1. **Open an issue** on `tintinweb/pi-subagents` describing the use case
   (non-Anthropic stacks, local model defaults)
2. **Split your patch** — ensure it's clean and not tied to LocalPibox config
3. **Submit a PR** against `tintinweb/pi-subagents` master
4. **Follow up** — if merged, fold into the LocalPibox patch set

### What goes upstream

- ✅ General-purpose features (model registry, parent-model inheritance)
- ✅ Bug fixes applicable to all installations
- ✅ Config patterns that help non-default-provider users

### What stays local

- ❌ LocalPibox-specific configuration (hardcoded model names, registry entries)
- ❌ Stack-specific agent definitions

## Reporting Issues

- **Extension core issues** → [tintinweb/pi-subagents/issues](https://github.com/tintinweb/pi-subagents/issues)
- **LocalPibox patch issues** → [localpibox/pi-subagents/issues](https://github.com/localpibox/pi-subagents/issues)
- **Stack configuration** → [localpibox/devstack/issues](https://github.com/localpibox/devstack/issues)

## Communication

- [Pi Discord](https://discord.com/invite/3cU7Bz4UPx) — upstream community
- Issues and PRs on GitHub — preferred for technical discussions
