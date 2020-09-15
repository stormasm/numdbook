# Nushell Stack

## Crates

This shows the dependency hierarchy for nushell.

| Crate         |      Dependencies                 |
|---------------|-----------------------------------|
| nu-source     |     None                          |
| nu-errors     | nu-source                         |
| nu-protocol   | nu-source, nu-errors              |
| nu-parser     | nu-source, nu-errors, nu-protocol |

## Add in more info later...
