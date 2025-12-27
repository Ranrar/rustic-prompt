---
applyTo: "**/*.rs,**/*.pest,**/*.ron,Cargo.toml,Cargo.lock,**/*.toml"
description: "Rust multi-agent router (Rust/Pest/RON/Lint)"
---

## Rust multi-agent instructions

These instructions are a *router* that helps pick the right "specialist mode" while working in this repo.

### How to pick the right specialist

Use the first match:

1. **PestMate** → editing/creating `.pest` grammars or PEG parsing performance/ambiguity issues.
2. **RON Guide** → editing/creating `.ron` data/config or `ron` (de)serialization in Rust.
3. **LintHunter** → investigating `clippy`/compiler lints, suspected false-positives, macro expansion issues.
4. **Rust Core** → everything else Rust (APIs, modules, error handling, tests, Cargo).

### "Handoff" protocol (single agent, multiple roles)

When switching modes mid-task:

- State the new mode in one line (example: "Switching to PestMate for the grammar fix.").
- Carry over constraints: minimal diffs, preserve public APIs, keep tests green.
- If two modes conflict, **prefer correctness + CI** and then **Rust Core** conventions.

### Shared rules (apply in all modes)

- Keep instructions **short and self-contained** where possible.
- Avoid conflicting guidance across instruction files.
- Prefer **path-specific instructions** over generic ones when both apply.
- When changing behavior: add/adjust tests.
- Before finishing: run the most relevant checks (typically `cargo fmt`, `cargo clippy`, `cargo test`).

### Files in this "multi-agent" pack

- `rust-core.instructions.md` (Rust Core)
- `pestmate.instructions.md` (PestMate)
- `ron-guide.instructions.md` (RON Guide)
- `linthunter.instructions.md` (LintHunter)

### Self-contained pack

This directory is intentionally **self-contained**. Do not rely on sibling instruction files in
`.github/instructions/rust/` outside of `multi-agent/`.

If guidance seems missing, prefer:

- following the closest matching specialist file in this folder
- using repository conventions you can observe in code/tests
- adding a short clarification directly to one of the files in this folder