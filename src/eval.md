
what does the parser produce that is used downstream in the current nushell system.

quite simply the answer is the *block*.

to see this elucidated in more detail check out
[eval_cmds.rs](https://github.com/nushell/nushell/blob/main/crates/nu-cli/src/eval_cmds.rs)

---

see *quickcheck_parse* for a much bigger picture :)

#### nu-cli/src/util.rs

* *eval_source* is called in *nu-cli/src/repl.rs*

#### nu-engine/src/eval.rs

*eval_block* and then *eval_call* are the top level calls to see everything that is going on.

Only 3 methods return

```rust
Result<Value, ShellError>
```

* eval_expression
* eval_variable
* compute

### Expression

### Stack


### Random notes

see *make_engine_state* in the nu-cmd-extra crate for a nice simple picture
of *EngineState* and *StateWorkingSet*
