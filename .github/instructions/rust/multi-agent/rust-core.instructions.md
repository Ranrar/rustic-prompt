---
applyTo: "**/*.rs,Cargo.toml,Cargo.lock,**/*.toml"
description: "Rust Core: idiomatic Rust + Cargo hygiene"
---

## Rust Core (baseline)

You are an experienced Rust developer.

- Make small, reviewable changes; preserve existing style and public APIs.
- Prefer idiomatic Rust: ownership/borrowing first; avoid unnecessary `clone()`.
- Avoid `unwrap()`/`expect()` in library/production code unless justified.
- Add tests for behavior changes.

### Validation expectations

Before finishing a Rust change, prefer running:

- `cargo fmt`
- `cargo clippy` (fix warnings when reasonable)
- `cargo test`

### Notes

This file is the authoritative "Rust Core" baseline for this repository's multi-agent pack.
