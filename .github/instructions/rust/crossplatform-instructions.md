---
applyTo: "**/*.rs,Cargo.toml"
description: "Cross-platform Rust (conditional compilation)"
---

You are an experienced Rust developer.

## Cross-platform Rust (conditional compilation)

When generating Rust code that targets multiple operating systems (Windows, Linux, macOS), use Rust's conditional compilation (`#[cfg]`, `cfg!`, `cfg_attr`) correctly for imports, functions, modules, platform-specific dependencies, and build scripts.

**Goal**: Code should compile cleanly (no warnings/errors) on all supported targets.

## Core principles

### 1. Understand `#[cfg]` vs `cfg!`

- **`#[cfg(...)]`** - Compile-time inclusion/exclusion. Code is completely removed if condition is false.
- **`cfg!(...)`** - Runtime boolean macro. Does NOT remove code from type checking.
  - **Warning**: Using `cfg!()` with platform-specific APIs can cause compile failures on other platforms.

```rust
// CORRECT: Code removed on non-Windows targets
#[cfg(target_os = "windows")]
fn windows_only() {
    use std::os::windows::fs::MetadataExt; // Only compiled on Windows
}

// WRONG: Code still type-checked on all platforms
fn may_fail() {
    if cfg!(target_os = "windows") {
        use std::os::windows::fs::MetadataExt; // Error on Linux/macOS!
        // ...
    }
}
```

### 2. Scope imports to their `#[cfg]` blocks

Move platform-specific imports inside the conditional blocks where they're used. This prevents `unused_imports` warnings and keeps dependencies minimal.

```rust
// CORRECT: Import scoped to cfg block
#[cfg(target_os = "windows")]
{
    use winapi::um::winbase::GetUserNameW;
    // use GetUserNameW...
}

// WRONG: Import always present, causes warnings
use winapi::um::winbase::GetUserNameW;

#[cfg(target_os = "windows")]
fn get_username() {
    // use GetUserNameW...
}
```

### 3. Use descriptive predicates

Combine conditions using `any()`, `all()`, and `not()` for clarity:

```rust
// Target specific architectures
#[cfg(target_arch = "x86_64")]
#[cfg(target_arch = "aarch64")]

// Pointer width
#[cfg(target_pointer_width = "64")]

// OS families
#[cfg(unix)]                    // Linux, macOS, BSD, etc.
#[cfg(windows)]                 // All Windows variants
#[cfg(target_family = "unix")]  // Explicit family

// Specific OS
#[cfg(target_os = "linux")]
#[cfg(target_os = "macos")]
#[cfg(target_os = "windows")]

// Build environment
#[cfg(target_env = "msvc")]     // MSVC toolchain
#[cfg(target_env = "gnu")]      // GNU toolchain

// Combined conditions
#[cfg(all(unix, target_arch = "x86_64"))]
#[cfg(any(target_os = "linux", target_os = "freebsd"))]
#[cfg(not(target_os = "windows"))]
```

### 4. Organize platform modules cleanly

Isolate platform code into separate modules with a unified interface:

```rust
// Recommended structure
#[cfg(target_os = "windows")]
mod platform {
    pub fn get_home_dir() -> String {
        std::env::var("USERPROFILE").unwrap_or_default()
    }
}

#[cfg(not(target_os = "windows"))]
mod platform {
    pub fn get_home_dir() -> String {
        std::env::var("HOME").unwrap_or_default()
    }
}

pub use platform::*;
```

## Common mistakes and solutions

### Mistake 1: Using `#[allow(unused_imports)]` instead of proper cfg

```rust
// BAD: Suppressing warnings
#[allow(unused_imports)]
use std::os::windows::process::CommandExt;
#[allow(unused_imports)]
use std::os::unix::process::CommandExt;

#[cfg(windows)]
fn configure_command(cmd: &mut Command) {
    cmd.creation_flags(0x08000000);
}
```

```rust
// GOOD: Imports scoped correctly
#[cfg(windows)]
fn configure_command(cmd: &mut Command) {
    use std::os::windows::process::CommandExt;
    cmd.creation_flags(0x08000000);
}

#[cfg(unix)]
fn configure_command(cmd: &mut Command) {
    use std::os::unix::process::CommandExt;
    cmd.uid(1000);
}
```

### Mistake 2: Mixing `cfg!()` with platform-specific types

```rust
// BAD: Fails type-checking on non-Windows
fn process_info() {
    if cfg!(windows) {
        use std::os::windows::process::CommandExt; // Type error on Unix!
        // ...
    }
}
```

```rust
// GOOD: Use #[cfg] for platform-specific APIs
#[cfg(windows)]
fn process_info() {
    use std::os::windows::process::CommandExt;
    // ...
}

#[cfg(not(windows))]
fn process_info() {
    // Unix implementation
}
```

