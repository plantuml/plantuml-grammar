# TextMate grammar

TextMate grammar for the PlantUML language, in the form consumed by
[GitHub Linguist](https://github.com/github-linguist/linguist).

| File | Scope | Role |
| --- | --- | --- |
| `syntaxes/plantuml.yaml-tmLanguage` | `source.wsd` | Grammar for PlantUML code. |
| `syntaxes/codeblock.json` | `markdown.plantuml.codeblock` | Injection grammar: applies `source.wsd` inside `plantuml` fenced blocks of Markdown files. |

## Origin

This is the first import. The two files in `syntaxes/` are **byte-for-byte
identical** to the ones Linguist currently uses, which come from
[qjebbs/vscode-plantuml](https://github.com/qjebbs/vscode-plantuml) at commit
`7bc1758ed73dc269f5721d78c6c6c01f461d7cb0` (MIT, Copyright (c) 2016 jebbs; see
`LICENSE.vscode-plantuml.txt`). Nothing has been changed yet, so switching
Linguist to this repository does not change any color on GitHub.

## Constraints from Linguist

- The scope name `source.wsd` is referenced by `languages.yml` (`tm_scope`) and
  `grammars.yml` in Linguist. Renaming it requires changing Linguist as well.
- Linguist's grammar compiler reads `.json` grammars only from a directory named
  `syntaxes` or `grammars`, hence `textmate/syntaxes/`.
- A given scope must be defined only once in the whole repository: do not add a
  second grammar with the scope `source.wsd` here.

## Development

Work on the grammar (tests, highlighting gallery, prototypes) happens in
[plantuml/language-grammar](https://github.com/plantuml/language-grammar).
