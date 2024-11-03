# 列挙型

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