# Milestone Delivery :mailbox:

**The delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/Support%20Docs/milestone-deliverables-guidelines.md).**

* **Application Document:** [ink! Analyzer (Phase 2)](https://github.com/w3f/Grants-Program/blob/master/applications/ink-analyzer-phase-2.md)
* **Milestone Number:** 5

**Context** (optional)

This delivery is for the [LSP (Language Server Protocol) implementation](https://github.com/ink-analyzer/ink-analyzer/tree/master/crates/lsp-server) of [semantic analyzer](https://github.com/ink-analyzer/ink-analyzer/tree/master/crates/analyzer) features that were delivered and evaluated in milestones 1 ([PR](https://github.com/w3f/Grant-Milestone-Delivery/pull/1004), [delivery](https://github.com/w3f/Grant-Milestone-Delivery/blob/master/deliveries/ink-analyzer-phase-2-milestone-1.md) and [evaluation](https://github.com/w3f/Grant-Milestone-Delivery/blob/master/evaluations/ink-analyzer-phase-2_1_dsm-w3f.md)) and 2 ([PR](https://github.com/w3f/Grant-Milestone-Delivery/pull/1025), [delivery](https://github.com/w3f/Grant-Milestone-Delivery/blob/master/deliveries/ink-analyzer-phase-2-milestone-2.md) and [evaluation](https://github.com/w3f/Grant-Milestone-Delivery/blob/master/evaluations/ink-analyzer-phase-2_m_2_nikw3f.md)).

**NOTE:** While milestones 3 and 4 (for the semantic analyzer) are still in development, this language server deliverable (milestone 5) only relies on semantic analyzer features that were already delivered in milestones 1 and 2.

Please see the [README](https://github.com/ink-analyzer/ink-analyzer#readme) for additional architectural details.

**Deliverables**

| Number  | Deliverable                                                                                                             | Link                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------|-------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **0a.** | License                                                                                                                 | [MIT](https://github.com/ink-analyzer/ink-analyzer/blob/master/LICENSE-MIT) or [Apache 2.0](https://github.com/ink-analyzer/ink-analyzer/blob/master/LICENSE-APACHE).                                                                                                                                                                                                                                                                                               | Dual-licensed under either of MIT or Apache 2.0 licenses at the downstream user's option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **0b.** | Documentation                                                                                                           | [Project README](https://github.com/ink-analyzer/ink-analyzer#readme), [language server (ink-lsp-server) crate README](https://github.com/ink-analyzer/ink-analyzer/tree/master/crates/lsp-server#readme) on GitHub (and [crates.io](https://crates.io/crates/ink-lsp-server)), [language server (ink-lsp-server) crate rustdoc](https://docs.rs/ink-lsp-server/latest/ink_lsp_server/) library documentation on docs.rs and extensive inline source documentation. | The language server's README is published on both [GitHub](https://github.com/ink-analyzer/ink-analyzer/tree/master/crates/lsp-server#readme) and [crates.io](https://crates.io/crates/ink-lsp-server). It contains instructions for installation and usage, and links to crate's associated library documentation on docs.rs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| **0c.** | Testing and Testing Guide                                                                                               | [Testing guide](https://github.com/ink-analyzer/ink-analyzer#testing).                                                                                                                                                                                                                                                                                                                                                                                              | Unit tests are defined in the [dispatch/handlers/request](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/dispatch/handlers/request.rs#L286-L542) module, while integration tests are found in the [tests directory of the language server (ink-lsp-server) crate](https://github.com/ink-analyzer/ink-analyzer/tree/master/crates/lsp-server/tests) (e.g. [tests/inlay_hints](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/tests/inlay_hints.rs), [tests/signature_help](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/tests/signature_help.rs), [tests/commands](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/tests/commands.rs) e.t.c) with related fixtures (where applicable) found in [test-utils/fixtures](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/test-utils/src/fixtures.rs). Checking out the [parse_offset_at](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/test-utils/src/lib.rs#L55-L86) utility may be useful as it is extensively used in both the unit and integration tests. All features in this milestone can also be manually tested using the latest version of the [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=ink-analyzer.ink-analyzer). For instructions for manual feature testing, please refer to the [VS Code extension's "Manual Feature Testing Guide"](https://github.com/ink-analyzer/ink-vscode/blob/master/TESTING.md). |
| **0d.** | Docker                                                                                                                  | [Dockerfile](https://github.com/ink-analyzer/ink-analyzer/blob/master/Dockerfile).                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 1.      | Language Server: Rust binary crate: ink! Language Server updates for semantic analyzer features from milestones 1 and 2 | [GitHub repository](https://github.com/ink-analyzer/ink-analyzer), [Language server crate (ink-lsp-server)](https://crates.io/crates/ink-lsp-server).                                                                                                                                                                                                                                                                                                               | At the highest level, features are implemented as dispatch actions (e.g. [diagnostics](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/dispatch/actions.rs)) or request handlers (e.g. [code actions, completions, inlay hints, signature help, commands e.t.c](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/dispatch/handlers/request.rs)) under the [dispatch](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/dispatch.rs) module, which implements the main loop for dispatching LSP requests and notifications and handling responses. Server initialization logic and setting/negotiating of capabilities is implemented in the [initialize](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/initialize.rs) module, while translation between analyzer and LSP types is implemented in the [translator](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/translator.rs) module. NOTE: Quickfixes are returned by the [code actions handler](https://github.com/ink-analyzer/ink-analyzer/blob/master/crates/lsp-server/src/dispatch/handlers/request.rs#L99-L135) as they're a [code action kind](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#codeActionKind) in LSP.                                                                                                                                                                  |

**Additional Information**

Please use the [lsp-server-v0.2.12](https://github.com/ink-analyzer/ink-analyzer/releases/tag/lsp-server-v0.2.12) tag for testing.

You can checkout the tag locally as follows:
```shell
git fetch --all --tags
git checkout tags/lsp-server-v0.2.12 -b lsp-server-v0.2.12
```