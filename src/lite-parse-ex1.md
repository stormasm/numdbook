## Lite Parse

This is going to talk about the lite parser...

```javascript
DEBUG nu_cli::cli > LiteBlock {
    block: [
        LitePipeline {
            commands: [
                LiteCommand {
                    name: Spanned {
                        span: Span {
                            start: 0,
                            end: 2,
                        },
                        item: "ls",
                    },
                    args: [
                        Spanned {
                            span: Span {
                                start: 3,
                                end: 5,
                            },
                            item: "-a",
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
                            name: "ls",
                            name_span: Span {
                                start: 0,
                                end: 2,
                            },
                            args: Call {
                                head: SpannedExpression {
                                    expr: Command,
                                    span: Span {
                                        start: 0,
                                        end: 2,
                                    },
                                },
                                positional: None,
                                named: Some(
                                    NamedArguments {
                                        named: {
                                            "all": PresentSwitch(
                                                Span {
                                                    start: 3,
                                                    end: 5,
                                                },
                                            ),
                                        },
                                    },
                                ),
                                span: Span {
                                    start: 0,
                                    end: 5,
                                },
                                external_redirection: None,
                            },
                        },
                    ),
                ],
                span: Span {
                    start: 0,
                    end: 5,
                },
            },
        ],
        span: Span {
            start: 0,
            end: 5,
        },
    },
    failed: None,
}
```
