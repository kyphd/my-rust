---
sidebar_position: 4
---

# 変数

## 宣言

```rust
let x = 5;  // 不変変数
x = 6;      // エラー

let mut y = 5;  // mut で可変に
y = 7;          // OK

const MAX_POINTS: u32 = 100_000;    // 定数
```

## シャドーイング

```rust
let x = 5;
let x = x + 1;      // シャドーイング, xを覆い隠せる
{
    let x = x * 2;
    println!("The value of x in the inner scope is: {}", x);    // 12
}

println!("The value of x is: {}", x);   // 6
```

`mut`と上書きのもう一つの違いは、再度`let`キーワードを使用したら、実効的には新しい変数を生成していることになるので、 値の型を変えつつ、同じ変数名を使いまわせる。

```rust
let spaces = "   ";
let spaces = spaces.len();
```

`mut`だとエラーになる。

```rust
let mut spaces = "   ";
spaces = spaces.len();      // エラー
```

## データ型

