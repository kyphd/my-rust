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

## 構造体とメモリ

- コードの中で構造体をインスタンス化する際、フィールドデータはメモリ上で隣り合うように作成される。
- 全てのフィールドの値を指定してインスタンス化をする場合、`let 変数名 = 構造体名 {...};`
- 構造体のフィールドは演算子`.`で取り出す。

```rust
struct SeaCreature {
    animal_type: String,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}

fn main() {
    // SeaCreatureのデータはスタックに入る。
    let ferris = SeaCreature {
        // String構造体もスタックに入るが、ヒープに入るデータの参照アドレスが一つ入る。
        animal_type: String::from("crab"),
        name: String::from("Ferris"),
        arms: 2,
        legs: 4,
        weapon: String::from("claw"),
    };

    let sarah = SeaCreature {
        animal_type: String::from("octopus"),
        name: String::from("Sarah"),
        arms: 8,
        legs: 0,
        weapon: String::from("none"),
    };
    
    println!(
        "{} is a {}. They have {} arms, {} legs, and a {} weapon",
        ferris.name, ferris.animal_type, ferris.arms, ferris.legs, ferris.weapon
    );
    println!(
        "{} is a {}. They have {} arms, and {} legs. They have no weapon..",
        sarah.name, sarah.animal_type, sarah.arms, sarah.legs
    );
}
```

- ダブルクオートに囲まれたテキスト(例: "Ferris")は読み取り専用データであるため、データメモリに入る。
- 関数の呼び出し`String::from`では構造体`String`を作成し、この構造体と`SeaCreature`のフィールドは隣り合う形でスタックに入れられる。フィールドの値は変更可能であり、メモリ上では以下の様に変更される。
    1. ヒープに変更可能なメモリを作り、テキストを入れる。
    2. 1.で作成した参照アドレスをヒープに保存し、それを`String`に保存。
- 最後に、`Ferris`と`Sarah`はプログラムの中では固定な位置であるため、スタックに入る。

## タプルライクな構造体

```rust
struct Location(i32, i32);

fn main() {
    // これもスタックに入れられる構造体。
    let loc = Location(42, 32);
    println!("{}, {}", loc.0, loc.1);
}
```

## ユニットライクな構造体

- フィールドを持たない構造体。
- `unit`は空ユニット()の別名称。
- あまり使われない。

```rust
struct Marker;

fn main() {
    let _m = Marker;
}
```
