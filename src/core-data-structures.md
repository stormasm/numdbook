
### StateWorkingSet

The *StateWorkingSet* is a way to get more information into the permanent state
or EngineState.

The EngineState is the permanent state and when you want to add more stuff to
the EngineState you first put the information into the StateWorkingSet and
then if you choose later you can merge the StateWorkingSet into the EngineState
via the EngineState method *merge_delta*.

```rust
StateWorkingSet::new(engine_state);
```

The above initializer for *StateWorkingSet* is used all over the place
and a great place to start to understand what this data structure does.
