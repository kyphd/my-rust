# 関数

関数名にはスネークケース`snake_case`を使用。

```rust
fn add(x: i32, y: i32) -> i32 {
    return x + y;
}

fn main() {
    println!("{}", add(42, 13));
}
```

## 戻り値

関数、ブロックの最後が`;`のない式であれば、戻り値として使用される。(return省略。最後以外は省略できない。)

```rust
fn example() -> i32 {
    let v = {
        // ブロックのスコープは関数のスコープから分離されている
        let a = 1;
        let b = 2;
        a + b
    };
    println!("ブロックより: {}", v);

    // Rust で関数の最後から値を返す慣用的な方法
    v + 4
}

fn main() {
    println!("関数より: {}", example());
}
```

### 複数の戻り値

値をタプルで返すことによって、複数の値を返せる。

```rust
fn swap(x: i32, y: i32) -> (i32, i32) {
    return (y, x);
}

fn main() {
    // 戻り値をタプルで返す
    let result = swap(123, 321);
    println!("{} {}", result.0, result.1);

    // タプルを2つの変数に分解
    let (a, b) = swap(result.0, result.1);
    println!("{} {}", a, b);
}
```

### 空の戻り値

関数に戻り値の型が指定されていない場合、unit と呼ばれる空のタプルを返す。

空のタプルは `()` と表記する。

```rust
fn make_nothing() -> () {
    return ();
}

// 戻り値は () と推論
fn make_nothing2() {
    // この関数は戻り値が指定されないため () を返す
}

fn main() {
    let a = make_nothing();
    let b = make_nothing2();

    // 空を表示するのは難しいので、
    // a と b のデバッグ文字列を表示
    println!("a の値: {:?}", a);
    println!("b の値: {:?}", b);
}
```
