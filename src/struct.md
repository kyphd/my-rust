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

## 列挙型

- キーワード`enum`で新しい型を生成することができる。
- いくつかのタグ付された値を持つことができる。
- `match`は保有する全ての列挙値を処理する手助けすることができ、コードの品質を維持することができる。

```rust
#![allow(dead_code)] // この行でコンパイラのwaringsメッセージを止める。

enum Species {
    Crab,
    Octopus,
    Fish,
    Clam
}

struct SeaCreature {
    species: Species,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}

fn main() {
    let ferris = SeaCreature {
        species: Species::Crab,
        name: String::from("Ferris"),
        arms: 2,
        legs: 4,
        weapon: String::from("claw"),
    };

    match ferris.species {
        Species::Crab => println!("{} is a crab",ferris.name),
        Species::Octopus => println!("{} is a octopus",ferris.name),
        Species::Fish => println!("{} is a fish",ferris.name),
        Species::Clam => println!("{} is a clam",ferris.name),
    }
}
```

## データを持つ列挙型

- `enum`は一個もしくは複数な型のデータを持つことができ、C言語の`union`の様な表現ができる。
- `match`を用いて列挙値に対するパターンマッチングを行う際、各データを変数名に束縛することができる。
- 列挙 のメモリ事情:
    - 列挙型のメモリサイズはそれが持つ最大要素のサイズと等しい。これにより全ての代入可能な値が同じサイズのメモリ空間を利用することが可能。
    - 要素の型以外に、各要素には数字値がついており、どのタグであるかについて示している。
- その他の事情:
    - Rustの列挙はtagged-unionとも言われる。
    - 複数の型を組み合わせて新しい型を作ることができる。Rustがalgebraic typesを持つと言われる理由。