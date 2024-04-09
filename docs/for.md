---
sidebar_position: 7
---

# for

イテレータとして評価される式を反復処理。

```rust
fn main() {
    for x in 0..5 {
        println!("{}", x);
    }

    for x in 0..=5 {
        println!("{}", x);
    }
}
```

- `..`演算子は、開始番号から終了番号の手前までの数値を生成するイテレータを作成する。
- `..=`演算子は、開始番号から終了番号までの数値を生成するイテレータを作成する。

## loop

### 無限ループ

```rust
fn main() {
    let mut x = 0;
    loop {
        x += 1;
        if x == 42 {
            break;
        }
    }
    println!("{}", x);
}
```

### `break` 抜けて値を返すことができる。

```rust
fn main() {
    let mut x = 0;
    let v = loop {
        x += 1;
        if x == 13 {
            break "13 を発見";
        }
    };
    println!("loop の戻り値: {}", v);
}
```

## while

条件が`false`と評価されたらループを終了。

```rust
fn main() {
    let mut x = 0;
    while x != 42 {
        x += 1;
    }
}
```