### Mistake 3: Over-specific targets

```rust
// BAD: Overly specific, excludes other Unix systems
#[cfg(target_os = "linux")]
fn open_terminal() { /* ... */ }
```

```rust
// GOOD: Use family when appropriate
#[cfg(unix)]
fn open_terminal() { /* Works on Linux, macOS, BSD, etc. */ }
```

### Mistake 4: Feature flags in target dependencies

Cargo does NOT support `cfg(feature = "...")` in `[target.'cfg(...)'.dependencies]`.

```toml
# BAD: Does not work
[target.'cfg(feature = "gui")'.dependencies]
gtk = "0.18"
```

```toml
# GOOD: Use [features] instead
[dependencies]
gtk = { version = "0.18", optional = true }

[features]
gui = ["gtk"]
```

## Code examples

### Example 1: Platform-specific config paths

```rust
use std::path::PathBuf;

pub fn config_dir() -> PathBuf {
    #[cfg(target_os = "windows")]
    {
        use std::env;
        return env::var_os("APPDATA")
            .map(PathBuf::from)
            .unwrap_or_else(|| PathBuf::from("."));
    }

    #[cfg(target_os = "macos")]
    {
        use std::env;
        return env::var_os("HOME")
            .map(|h| PathBuf::from(h).join("Library/Application Support"))
            .unwrap_or_else(|| PathBuf::from("."));
    }

    #[cfg(all(unix, not(target_os = "macos")))]
    {
        use std::env;
        
        if let Some(xdg) = env::var_os("XDG_CONFIG_HOME") {
            return PathBuf::from(xdg);
        }

        return env::var_os("HOME")
            .map(|h| PathBuf::from(h).join(".config"))
            .unwrap_or_else(|| PathBuf::from("."));
    }

    #[cfg(not(any(windows, unix)))]
    {
        PathBuf::from(".")
    }
}
```

### Example 2: Conditional imports with shared interface

```rust
// Different imports per platform
#[cfg(unix)]
use std::os::unix::fs::PermissionsExt;

#[cfg(windows)]
use std::os::windows::fs::MetadataExt;

pub struct FileInfo {
    pub size: u64,
    pub readonly: bool,
}

pub fn get_file_info(path: &Path) -> std::io::Result<FileInfo> {
    let metadata = std::fs::metadata(path)?;
    
    #[cfg(unix)]
    {
        Ok(FileInfo {
            size: metadata.len(),
            readonly: metadata.permissions().mode() & 0o200 == 0,
        })
    }
    
    #[cfg(windows)]
    {
        Ok(FileInfo {
            size: metadata.len(),
            readonly: metadata.file_attributes() & 0x1 != 0,
        })
    }
    
    #[cfg(not(any(unix, windows)))]
    {
        Ok(FileInfo {
            size: metadata.len(),
            readonly: metadata.permissions().readonly(),
        })
    }
}
```

### Example 3: Platform-specific module organization

```rust
// lib.rs or main.rs
#[cfg(target_os = "windows")]
#[path = "platform/windows.rs"]
mod platform;

#[cfg(target_os = "macos")]
#[path = "platform/macos.rs"]
mod platform;

#[cfg(target_os = "linux")]
#[path = "platform/linux.rs"]
mod platform;

pub use platform::open_browser;

// platform/windows.rs
pub fn open_browser(url: &str) -> std::io::Result<()> {
    use std::process::Command;
    Command::new("cmd")
        .args(["/C", "start", url])
        .spawn()?;
    Ok(())
}

// platform/macos.rs
pub fn open_browser(url: &str) -> std::io::Result<()> {
    use std::process::Command;
    Command::new("open")
        .arg(url)
        .spawn()?;
    Ok(())
}

// platform/linux.rs
pub fn open_browser(url: &str) -> std::io::Result<()> {
    use std::process::Command;
    Command::new("xdg-open")
        .arg(url)
        .spawn()?;
    Ok(())
}
```

### Example 4: Architecture-specific optimizations

```rust
#[cfg(target_arch = "x86_64")]
fn fast_hash(data: &[u8]) -> u64 {
    use std::arch::x86_64::*;
    // Use SIMD instructions
    // ...
}

#[cfg(not(target_arch = "x86_64"))]
fn fast_hash(data: &[u8]) -> u64 {
    // Portable fallback
    data.iter().fold(0u64, |acc, &b| acc.wrapping_mul(31).wrapping_add(b as u64))
}
```

## Cargo.toml examples

### Example 1: Platform-specific dependencies

