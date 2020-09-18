## Lite Parse Example 2

This is going to talk about the lite parser...

```rust
echo [[name age] ; [bob 13] [sally 20]]   
```

This is an example about table literals.

```javascript

LiteBlock {
    block: [
       LitePipeline {
           commands: [
               LiteCommand {
                   name: Spanned {
                       span: Span {
                           start: 0,
                           end: 4,
                       },
                       item: "echo",
                   },
                   args: [
                       Spanned {
                           span: Span {
                               start: 5,
                               end: 39,
                           },
                           item: "[[name age] ; [bob 13] [sally 20]]",
                       },
                   ],
               },
           ],
       },
   ],
}
DEBUG nu_cli::cli > ClassifiedBlock {
   block: Block {
       block: [
           Commands {
               list: [
                   Internal(
                       InternalCommand {
                           name: "echo",
                           name_span: Span {
                               start: 0,
                               end: 4,
                           },
                           args: Call {
                               head: SpannedExpression {
                                   expr: Command,
                                   span: Span {
                                       start: 0,
                                       end: 4,
                                   },
                               },
                               positional: Some(
                                   [
                                       SpannedExpression {
                                           expr: Table(
                                               [
                                                   SpannedExpression {
                                                       expr: Literal(
                                                           String(
                                                               "name",
                                                           ),
                                                       ),
                                                       span: Span {
                                                           start: 7,
                                                           end: 11,
                                                       },
                                                   },
                                                   SpannedExpression {
                                                       expr: Literal(
                                                           String(
                                                               "age",
                                                           ),
                                                       ),
                                                       span: Span {
                                                           start: 12,
                                                           end: 15,
                                                       },
                                                   },
                                               ],
                                               [
                                                   [
                                                       SpannedExpression {
                                                           expr: Literal(
                                                               String(
                                                                   "bob",
                                                               ),
                                                           ),
                                                           span: Span {
                                                               start: 20,
                                                               end: 23,
                                                           },
                                                       },
                                                       SpannedExpression {
                                                           expr: Literal(
                                                               Number(
                                                                   Int(
                                                                       BigInt {
                                                                           sign: Plus,
                                                                           data: BigUint {
                                                                               data: [
                                                                                   13,
                                                                               ],
                                                                           },
                                                                       },
                                                                   ),
                                                               ),
                                                           ),
                                                           span: Span {
                                                               start: 24,
                                                               end: 26,
                                                           },
                                                       },
                                                   ],
                                                   [
                                                       SpannedExpression {
                                                           expr: Literal(
                                                               String(
                                                                   "sally",
                                                               ),
                                                           ),
                                                           span: Span {
                                                               start: 29,
                                                               end: 34,
                                                           },
                                                       },
                                                       SpannedExpression {
                                                           expr: Literal(
                                                               Number(
                                                                   Int(
                                                                       BigInt {
                                                                           sign: Plus,
                                                                           data: BigUint {
                                                                               data: [
                                                                                   20,
                                                                               ],
                                                                           },
                                                                       },
                                                                   ),
                                                               ),
                                                           ),
                                                           span: Span {
                                                               start: 35,
                                                               end: 37,
                                                           },
                                                       },
                                                   ],
                                               ],
                                           ),
                                           span: Span {
                                               start: 5,
                                               end: 39,
                                           },
                                       },
                                   ],
                               ),
                               named: Some(
                                   NamedArguments {
                                       named: {
                                           "help": AbsentSwitch,
                                       },
                                   },
                               ),
                               span: Span {
                                   start: 0,
                                   end: 39,
                               },
                               external_redirection: None,
                           },
                       },
                   ),
               ],
               span: Span {
                   start: 0,
                   end: 39,
               },
           },
       ],
       span: Span {
           start: 0,
           end: 39,
       },
   },
   failed: None,
}
```
