
### Notes on eval.rs

Only 3 methods return

```rust
Result<Value, ShellError>
```

* eval_expression
* eval_variable
* compute

### Random notes

see *make_engine_state* in the nu-cmd-extra crate for a nice simple picture
of *EngineState* and *StateWorkingSet*
