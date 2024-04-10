# 変数

## 宣言

```rust
let x = 5;  // 不変変数
x = 6;      // エラー

let mut y = 5;  // mut で可変に
y = 7;          // OK

const MAX_POINTS: u32 = 100_000;    // 定数
```

- 変数名にはスネークケース`snake_case`を使用
- 定数名には大文字のスネークケース`SCREAMING_SNAKE_CASE`を使用。

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

### 基本的な型

- ブール型 - bool は true または false を表します
- 符号なし整数型 - u8 u32 u64 u128 は正の整数を表します
- 符号付き整数型 - i8 i32 i64 i128 は正と負の整数を表します
- ポインタサイズ整数型 - usize isize はメモリ内のインデックスとサイズを表します
- 浮動小数点数型 - f32 f64
- タプル型 - (value, value, ...) スタック上の固定された値の組を渡すために使用されます
- 配列型 - コンパイル時に長さが決まる同じ要素のコレクション
- スライス型 - 実行時に長さが決まる同じ要素のコレクション
- str(string slice) - 実行時に長さが決まるテキスト

```rust
bool			// 真偽値(true/false)
i8			// 符号付き8ビット整数
u8			// 符号無し8ビット整数
i16			// 符号付き16ビット整数
u16			// 符号無し16ビット整数
i32			// 符号付き32ビット整数
u32			// 符号無し32ビット整数
i64			// 符号付き64ビット整数
u64			// 符号無し64ビット整数
i128			// 符号付き128ビット整数
u128			// 符号無し128ビット整数
isize			// ポインタサイズと同じ符号付き整数
usize			// ポインタサイズと同じ符号無し整数
f32			// 32ビット浮動小数点数
f64			// 64ビット浮動小数点数
char			// 文字(U+0000～U+D7FF, U+E000～U+10FFFF)
str			// 文字列(&strとして使用することが多い)
(type, type, ...)	// タプル
[type; len]		// 配列
Vec<type>		// ベクタ
&type			// typeへの参照
&mut type		// typeへのミュータブルな参照
&[type]			// type型要素を持つスライス
```

```rust
let x = 12; // デフォルトでは i32
let a = 12u8;  // 数値の後に型を付加することでも指定できる。
let b = 4.3; // デフォルトでは f64
let c = 4.3f32;
let bv = true;
let t = (13, false);
let sentence = "hello world!";
println!(
    "{} {} {} {} {} {} {} {}",
    x, a, b, c, bv, t.0, t.1, sentence
);
```

### 型変換

`as`を使う。

```rust
let a = 13u8;
let b = 7u32;
let c = a as u32 + b;   // u8とu32を混ぜるとエラー。型変換必要
println!("{}", c);

let t = true;
println!("{}", t as u8);
```

## 配列

```rust
let nums: [i32; 3] = [1, 2, 3];
println!("{:?}", nums);
println!("{}", nums[1]);
```