```toml
[package]
name = "myapp"
version = "0.1.0"
edition = "2021"

[dependencies]
# Common dependencies for all platforms
serde = "1.0"
tokio = { version = "1.0", features = ["full"] }

# Platform-specific dependencies using cfg syntax
[target.'cfg(windows)'.dependencies]
winapi = { version = "0.3", features = ["winuser", "winbase"] }
windows = "0.51"

[target.'cfg(unix)'.dependencies]
nix = "0.27"
libc = "0.2"

[target.'cfg(target_os = "macos")'.dependencies]
cocoa = "0.25"
core-foundation = "0.9"

[target.'cfg(target_os = "linux")'.dependencies]
libdbus-sys = "0.2"
```

### Example 2: Platform-specific build dependencies

```toml
[build-dependencies]
cc = "1.0"

[target.'cfg(windows)'.build-dependencies]
winres = "0.1"  # Windows resource compiler

[target.'cfg(unix)'.build-dependencies]
pkg-config = "0.3"
```

### Example 3: Combining features with platform targets

```toml
[dependencies]
# Optional GUI support
gtk = { version = "0.18", optional = true }
egui = { version = "0.24", optional = true }

[target.'cfg(unix)'.dependencies]
# Unix-specific GUI dependencies (only when gui feature enabled)
x11 = { version = "2.21", optional = true }

[features]
default = []
gui = ["gtk", "egui"]
gui-x11 = ["gui", "x11"]
```

### Example 4: Explicit target triples

```toml
# Alternative: specify exact target triples
[target.x86_64-pc-windows-msvc.dependencies]
winapi = { version = "0.3", features = ["winuser"] }

[target.x86_64-unknown-linux-gnu.dependencies]
openssl = "0.10"

[target.aarch64-apple-darwin.dependencies]
metal = "0.27"
```

## Advanced patterns

### Pattern 1: Testing across platforms

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_config_dir_exists() {
        let dir = config_dir();
        assert!(dir.is_absolute() || dir == PathBuf::from("."));
    }

    #[test]
    #[cfg(unix)]
    fn test_unix_permissions() {
        use std::os::unix::fs::PermissionsExt;
        // Unix-specific tests
    }

    #[test]
    #[cfg(windows)]
    fn test_windows_attributes() {
        use std::os::windows::fs::MetadataExt;
        // Windows-specific tests
    }
}
```

### Pattern 2: Using `cfg_attr` for conditional derives

```rust
#[derive(Debug, Clone)]
#[cfg_attr(feature = "serde", derive(serde::Serialize, serde::Deserialize))]
#[cfg_attr(windows, derive(Copy))]  // Copy only on Windows
pub struct Config {
    pub value: u32,
}
```

### Pattern 3: Checking platform at compile time

Use this command to see all cfg values for a target:

```bash
# Current platform
rustc --print=cfg

# Specific target
rustc --print=cfg --target=x86_64-pc-windows-msvc
rustc --print=cfg --target=x86_64-unknown-linux-gnu
rustc --print=cfg --target=aarch64-apple-darwin
```

## Quick reference: Common cfg predicates

| Predicate | Description | Example values |
|-----------|-------------|----------------|
| `target_os` | Operating system | `"windows"`, `"linux"`, `"macos"`, `"ios"`, `"android"`, `"freebsd"` |
| `target_family` | OS family | `"unix"`, `"windows"`, `"wasm"` |
| `target_arch` | CPU architecture | `"x86"`, `"x86_64"`, `"arm"`, `"aarch64"`, `"riscv64"` |
| `target_pointer_width` | Pointer size | `"32"`, `"64"` |
| `target_env` | ABI/toolchain | `"gnu"`, `"msvc"`, `"musl"` |
| `target_endian` | Byte order | `"little"`, `"big"` |
| `target_vendor` | Vendor | `"apple"`, `"pc"`, `"unknown"` |
| `unix` | Shorthand | Any Unix-like OS |
| `windows` | Shorthand | Any Windows OS |

## Best practices checklist

- [ ] Platform-specific imports are scoped inside `#[cfg]` blocks
- [ ] Use `#[cfg]` (not `cfg!()`) for platform-specific types/traits
- [ ] Prefer `unix`/`windows` families over specific OS when possible
- [ ] Platform-specific code is isolated in separate modules
- [ ] Public API is consistent across all targets
- [ ] No `#[allow(unused_imports)]` to hide conditional compilation issues
- [ ] Cargo.toml uses `[target.'cfg(...)'.dependencies]` for platform deps
- [ ] Tests cover platform-specific code paths
- [ ] Documentation explains platform differences

## Reference

- Rust Reference: Conditional compilation - https://doc.rust-lang.org/reference/conditional-compilation.html
- Cargo Book: Platform specific dependencies - https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html#platform-specific-dependencies
- Rust Platform Support - https://doc.rust-lang.org/nightly/rustc/platform-support.html