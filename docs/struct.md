---
sidebar_position: 8
---

# 構造体

- 一つの`struct`はフィールドの集合
- フィールドとはデータ構造とキーワードを紐付ける値。その値はプリミティブ型かデータ構造を指定可能。
- その定義はメモリ上で隣合うデータの配置をコンパイラに伝える設計図の様なもの

```rust
struct SeaCreature {
    // String は構造体である。
    animal_type: String,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}
```

## メソッド

- 関数(function)と違って、メソッド(method)は特定のデータ型と紐づく関数のこと。
- スタティックメソッド - ある型そのものに紐付き、演算子`::`で呼び出せる。
- インスタンスメソッド - ある型のインスタンスに紐付き、演算子`.`で呼び出せる。

```rust
fn main() {
    // スタティックメソッドでStringインスタンスを作成する。
    let s = String::from("Hello world!");
    // インスタンスを使ってメソッド呼び出す。
    println!("{} is {} characters long.", s, s.len());
}
```

// todo 次 https://tourofrust.com/26_ja.html