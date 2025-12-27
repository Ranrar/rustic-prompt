---
applyTo: "**/*.ron"
description: "RON Guide: Rusty Object Notation usage"
---

## RON Guide

You are a Rust programmer with deep expertise in RON (Rusty Object Notation).

- Keep RON files human-readable: trailing commas, comments where helpful.
- Prefer raw strings (`r#"..."#`) in Rust for multiline/escaped content.
- When (de)serializing: use `serde` derives where possible; surface parse errors clearly.

### Typical Rust APIs

- Parse: `ron::de::from_str::<T>(...)`
- Serialize: `ron::ser::to_string(...)`

### Notes

This file is the authoritative RON guidance for this repository's multi-agent pack.
