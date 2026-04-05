# Claude Code 2.1.88 — Source Recovery

<p align="center">
  <img src="https://img.shields.io/badge/Version-2.1.88-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/Status-Recovered-green.svg" alt="Status">
  <img src="https://img.shields.io/badge/Language-TypeScript-blue.svg" alt="Language">
  <img src="https://img.shields.io/badge/UI-Ink%20%2F%20React-orange.svg" alt="UI">
</p>

> [!IMPORTANT]
> This is a source reconstruction project for `@anthropic-ai/claude-code` version **2.1.88**.
> When this version was published to npm, it accidentally included a `cli.js.map` source map
> containing the full original source. This project uses the `sources` and `sourcesContent`
> fields from that map to reconstruct a readable source tree — for the purpose of studying
> Claude Code's CLI architecture, command system, and MCP implementation.
>
> The recovered source spans approximately **700,000 lines of code**.
>
> <img width="794" height="387" alt="Source recovery stats" src="https://github.com/user-attachments/assets/ab30578b-d6d2-440c-abde-ddf09e5d42de" />

---

## Background

On **2026-03-31**, Anthropic published `@anthropic-ai/claude-code@2.1.88` to npm with a
`cli.js.map` source map that contained the full TypeScript source code of the application.

<img width="1497" height="242" alt="npm upload with source map" src="https://github.com/user-attachments/assets/b1a01c8d-f14c-46d5-b6cb-4f5b4f90c9ab" />

This version has since been **removed from the official npm registry**. Running
`npm install @anthropic-ai/claude-code@2.1.88` will now fail. However, it can still
be installed from the Tencent npm mirror cache while it remains available:
```shell
npm install -g https://mirrors.cloud.tencent.com/npm/@anthropic-ai/claude-code/-/claude-code-2.1.88.tgz
```

<img width="626" height="370" alt="Install from mirror" src="https://github.com/user-attachments/assets/bcc1d094-f19d-4bd7-b53b-898399c6d117" />

> Act fast — mirror caches may also expire without notice.

---

## Project Structure

The recovered source is organized under `src/`, closely mirroring the original layout:

| Directory | Description |
|-----------|-------------|
| `src/entrypoints/` | CLI entry points and initialization logic |
| `src/commands/` | Full command system (`login`, `mcp`, `review`, `tasks`, etc.) |
| `src/components/` | Terminal UI components built with **React + Ink** |
| `src/services/` | Core business logic (policies, sync, remote capabilities, etc.) |
| `src/hooks/` | Interactive terminal state management |
| `src/utils/` | Auth, file operations, process management, and other utilities |
| `src/ink/` | Custom terminal rendering infrastructure |

---

## What's Interesting in the Source

The recovered code reveals several architectural highlights:

- **Command loading system** — Supports a hybrid loader for built-in commands, dynamic skills, plugins, and MCP commands all in one pipeline.
- **Terminal UI with React** — Shows how complex interactive interfaces are built in the terminal using React component trees rendered by Ink.
- **MCP deep integration** — Concrete implementation of the Model Context Protocol inside a production CLI tool.
- **Feature flags** — Build-time feature flags and conditional compilation patterns are visible throughout the codebase.

---

## Package Contents (npm tgz)

| File | Size | Description |
|------|------|-------------|
| `cli.js` | ~13 MB | Entire application — minified, bundled JavaScript (Node.js ESM) |
| `cli.js.map` | ~57 MB | Source map — maps minified positions back to original TypeScript |
| `package.json` | ~1 KB | Package metadata and dependency declarations |
| `sdk-tools.d.ts` | ~117 KB | TypeScript type definitions for all tool input/output schemas |
| `LICENSE.md` | — | Anthropic copyright notice |
| `vendor/ripgrep/` | — | Pre-compiled `rg` binaries for all platforms (used by the Grep tool) |
| `vendor/audio-capture/` | — | Pre-compiled audio capture `.node` binaries for all platforms |

### About the CJK Text in cli.js

The Chinese and Japanese strings embedded in `cli.js` are **not part of Anthropic's own code**.
They come from the bundled **Zod** validation library, which ships i18n error messages in 24
languages. They only appear if the user's system locale is set to Chinese or Japanese.

Examples:

| Simplified Chinese | English Equivalent |
|--------------------|--------------------|
| `无效输入：期望 X，实际接收 Y` | `Invalid input: expected X, received Y` |
| `数值过大：期望 X <= Y` | `Value too large: expected X <= Y` |
| `无效字符串：必须满足正则表达式` | `Invalid string: must match regex` |
| `出现未知的键(key)` | `Unrecognized key(s)` |

---

## Running the Source (Experimental)

If you want to attempt running the recovered code:

1. Add a `package.json` and configure the required dependencies.
2. Set up a compatible build toolchain (the original uses Bun).
3. Handle `bun:bundle` macros and feature flag values.
4. Verify that core commands execute correctly.

---

## Disclaimer

- **Unofficial** — This repository is not affiliated with or endorsed by Anthropic.
- **Copyright** — All original code, trademarks, and intellectual property belong to Anthropic PBC.
- **Research only** — This project exists for archival purposes, structural analysis, and code study. It is not an official open-source release.
- **Legal responsibility** — If you intend to redistribute or use this commercially, assess the applicable licenses and legal risks yourself.

---

## Acknowledgement

Thanks to the accidentally included **source map** that made this reconstruction possible —
and to the engineering quality it revealed.

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=HP980322/claude_code_src&type=Date)](https://star-history.com/#HP980322/claude_code_src&Date)