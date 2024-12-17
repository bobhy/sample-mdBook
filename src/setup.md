# Setup and Configuration

## `Cargo.toml`

Dependencies section must reference the crates (by version and feature) that you which to use in code samples and doc tests.

```toml

[dependencies]
serde = { version = "1.0.216", features = ["derive"] }
anyhow = "1.0.94"
serde_json = "1.0.133"
```

## `book.toml`

`[rust]` section must include `manifest = path/to/Cargo.toml`

```toml
[rust]
# path is relative to `book.toml`
manifest = "./Cargo.toml"

```

## Code samples

Must `use <crate>` as they would in open Rust code.

```text
```rust,editable
use serde::{Serialize, Deserialize};

#[derive(Serialize, Deserialize, Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32,
}
```

