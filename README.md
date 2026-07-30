<div align="center">

<p><strong>English</strong> · <a href="README.ko.md">한국어</a></p>

<h1>extract-design-md</h1>

<p>
Turn design rules scattered across a frontend codebase into a reusable,<br>
evidence-backed <code>DESIGN.md</code>.
</p>

[![DESIGN.md 0.4.0](https://img.shields.io/badge/DESIGN.md-0.4.0-2563EB?style=classic)](https://github.com/google-labs-code/design.md)
[![Agent Skill](https://img.shields.io/badge/Agent-Skill-111827?style=classic)](skills/extract-design-md)
[![Apache License 2.0](https://img.shields.io/badge/License-Apache--2.0-64748B?style=classic)](LICENSE)

<p>
  <a href="#what-you-get">What you get</a> ·
  <a href="#install">Install</a> ·
  <a href="#use">Use</a> ·
  <a href="#example-output">Example</a>
</p>

</div>

---

`extract-design-md` analyzes an existing frontend codebase and creates a reviewable `DESIGN.md` at the project root. The result gives coding agents reusable guidance for colors, typography, spacing, shapes, components, responsive behavior, accessibility, themes, and motion.

> Source code is the primary evidence. A matching local app or website URL can be used for optional runtime verification.

The Skill follows the [Google Labs DESIGN.md format specification](https://github.com/google-labs-code/design.md) pinned to `0.4.0`.

## What you get

| Result | Why it matters |
|---|---|
| Project-root `DESIGN.md` | Gives coding agents persistent design guidance |
| Evidence-backed rules | Keeps unused or guessed values from becoming project standards |
| Machine-readable tokens | Preserves exact colors, typography, spacing, shapes, and component values |
| Human-readable guidance | Explains how and why the design rules should be applied |
| Reviewed updates | Prevents an existing `DESIGN.md` from being silently overwritten |

## From source to DESIGN.md

<div align="center">

<code>Frontend source</code> → <code>Evidence-backed analysis</code> → <code>Optional runtime verification</code> → <code>Reviewed DESIGN.md</code>

</div>

## What it analyzes

The Skill examines these sources in order:

1. Design tokens, theme files, and Tailwind configuration
2. Global CSS and CSS custom properties
3. Shared UI components
4. Primary layouts and representative pages
5. Page-specific exceptions

It extracts only decisions supported by project evidence. Installed dependencies, build output, caches, generated code, test snapshots, secrets, and environment files are excluded.

## Install

### Ask your coding agent (recommended)

Ask a coding agent that supports Agent Skills:

```text
Install the extract-design-md Agent Skill from:
https://github.com/trycatch98/extract-design-md/tree/main/skills/extract-design-md
```

### Skills CLI

Use the [`skills` CLI](https://github.com/vercel-labs/skills) when you want to choose a supported coding agent and installation scope yourself:

```bash
npx skills add https://github.com/trycatch98/extract-design-md/tree/main/skills/extract-design-md
```

This command resolves the current Skills CLI release. At the time of this README update, Skills CLI `1.5.21` requires Node.js `22.20` or later and npm. Check its current [package requirements](https://github.com/vercel-labs/skills/blob/main/package.json) if the command reports a Node.js version error.

## Use

Invoke the Skill explicitly:

```text
Use $extract-design-md to analyze this frontend project and create DESIGN.md.
```

Provide a matching URL when runtime verification would help:

```text
Use $extract-design-md to analyze this frontend project and create DESIGN.md. Verify it against http://localhost:3000.
```

By default, the result is created at the target project root. If a `DESIGN.md` already exists, the Skill proposes a reviewed update instead of replacing it immediately.

## Example output

An abbreviated result looks like this:

```markdown
---
name: Acme Dashboard
description: A focused operations interface
colors:
  primary: "#2457D6"
  surface: "#FFFFFF"
typography:
  body:
    fontFamily: Inter
    fontSize: 1rem
spacing:
  md: 16px
rounded:
  control: 8px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    rounded: "{rounded.control}"
    padding: "{spacing.md}"
---

## Overview

Use a compact, information-first layout with clear visual hierarchy.

## Colors

Primary blue identifies actions and selected states. White is the main content surface.

## Components

Primary buttons use the primary color, medium spacing, and the shared control radius.
```

The actual document includes only rules supported by the target project. It may contain additional official or evidence-backed sections when they apply.

## Compatibility and versioning

| Target | Pinned value |
|---|---|
| Specification tag | `0.4.0` |
| Specification commit | `9bf8eae` |
| Validator | `@google/design.md@0.4.0` |

A newer specification release is not adopted automatically. The bundled specification and Skill must be reviewed and updated together.

The source-analysis approach was adapted from [Google Labs Code's `extract-design-md` Agent Skill](https://github.com/google-labs-code/stitch-skills/tree/main/plugins/stitch-design/skills/extract-design-md). This implementation generates and validates the pinned Google Labs DESIGN.md `0.4.0` format.

## License and attribution

The project is licensed under the Apache License 2.0. The Skill bundles a snapshot of Google's `DESIGN.md` format specification from tag `0.4.0`, commit `9bf8eae`, under the same license. A metadata and attribution header was added to the bundled file; the specification body is otherwise unchanged. See [`NOTICE`](NOTICE) for attribution.

Questions and bug reports are welcome in [GitHub Issues](https://github.com/trycatch98/extract-design-md/issues).
