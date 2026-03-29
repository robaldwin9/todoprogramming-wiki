---
title: Rust Programming Language
description: 
published: true
date: 2025-02-21T07:49:46.405Z
tags: 
editor: markdown
dateCreated: 2025-02-20T07:38:24.667Z
---

# Introduction
Rust is a systems programing language that prioritizes memory safety it is considered a safer alternative to languages like C, and C++. This page summerizes details about rust, but there are many other resources available

## Resources
* [rust book](https://doc.rust-lang.org/beta/book/title-page.html)
* [libs.rs](https://lib.rs/)
* [crates](https://crates.io/)
* [Docs.rs](https://docs.rs/)
* [rust playground](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://play.rust-lang.org/&ved=2ahUKEwiz9qWSotSLAxUwhIkEHflBHqsQFnoECBMQAQ&usg=AOvVaw3BJT62fT4LznNOufePc50Ehttps://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://play.rust-lang.org/&ved=2ahUKEwiz9qWSotSLAxUwhIkEHflBHqsQFnoECBMQAQ&usg=AOvVaw3BJT62fT4LznNOufePc50E)

# Setup For Development

## Windows Rust Build Tools Install

Easiest way to setup for rust software development on windows is using winget.
`winget install -e --id Rustlang.Rust.MSVC`

## Jetbrains Rustrover Install
Good choice if you have past experience with jetbrains, though we do not necesairly need an IDE for smaller projects.
`winget install --id=JetBrains.RustRover.EAP  -e`

## Sublime Packages
* `ctrl + shift + p` for command window
	* ["Rust Enhanced"](https://github.com/rust-lang/rust-enhanced) package for syntax highlighting and inline warnings/errors
  * ["TOML"](https://github.com/jasonwilliams/sublime_toml_highlighting) package For editing .toml files 	

# Cargo
Cargo is the official package manager and build tool for rust. This section is a quck reference, but the [cargo book](https://doc.rust-lang.org/cargo/commands/package-commands.html) the has much more detailed information.

## Create Project
* `cargo init`  initialize current directory as rust project

```
cargo init 
	Creating binary (application) package
note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html
```

* `cargo new <name> --bin` Creates a directory `<name>` and ititializes it as a rust proejct.
* `cargo new <name> --lib` initialize project as a library.

## Build Project
* `cargo build` builds the project 
	* The resulting executable can be found at `./target/debug/<name>.exe`
* `cargo build --release` builds an optimized release binary. 
	* The resulting executable can be found at `./target/release/<name>.exe`

## Add Crates
* `cargo add clap --features derive`
	* 	`cargo add <crate>`	addes a library/crate to the project
	* `--features derive` includes a feature of the crate
	* `cargo add` edits the cargo.toml