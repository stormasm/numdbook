
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

    /// An error value that represents an error that occurred
    /// as the values in the pipeline were built
    Error(ShellError),

    /// A block of Nu code, eg `{ ls | get name ; echo "done" }`
    Block(hir::Block),
}


pub struct Value {
	pub value: UntaggedValue,
	pub tag: Tag,
}
```

##### type_shape.rs

```rust

/// Representation of the type of a value in Nu

pub enum Type {
    /// A value which has no value
    Nothing,
    /// An integer-based value
    Int,
    /// A range between two values
    Range(Box<RangeType>),
    /// A decimal (floating point) value
    Decimal,
    /// A filesize in bytes
    Filesize,
    /// A string of text
    String,
    /// A line of text (a string with trailing line ending)
    Line,
    /// A path through a table
    ColumnPath,
    /// A glob pattern (like foo*)
    Pattern,
    /// A boolean value
    Boolean,
    /// A date value (in UTC)
    Date,
    /// A data duration value
    Duration,
    /// A filepath value
    Path,
    /// A binary (non-text) buffer value
    Binary,

    /// A row of data
    Row(Row),
    /// A full table of data
    Table(Vec<Type>),

    /// A block of script (TODO)
    Block,
    /// An error value (TODO)
    Error,

    /// Beginning of stream marker (used as bookend markers rather than actual values)
    BeginningOfStream,
    /// End of stream marker (used as bookend markers rather than actual values)
    EndOfStream,
}
```

##### evaluate.rs

An evaluation scope. Scopes map variable names to Values and aid in evaluating blocks and expressions.
Additionally, holds the value for the special $it variable, a variable used to refer to the value passing
through the pipeline at that moment

```rust
pub struct Scope {
    vars: IndexMap<String, Value>,
    env: IndexMap<String, String>,
    parent: Option<Arc<Scope>>,
}
```

##### hir.rs

```rust
pub struct InternalCommand {
    pub name: String,
    pub name_span: Span,
    pub args: crate::hir::Call,
}

pub struct ClassifiedBlock {
    pub block: Block,
    // this is not a Result to make it crystal clear that these shapes
    // aren't intended to be used directly with `?`
    pub failed: Option<ParseError>,
}

pub struct ClassifiedPipeline {
    pub commands: Commands,
}

pub struct Commands {
    pub list: Vec<ClassifiedCommand>,
    pub span: Span,
}

pub struct Block {
    pub block: Vec<Commands>,
    pub span: Span,
}

pub struct SpannedExpression {
    pub expr: Expression,
    pub span: Span,
}

pub struct Call {
    pub head: Box<SpannedExpression>,
    pub positional: Option<Vec<SpannedExpression>>,
    pub named: Option<NamedArguments>,
    pub span: Span,
    pub external_redirection: ExternalRedirection,
}

pub struct NamedArguments {
    pub named: IndexMap<String, NamedValue>,
}

pub struct ExternalArgs {
    pub list: Vec<SpannedExpression>,
    pub span: Span,
}

pub struct ExternalCommand {
    pub name: String,
    pub name_tag: Tag,
    pub args: ExternalArgs,
}

pub struct ExternalStringCommand {
    pub name: Spanned<String>,
    pub args: Vec<Spanned<String>>,
}

pub struct Binary {
    pub left: SpannedExpression,
    pub op: SpannedExpression,
    pub right: SpannedExpression,
}

pub struct Range {
    pub left: Option<SpannedExpression>,
    pub operator: Spanned<RangeOperator>,
    pub right: Option<SpannedExpression>,
}

pub struct SpannedLiteral {
    pub literal: Literal,
    pub span: Span,
}

pub struct Path {
    pub head: SpannedExpression,
    pub tail: Vec<PathMember>,
}

pub struct Flag {
    pub(crate) kind: FlagKind,
    pub(crate) name: Span,
}

pub enum ClassifiedCommand {
    Expr(Box<SpannedExpression>),
    #[allow(unused)]
    Dynamic(crate::hir::Call),
    Internal(InternalCommand),
    Error(ParseError),
}

pub enum Expression {
    Literal(Literal),
    ExternalWord,
    Synthetic(Synthetic),
    Variable(Variable),
    Binary(Box<Binary>),
    Range(Box<Range>),
    Block(hir::Block),
    List(Vec<SpannedExpression>),
    Table(Vec<SpannedExpression>, Vec<Vec<SpannedExpression>>),
    Path(Box<Path>),

    FilePath(PathBuf),
    ExternalCommand(ExternalStringCommand),
    Command,
    Invocation(hir::Block),

    Boolean(bool),
    Garbage,
}
```
