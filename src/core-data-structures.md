
### nu-protocol

##### value.rs

```rust
pub enum UntaggedValue {
    /// A primitive (or fundamental) type of values
    Primitive(Primitive),

    /// A table row
    Row(Dictionary),

    /// A full inner (or embedded) table
    Table(Vec<Value>),

    /// An error value that represents an error that occurred as the values in the pipeline were built
    Error(ShellError),

    /// A block of Nu code, eg `{ ls | get name ; echo "done" }`
    Block(hir::Block),
}


pub struct Value {
	pub value: UntaggedValue,
	pub tag: Tag,
}
```

### nu-source

##### meta.rs

```rust

/// A Span is metadata which indicates the start and end positions.
/// Spans are combined with AnchorLocations
/// to form another type of metadata, a Tag

pub struct Span {
	start: usize,
	end: usize,
}

pub struct Tag {
    /// The original source for this value
    pub anchor: Option<AnchorLocation>,
    /// The span in the source text for the command that created this value
    pub span: Span,
}

/// A wrapper type that attaches a Span to a value
pub struct Spanned<T> {
    pub span: Span,
    pub item: T,
}

/// A wrapper type that attaches a Tag to a value
pub struct Tagged<T> {
    pub tag: Tag,
    pub item: T,
}

/// Anchors represent a location that a value originated from.
/// The value may have been loaded from a file,
/// fetched from a website, or parsed from some text

pub enum AnchorLocation {
    /// The originating site where the value was first found
    Url(String),
    /// The original file where the value was loaded from
    File(String),
    /// The text where the value was parsed from
    Source(Text),
}
```

##### text.rs

```rust
/// A "Text" is like a string except that it can be cheaply cloned.
/// You can also "extract" subtexts quite cheaply. You can also deref
/// an `&Text` into a `&str` for interoperability.
///
/// Used to represent the value of an input file.
pub struct Text {
    text: Arc<String>,
    start: usize,
    end: usize,
}
```
