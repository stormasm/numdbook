
### nu-protocol/src/value.rs

```rust
/// The fundamental structured value that flows through the pipeline, with associated metadata
#[derive(Debug, Clone, PartialOrd, Ord, Eq, Serialize, Deserialize)]
pub struct Value {
    pub value: UntaggedValue,
    pub tag: Tag,
}

/// The core structured values that flow through a pipeline
#[derive(Debug, Clone, PartialEq, PartialOrd, Eq, Ord, Hash, Serialize, Deserialize)]
pub enum UntaggedValue {
    /// A primitive (or fundamental) type of values
    Primitive(Primitive),

    /// A table row
    Row(Dictionary),

    /// A full inner (or embedded) table
    Table(Vec<Value>),

    /// An error value that represents an error that occurred as the values in the pipeline were built
    Error(ShellError),

    /// A block of Nu code, eg `{ ls | get name ; echo "done" }` with its captured values
    Block(Box<hir::CapturedBlock>),
}
```

### nu-source/src/meta.rs

```rust
pub struct Tag {
    /// The original source for this value
    pub anchor: Option<AnchorLocation>,
    /// The span in the source text for the command that created this value
    pub span: Span,
}

/// Anchors represent a location that a value originated from. The value may have been loaded from a file, fetched from a website, or parsed from some text
#[derive(Clone, Debug, Serialize, Deserialize, PartialEq, Eq, PartialOrd, Ord, Hash)]
pub enum AnchorLocation {
    /// The originating site where the value was first found
    Url(String),
    /// The original file where the value was loaded from
    File(String),
    /// The text where the value was parsed from
    Source(Text),
}

/// A `Span` is metadata which indicates the start and end positions.
/// `Span`s are combined with `AnchorLocation`s to form another type of metadata, a `Tag`.
/// A `Span`'s end position must be greater than or equal to its start position.
#[derive(Debug, Default, Clone, Copy, PartialEq, Eq, Ord, PartialOrd,Serialize, Deserialize, Hash,)]
pub struct Span {
    start: usize,
    end: usize,
}
```
