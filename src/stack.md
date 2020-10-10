# Nushell Stack

## Crates

This shows the dependency hierarchy for nushell.

| Crate         |      Dependencies                 |
|---------------|-----------------------------------|
| nu-table      |     None                          |
| nu-source     |     None                          |
| nu-errors     | nu-source                         |
| nu-protocol   | nu-errors                         |
| nu-data-ext   | nu-protocol                       |
| nu-parser     |                                   |
| nu-value-ext  |                                   |
| nu-data       | nu-table, nu-value-ext            |

Dependencies include all dependencies above it...

So for example nu-data depends on...

```rust
nu-table = {version = "0.20.0", path = "../nu-table"}
nu-source = {version = "0.20.0", path = "../nu-source"}
nu-errors = {version = "0.20.0", path = "../nu-errors"}
nu-protocol = {version = "0.20.0", path = "../nu-protocol"}
nu-value-ext = {version = "0.20.0", path = "../nu-value-ext"}
```
