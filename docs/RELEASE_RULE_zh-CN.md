# Tessera Release Rule

[![English][release-en-badge]][release-en-url]

[release-en-badge]: https://img.shields.io/badge/RELEASE%20RULE-English-blue.svg?style=for-the-badge&logo=release
[release-en-url]: RELEASE_RULE.md

## 版本号规则

版本号由三部分组成：`主版本号.次版本号.修订号`，例如 `1.0.0`。

- **主版本号**：roadmap 彻底完成时增加。
- **次版本号**：任何功能更新或者破坏性变更时增加。
- **修订号**：任何 bug 修复或者小的改进时增加。

## 发布流程

必须使用`script/release-package.rs`脚本发布，它会自动处理版本号的更新和打包，生成更新日志并推送。

1. 建议先 dry run 发布脚本，看看是否符合预期，下面是 dry run 的例子:

   ```bash
   tessera on  main [!?⇡] via 🦀 v1.88.0
   ❯ rust-script scripts/release-package.rs -p tessera-ui patch
   📦 Package: tessera-ui
   📄 Path: tessera-ui\Cargo.toml
   🕓 Old version: 0.2.0
   🆕 New version: 0.2.1
   tessera-ui\CHANGELOG.md
   ╭───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
   │ line                                                                                                                  │
   ├───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
   │ --- original                                                                                                          │
   │ +++ modified                                                                                                          │
   │ @@ -0,0 +1,6 @@                                                                                                       │
   │ +## [v0.2.1] - 2025-07-19 +08:00                                                                                      │
   │ +                                                                                                                     │
   │ +### Changes                                                                                                          │
   │ +                                                                                                                     │
   │ +[Compare with previous release](https://github.com/shadow3aaa/tessera/compare/tessera-ui-v0.2.0...tessera-ui-v0.2.1) │
   │ +                                                                                                                     │
   ╰───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
   [dry-run] git add tessera-ui\CHANGELOG.md
   tessera-ui\Cargo.toml
   ╭──────────────────────────────╮
   │ line                         │
   ├──────────────────────────────┤
   │ --- original                 │
   │ +++ modified                 │
   │ @@ -1,7 +1,7 @@              │
   │                              │
   │  [package]                   │
   │  name = "tessera-ui"         │
   │ -version = "0.2.0"           │
   │ +version = "0.2.1"           │
   │  edition.workspace = true    │
   │  license.workspace = true    │
   │  repository.workspace = true │
   ╰──────────────────────────────╯
   [dry-run] git add tessera-ui\Cargo.toml
   [dry-run] git commit -m "release(tessera-ui): v0.2.1"
   [dry-run] git tag tessera-ui-v0.2.1
   [dry-run] git push
   [dry-run] git push --tags
   example\Cargo.toml
   ╭────────────────────────────────────────────────────────────────────────────╮
   │ line                                                                       │
   ├────────────────────────────────────────────────────────────────────────────┤
   │ --- original                                                               │
   │ +++ modified                                                               │
   │ @@ -13,9 +13,9 @@                                                          │
   │  path = "src/lib.rs"                                                       │
   │                                                                            │
   │  [dependencies]                                                            │
   │ -tessera-ui = { path = "../tessera-ui" }                                   │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }                     │
   │ -tessera-ui-basic-components = { path = "../tessera-ui-basic-components" } │
   │ +tessera-ui = { version = "0.2.1" }                                        │
   │ +tessera-ui-macros = { version = "0.1.0" }                                 │
   │ +tessera-ui-basic-components = { version = "0.0.0" }                       │
   │  rand = "0.9.1"                                                            │
   │  tokio = { version = "1.45.1", features = ["full"] }                       │
   │  log = "0.4.27"                                                            │
   ╰────────────────────────────────────────────────────────────────────────────╯
   [dry-run] git add example\Cargo.toml
   tessera-ui-logo\Cargo.toml
   ╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
   │ line                                                                                              │
   ├───────────────────────────────────────────────────────────────────────────────────────────────────┤
   │ --- original                                                                                      │
   │ +++ modified                                                                                      │
   │ @@ -7,9 +7,9 @@                                                                                   │
   │  # See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html │
   │                                                                                                   │
   │  [dependencies]                                                                                   │
   │ -tessera-ui = { path = "../tessera-ui" }                                                          │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }                                            │
   │ -tessera-ui-basic-components = { path = "../tessera-ui-basic-components" }                        │
   │ +tessera-ui = { version = "0.2.1" }                                                               │
   │ +tessera-ui-macros = { version = "0.1.0" }                                                        │
   │ +tessera-ui-basic-components = { version = "0.0.0" }                                              │
   │  rand = "0.9.1"                                                                                   │
   │  rand_pcg = "0.9.0"                                                                               │
   │  tokio = { version = "1.46.1", features = ["full"] }                                              │
   ╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
   [dry-run] git add tessera-ui-logo\Cargo.toml
   tessera-ui-basic-components\Cargo.toml
   ╭────────────────────────────────────────────────────────────────────╮
   │ line                                                               │
   ├────────────────────────────────────────────────────────────────────┤
   │ --- original                                                       │
   │ +++ modified                                                       │
   │ @@ -17,8 +17,8 @@                                                  │
   │  glyphon = { package = "glyphon-tessera-fork", version = "0.9.0" } │
   │  log = "0.4.27"                                                    │
   │  parking_lot = "0.12.4"                                            │
   │ -tessera-ui = { path = "../tessera-ui" }                           │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }             │
   │ +tessera-ui = { version = "0.2.1" }                                │
   │ +tessera-ui-macros = { version = "0.1.0" }                         │
   │  unicode-segmentation = "1.12.0"                                   │
   │  encase = { version = "0.11.1", features = ["glam"] }              │
   │  glam = "0.30.4"                                                   │
   ╰────────────────────────────────────────────────────────────────────╯
   [dry-run] git add tessera-ui-basic-components\Cargo.toml
   tessera-ui-macros\Cargo.toml
   ╭──────────────────────────────────────────╮
   │ line                                     │
   ├──────────────────────────────────────────┤
   │ --- original                             │
   │ +++ modified                             │
   │ @@ -13,4 +13,4 @@                        │
   │  [dependencies]                          │
   │  quote = "1.0.40"                        │
   │  syn = "2.0.101"                         │
   │ -tessera-ui = { path = "../tessera-ui" } │
   │ +tessera-ui = { version = "0.2.1" }      │
   ╰──────────────────────────────────────────╯
   [dry-run] git add tessera-ui-macros\Cargo.toml
   [dry-run] git commit -m "chore: replace path dependencies with version for publish"
   [dry-run] cargo publish -p tessera-ui
   [dry-run] git reset --hard tessera-ui-v0.2.1
   example\Cargo.toml
   ╭────────────────────────────────────────────────────────────────────────────╮
   │ line                                                                       │
   ├────────────────────────────────────────────────────────────────────────────┤
   │ --- original                                                               │
   │ +++ modified                                                               │
   │ @@ -13,9 +13,9 @@                                                          │
   │  path = "src/lib.rs"                                                       │
   │                                                                            │
   │  [dependencies]                                                            │
   │ -tessera-ui = { path = "../tessera-ui" }                                   │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }                     │
   │ -tessera-ui-basic-components = { path = "../tessera-ui-basic-components" } │
   │ +tessera-ui = { version = "0.2.1" }                                        │
   │ +tessera-ui-macros = { version = "0.1.0" }                                 │
   │ +tessera-ui-basic-components = { version = "0.0.0" }                       │
   │  rand = "0.9.1"                                                            │
   │  tokio = { version = "1.45.1", features = ["full"] }                       │
   │  log = "0.4.27"                                                            │
   ╰────────────────────────────────────────────────────────────────────────────╯
   tessera-ui-logo\Cargo.toml
   ╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
   │ line                                                                                              │
   ├───────────────────────────────────────────────────────────────────────────────────────────────────┤
   │ --- original                                                                                      │
   │ +++ modified                                                                                      │
   │ @@ -7,9 +7,9 @@                                                                                   │
   │  # See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html │
   │                                                                                                   │
   │  [dependencies]                                                                                   │
   │ -tessera-ui = { path = "../tessera-ui" }                                                          │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }                                            │
   │ -tessera-ui-basic-components = { path = "../tessera-ui-basic-components" }                        │
   │ +tessera-ui = { version = "0.2.1" }                                                               │
   │ +tessera-ui-macros = { version = "0.1.0" }                                                        │
   │ +tessera-ui-basic-components = { version = "0.0.0" }                                              │
   │  rand = "0.9.1"                                                                                   │
   │  rand_pcg = "0.9.0"                                                                               │
   │  tokio = { version = "1.46.1", features = ["full"] }                                              │
   ╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
   tessera-ui-basic-components\Cargo.toml
   ╭────────────────────────────────────────────────────────────────────╮
   │ line                                                               │
   ├────────────────────────────────────────────────────────────────────┤
   │ --- original                                                       │
   │ +++ modified                                                       │
   │ @@ -17,8 +17,8 @@                                                  │
   │  glyphon = { package = "glyphon-tessera-fork", version = "0.9.0" } │
   │  log = "0.4.27"                                                    │
   │  parking_lot = "0.12.4"                                            │
   │ -tessera-ui = { path = "../tessera-ui" }                           │
   │ -tessera-ui-macros = { path = "../tessera-ui-macros" }             │
   │ +tessera-ui = { version = "0.2.1" }                                │
   │ +tessera-ui-macros = { version = "0.1.0" }                         │
   │  unicode-segmentation = "1.12.0"                                   │
   │  encase = { version = "0.11.1", features = ["glam"] }              │
   │  glam = "0.30.4"                                                   │
   ╰────────────────────────────────────────────────────────────────────╯
   tessera-ui-macros\Cargo.toml
   ╭──────────────────────────────────────────╮
   │ line                                     │
   ├──────────────────────────────────────────┤
   │ --- original                             │
   │ +++ modified                             │
   │ @@ -13,4 +13,4 @@                        │
   │  [dependencies]                          │
   │  quote = "1.0.40"                        │
   │  syn = "2.0.101"                         │
   │ -tessera-ui = { path = "../tessera-ui" } │
   │ +tessera-ui = { version = "0.2.1" }      │
   ╰──────────────────────────────────────────╯
   ```

   可以看到，dry run 会显示所有的操作，负责任的发版应该先审查是否符合预期。

2. 如果 dry run 没有问题，可以执行实际的发布，这里举例发布 tessera-ui：

   ```bash
   rust-script scripts/release-package.rs -p tessera-ui patch --execute
   ```

   这会执行实际的发布操作，包括更新版本号、生成更新日志、自动处理 path 转为版本号（这样才能发布到 crates.io），发布到 crates.io，并推送到远程仓库。

   注意：`--execute` 参数是必须的，否则脚本只会 dry run，不会执行实际操作。
