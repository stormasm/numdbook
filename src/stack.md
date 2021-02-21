# Nushell Stack

## Crates

This shows the dependency hierarchy for nushell.

#### Bottom to Top

| Crate         |      Dependencies                 |
|---------------|-----------------------------------|
| nu-parser     |     nu-test-support               |
| nu-protocol   |     nu-errors                     |
| nu-errors     |     nu-source                     |
| nu-source     |     None                          |
| nu-table      |     None                          |

Dependencies include all dependencies below it...

#### Top to Bottom

| Crate         |     Dependencies                  |
|---------------|-----------------------------------|
| nu-table      |     None                          |
| nu-source     |     None                          |
| nu-errors     |     nu-source                     |
| nu-protocol   |     nu-errors                     |
| nu-parser     |     nu-test-support               |

Dependencies include all dependencies above it...

### nu-value-ext depends on...

```rust
nu-errors = { path = "../nu-errors", version = "0.27.1" }
nu-protocol = { path = "../nu-protocol", version = "0.27.1" }
nu-source = { path = "../nu-source", version = "0.27.1" }
```

### nu-parser depends on...

```rust
nu-errors = { version = "0.27.1", path = "../nu-errors" }
nu-protocol = { version = "0.27.1", path = "../nu-protocol" }
nu-source = { version = "0.27.1", path = "../nu-source" }
nu-test-support = { version = "0.27.1", path = "../nu-test-support" }
```

### nu-data depends on...

```rust
nu-errors = { version = "0.27.1", path = "../nu-errors" }
nu-protocol = { version = "0.27.1", path = "../nu-protocol" }
nu-source = { version = "0.27.1", path = "../nu-source" }
nu-table = { version = "0.27.1", path = "../nu-table" }
nu-test-support = { version = "0.27.1", path = "../nu-test-support" }
nu-value-ext = { version = "0.27.1", path = "../nu-value-ext" }
```

### nu-engine depends on...

```rust
nu-data = { version = "0.27.1", path = "../nu-data" }
nu-errors = { version = "0.27.1", path = "../nu-errors" }
nu-parser = { version = "0.27.1", path = "../nu-parser" }
nu-plugin = { version = "0.27.1", path = "../nu-plugin" }
nu-protocol = { version = "0.27.1", path = "../nu-protocol" }
nu-source = { version = "0.27.1", path = "../nu-source" }
nu-stream = { version = "0.27.1", path = "../nu-stream" }
nu-value-ext = { version = "0.27.1", path = "../nu-value-ext" }
```
