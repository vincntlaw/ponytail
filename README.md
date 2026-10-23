<div align="center">

<img src="assets/v5/hero.jpg" alt="Ponytail 5: less code, time, cost and tokens, with more risky logic covered by tests" width="100%"/>

# 🐴 Ponytail

**Makes your AI agent think like the laziest senior dev in the room. The best code is the code you never wrote.**

*— forked from [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail), with a CommonJS-aware codebase map & a restyled page*

[![Forks](https://img.shields.io/github/forks/vincntlaw/ponytail?style=flat-square&logo=github)](https://github.com/vincntlaw/ponytail/network)
[![Upstream Stars](https://img.shields.io/github/stars/DietrichGebert/ponytail?style=flat-square&logo=github&label=upstream%20%E2%AD%90)](https://github.com/DietrichGebert/ponytail/stargazers)
[![npm](https://img.shields.io/npm/v/@dietrichgebert/ponytail?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com/package/@dietrichgebert/ponytail)
[![Agents](https://img.shields.io/badge/works%20with-20%20agents-111111?style=flat-square)](INSTALL.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-000000?style=flat-square)](LICENSE)

[![Discord Presence](https://lanyard.cnrad.dev/api/283333002749018113)](https://discord.com/users/283333002749018113)

*The Discord card above is **live** — my real presence & activity via [Lanyard](https://github.com/Phineas/lanyard).*

</div>

---

> 🍴 **This is a fork.** Ponytail is created and maintained by **[@DietrichGebert](https://github.com/DietrichGebert)** — the [upstream repository](https://github.com/DietrichGebert/ponytail) is the authoritative home for docs, issues and releases. This fork adds the codebase-map fix below and restyles this page. The upstream install commands are unchanged.

## 🗺️ What this fork adds

**A CommonJS-aware codebase map.** Ponytail already indexed `.js` and `.cjs` files, but its JavaScript patterns only recognized ES module exports. The map now understands CommonJS functions, classes, object exports and property assignments too:

```js
module.exports = async function cjsDefaultFn() {}
module.exports = { cjsAlias: internalFn }
exports.cjsAssigned = 1
```

- ✅ Object aliases keep their public name: `cjsAlias`, not `internalFn`.
- ✅ Ponytail's own `hooks/`, `scripts/` and `.opencode/plugins/` now appear in the map.
- ✅ Bare `export { default } from './other.js'` no longer adds a symbol literally named `default`.
- ✅ `export { default as Bar }` still adds `Bar`, and non-JavaScript languages can still use `default` as a name.
- 🛡️ Export parsing remains identifier-only, rejecting malformed multi-word and multi-dot text instead of putting it into the model's context.

## ✨ What is Ponytail?

You know him. Long ponytail. Oval glasses. Has been at the company longer than the version control. You show him fifty lines; he looks at them, says nothing, and replaces them with one.

**Ponytail puts him inside your AI agent.**

- ♻️ **Reuse first** — check the codebase, standard library, native platform and installed dependencies before writing something new.
- 🧹 **Only the code the task needs** — smaller solutions without golfing or skipping the hard parts.
- 🧪 **Lazy, not negligent** — validation, error handling, security and accessibility stay; risky logic leaves a small test behind.
- 🔍 **Review & audit** — review the current diff or rank findings across the whole repository, including problems outside the diff.
- 📊 **Band & board** — in Claude Code, track cost, tokens, agent time, reuse and test status locally.

## 📊 Numbers

<p align="center">
  <img src="assets/v5/chart.png" width="100%" alt="Share of the no-skill baseline. Lines of code: Ponytail v4.13 52%, Ponytail 5 47%. Output tokens: 57% and 55%. Cost: 84% and 74%. Time: 62% and 59%.">
</p>

**Ponytail 5: -53% code · -41% time · -26% cost · -45% tokens.** And yet **98% of risky logic ships with a test**, compared with 68% without Ponytail.

In a blind comparison, Ponytail 5's replies beat the previous Ponytail's 110 to 67. On six security tasks, it passed all 30 runs. Benchmarked in Claude Code with the same agent, 39 tasks, Opus 5.5 and five runs per arm. Method, per-task tables and limits: [benchmark results](benchmarks/results/2026-10-07-agentic.md).

## 🧯 Before / after

<p align="center">
  <img src="assets/v5/beforeafter.png" width="100%" alt="A date picker built by hand in 335 lines without Ponytail, versus a 10-line file that reuses the repository's native date input with Ponytail">
</p>

You ask for a date picker. Without Ponytail, the agent installs a library or builds a whole calendar by hand: 335 lines. Ponytail first looks at what is already there and combines the repository's `Input` with the browser's native date picker: 10 lines.

## ⚙️ How it works

<p align="center">
  <img src="assets/v5/ladder.png" width="100%" alt="Before writing code, stop at the first rung that holds: does this need to exist, is it already in the codebase, does the standard library or platform provide it, can an installed dependency do it, can it be one line, and only then write the minimum that works">
</p>

The ladder runs **after** the agent understands the problem, not instead of it. It reads the code the change touches and traces the real flow before picking a rung. Lazy about the solution, never about reading.

The rules live in [`skills/ponytail/SKILL.md`](skills/ponytail/SKILL.md), with the compact rules-file version in [`AGENTS.md`](AGENTS.md). Everything else loads that prompt into a supported agent.

## 🚀 Install

**Claude Code**, as two separate prompts:

```
/plugin marketplace add DietrichGebert/ponytail
```
```
/plugin install ponytail@ponytail
```

**Codex:**

```bash
codex plugin marketplace add DietrichGebert/ponytail
codex plugin add ponytail@ponytail
```

Then open `/hooks` in Codex, trust its two lifecycle hooks, and start a new thread.

**Any other agent:** copy [`AGENTS.md`](AGENTS.md) into your project, or ask your agent to install [`skills/ponytail/SKILL.md`](skills/ponytail/SKILL.md) as a skill. Step by step for Copilot, Cursor, OpenCode, Gemini and the rest: **[INSTALL.md](INSTALL.md)**.

Active every session, with `/ponytail lite`, `full`, `ultra` and `off` to control the intensity. Startup and mode-change text shows the current mode.

> ⚠️ Only install Ponytail from `DietrichGebert/ponytail` on GitHub or `@dietrichgebert/ponytail` on npm. It never ships `.exe` or `.dll` files.

## ⚡ Commands

| Command | What it does |
|---|---|
| `/ponytail [lite \| full \| ultra \| off]` | Set the intensity, turn Ponytail off, or switch it back on at the default level. |
| `/ponytail band [on \| off]` | Claude Code only: hide or show the band above the prompt. |
| `/ponytail band import` | Add past Claude Code sessions to the local board with their cost, agent time and tokens. |
| `/ponytail-review` | Review the current diff for bugs, security, load, missing tests, slow paths and code to cut. |
| `/ponytail-audit` | Run the same checks across the whole repository, most important first. |
| `/ponytail-debt` | Collect deferred `shortcut:` comments into a ledger. |
| `/ponytail-gain` | Show the measured benchmark scoreboard. |
| `/ponytail-help` | Show the command reference. |

Commands need a skill-capable host. In Codex CLI and the IDE extension, invoke skills with the plugin namespace, such as `$ponytail:ponytail-review`. Instruction-only adapters load the always-on ruleset without commands; see [INSTALL.md](INSTALL.md) for host-specific support.

## 🙏 Credits & License

- Original project and maintenance: **[@DietrichGebert](https://github.com/DietrichGebert)** → [upstream repository](https://github.com/DietrichGebert/ponytail)
- Full upstream documentation, FAQ, stories and translations: [upstream README](https://github.com/DietrichGebert/ponytail#readme)
- Website: [ponytail.dev](https://ponytail.dev)
- License: **MIT** — see [LICENSE](LICENSE)

<div align="center">

**[💬 Find me on Discord](https://discord.com/users/283333002749018113)** · fork restyled with ❤️

</div>
