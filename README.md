# plantuml-grammar

The official home of the **syntax definitions of the PlantUML language**, as consumed by code hosts, editors and documentation tools.

## Why this repository exists

PlantUML code is colored in many places, and today none of them gets its syntax definition from PlantUML itself:

- **GitHub** colors `.puml` files (and `plantuml` code blocks in Markdown) with a TextMate grammar declared in [GitHub Linguist](https://github.com/github-linguist/linguist). Linguist does not own that grammar: it vendors it from a third-party VS Code extension, [qjebbs/vscode-plantuml](https://github.com/qjebbs/vscode-plantuml), pinned at a fixed commit.
- **Other tools** (editors, web editors, documentation generators, static site generators) each ship their own definition, or none at all, and these definitions drift apart.

The goal of this repository is to be **the official, maintained source of the PlantUML grammar**: first for GitHub, then for the other tools and platforms that need to highlight or parse PlantUML. One place, owned by the PlantUML project, so that a fix or a new keyword is made once and reaches everybody.

## Layout

One directory per grammar format, so that each consumer can point at exactly what it needs.

| Directory | Format | Consumers |
| --- | --- | --- |
| [`textmate/`](textmate/) | TextMate grammar | GitHub (through Linguist), Visual Studio Code, and every tool that loads TextMate grammars |

Other formats (for example Monarch for Monaco-based editors, tree-sitter, or lexers for documentation tools) can be added as sibling directories when there is a real consumer for them.

## Current status

- `textmate/` currently holds the grammar GitHub uses today, **byte-for-byte identical** to the upstream files from `qjebbs/vscode-plantuml` at commit `7bc1758`, with the upstream MIT license text. Nothing is changed yet, on purpose: switching a consumer to this repository must not alter any color.
- The next step is to make **GitHub Linguist take its PlantUML grammar from this repository** instead of from vscode-plantuml. This is a change of source only, with no visible effect on GitHub.
- Improvements to the grammar come after that, in small steps, each of them reviewed on its own.

Nothing here has been accepted by Linguist yet: until it is, GitHub keeps using the grammar from vscode-plantuml.

## Where the work happens

This repository is the **deliverable**: it contains only what the consumers need, kept small and easy to review.

Development of the grammar (samples, highlighting tests, a gallery that shows the result in the GitHub themes, and prototypes such as a grammar generated from the keywords of PlantUML itself) happens in [plantuml/language-grammar](https://github.com/plantuml/language-grammar). Changes that are ready are brought here.

## Rules for contributors

- **A scope is defined once.** Linguist's grammar compiler reads every grammar file of the repository and refuses duplicates. Do not add a second grammar with the scope `source.wsd`; experiments belong in `language-grammar`.
- **The scope name `source.wsd` is a public contract.** It is referenced by Linguist (`tm_scope` in `languages.yml`, and `grammars.yml`) and by the Markdown injection grammar. Renaming it, for example to `source.plantuml`, requires a coordinated change in every consumer and is a separate decision.
- **Grammar files go in a `syntaxes/` directory.** Linguist reads `.json` grammars only from a directory named `syntaxes` or `grammars`.

## License

This repository is licensed under the [MIT License](LICENSE).

The TextMate grammar derives from [vscode-plantuml](https://github.com/qjebbs/vscode-plantuml), Copyright (c) 2016 jebbs, also under the MIT License (see [`textmate/LICENSE.vscode-plantuml.txt`](textmate/LICENSE.vscode-plantuml.txt)).
