---
sidebar_position: 3
---

# Cargo

CargoはRustのビルドシステム兼パッケージマネージャ。

- `cargo new`を使ってプロジェクトを作成できる
    -  利用可能なオプションを確認するには`cargo new --help`を実行。
- `cargo build`を使ってプロジェクトをビルドできる。`target/debug`に作成される。
- `cargo build --release`でリリース版をビルド。`target/release`に作成される。
- `cargo run`を使うとプロジェクトのビルドと実行を1ステップで行える
- `cargo check`を使うとバイナリを生成せずにプロジェクトをビルドして、エラーがないか確認できる
- `cargo update`：クレートをアップグレード
- `cargo doc --open`: すべての依存クレートが提供するドキュメントをローカルでビルドしてブラウザで開く
- `cargo search`: クレートの最新バージョンを検索

```bash
$ cargo --version
```

## プロジェクトの作成

```bash
$ cargo new hello
$ cd hello
```

### Cargo.toml

Cargoの設定フォーマット

```toml title="Cargo.toml"
[package]
name = "hello"
version = "0.1.0"
edition = "2021"

[dependencies]
```

### src/main.rs

```rust title="src/main.rs"
fn main() {
    println!("Hello, world!");
}
```

## プロジェクトのビルドと実行

### ビルド

```bash
$ cargo build
   Compiling hello v0.1.0 (/Users/ky/Desktop/rust/test/hello)
    Finished dev [unoptimized + debuginfo] target(s) in 3.51s
```

実行ファイル`target/debug/hello`が生成される。

```bash
$ ./target/debug/hello
Hello, world!
```

### run（ビルドと実行）

```bash
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/hello`
Hello, world!
```

