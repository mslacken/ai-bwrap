# Changelog

All notable changes to this project are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Multi-agent sandbox wrapper with built-in agents: `claude`, `opencode`,
  `grok`, and `bash` (aliases `cc`, `oc`).
- Extensible agent registry — define `agent_<name>` functions in
  `~/.config/ai-bwrap/config.sh` without editing the wrapper.
- CLI options: `--branch`, `--overlay`, `--bind`, `--ro-bind`, `--no-net`,
  `--dry-run`, `--list`, `--help`.
- `--overlay` runs the agent on a private copy-on-write view of the working
  directory (kernel overlayfs). On exit you get a summary of what changed and
  are asked whether to write it back; declining leaves your tree untouched.
  Where `--branch` copies the tree up front and leaves you to merge, `--overlay`
  records only the changes and merges them back on one keypress — the two are
  mutually exclusive. Scratch layers live under `$AI_BWRAP_OVERLAY_BASE`
  (default `~/.local/share/ai-bwrap`), which must be on a real filesystem with
  user xattr support.
- `EXTRA_BINDS` / `EXTRA_RO_BINDS` config hooks for shared passthrough mounts.
- `scripts/screenshots.sh` to regenerate README images with `freeze`.

### Changed

- The `claude` agent no longer runs with `--dangerously-skip-permissions`; it
  starts with Claude Code's own default permission mode. Pass the flag yourself
  if you want the old behaviour: `ai-bwrap claude -- --dangerously-skip-permissions`.

[Unreleased]: https://github.com/didvc/ai-bwrap
