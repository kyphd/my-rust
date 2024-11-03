# ジェネリック型

Rustでは、例えば数値演算をするときに、左値と右値の型が同じである必要がある。

例えば、加算を行う`add`という関数を考える。数値型には整数型や浮動小数点型などあるが、型の数だけ`add`関数を定義してしまうと同じコードが大量に出来てしまう。そこで，引数の型が変わっても関数本体のコードが変わらない場合は、任意の型を受け取れる関数を定義することでコードの重複を避けることが出来る。このような仕組みをジェネリクスと言い，任意の型のことをジェネリック型と言う。

- null 許容な値（つまりまだ値を持たない変数）の表現
- エラー処理
- コレクション

などにも使用される。

```rust
fn add<T: std::ops::Add<Output=T> >(a: T, b: T) -> T {
    a+b
}

struct Point<T> { x: T, y: T }

enum Result<T,E> {
    Ok(T),
    Err(E),
}
```

```rust
struct Point<T> { x: T, y: T }

impl<T> Point<T> {
    fn xy(self) -> (T, T) {
        (self.x, self.y)
    }
}
```

`impl`の後ろに`<T>`が必要。

```rust
let point = Point::<f64>{x: 3., y: 5.};
```

Rustは強い型推論があるので、ジェネリック型に対して適切な型を自動で推論してくれる。明示的に指定したい場合、`::<>`演算子を使う。この演算子は魚が速く泳いでいるように見えることから`turbofish`と呼ばれている。


## Option, Some, None

Rustは基本NULLになりえない。もしNULLを使いたいなら明示する必要がある。それが`Option`。

```rust
enum Option<T> {
    Some(T),
    None,
}
```

`Option`は標準ライブラリに定義されている。さらに初期化処理にもあるため、`use`などせずとも使える。列挙子までそうであるため、接頭辞`Option::`なしで`Some`、`None`が使える。

```rust
enum Item {
    Inventory(String),
    // None は項目がないことを表す
    None,
}

struct BagOfHolding {
    item: Item,
}
```

### Some(T)

`Some(T)`は何かしらの型を1つ持った、匿名タプル構造体型。

```rust
let some1 = Some(5);
let some2 = Some("hello");
```

`Some`の引数はi32型, &str型など、何でもいい。

#### Some(T)におけるTの値の取得

```rust
fn main() {
    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}
```

ポイントは`match x { Some(i) => ... }`の`Some(i)`にある`i`。値がなんであれマッチするし、その値を変数`i`として取り出せる。

### None

他言語でいうところのNULL相当。enum型`Option<T>`の値のひとつであり、引数に構造体をとらない。

```rust
let nullable_int: Option<i32> = None;
nullable_int = Some(100);
```

変数`nullable_int`はi32型だが、NULLも許容したい。そんなときに`Option<i32>`型を使う。

以下はエラーになる。

```rust
nullable_int = 100; // error
nullable_int = Some("hello"); // error
let sum = Some(5) + 1; // error
```

## Result

Rustには`Result`と呼ばれるジェネリックな列挙型が組み込まれており、失敗する可能性のある値を返せる。これは言語がエラーを処理する際の慣用的な方法です。

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

このジェネリック型はカンマで区切られた複数のパラメータ化された型を持つことに注意。

この列挙型はとても一般的なもので、`Ok`と`Err`を使えばどこでもインスタンスを生成できる。

```rust
fn do_something_that_might_fail(i:i32) -> Result<f32,String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() {
    let result = do_something_that_might_fail(12);

    // match は Result をエレガントに分解して、
    // すべてのケースが処理されることを保証できます！
    match result {
        Ok(v) => println!("発見 {}", v),
        Err(e) => println!("Error: {}",e),
    }
}
```

### mainはResultを返せる。

```rust
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

// main は値を返しませんが、エラーを返すことがあります！
fn main() -> Result<(), String> {
    let result = do_something_that_might_fail(12);

    match result {
        Ok(v) => println!("発見 {}", v),
        Err(_e) => {
            // エラーをうまく処理
            
            // 何が起きたのかを説明する新しい Err を main から返します！
            return Err(String::from("main で何か問題が起きました！"));
        }
    }

    // Result の Ok の中にある unit 値によって、
    // すべてが正常であることを表現していることに注意してください。
    Ok(())
}
```

### 簡潔なエラー処理

`Result`はとてもよく使うので、Rustにはそれを扱うための強力な演算子`?`が用意されている。以下の2つのコードは等価。

```rust
do_something_that_might_fail()?
```

```rust
match do_something_that_might_fail() {
    Ok(v) => v,
    Err(e) => return Err(e),
}
```

```rust
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() -> Result<(), String> {
    // コードが簡潔なのに注目！
    let v = do_something_that_might_fail(42)?;
    println!("発見 {}", v);
    Ok(())
}
```

### やっつけなOption/Result処理

`Option`/`Result`を使って作業するのは、ちょっとしたコードを書くのには厄介である。

`Option`と`Result`の両方には`unwrap`と呼ばれる関数があり、手っ取り早く値を取得するのには便利である。

`unwrap`は以下のことを行う。

- `Option`/`Result`内の値を取得する。
- 列挙型が`None`/`Err`の場合、`panic!`する。

以下の2つのコードは等価です。

```rust
my_option.unwrap()
```

```rust
match my_option {
    Some(v) => v,
    None => panic!("Rust によって生成されたエラーメッセージ！"),
}
```

同様に:

```rust
my_result.unwrap()
```

```rust
match my_result {
    Ok(v) => v,
    Err(e) => panic!("Rust によって生成されたエラーメッセージ！"),
}
```

良いRust使い（Rustacean）であるためには、可能な限り適切に`match`を使用すること。

```rust
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() -> Result<(), String> {
    // 簡潔ですが、値が存在することを仮定しており、
    // すぐにダメになる可能性があります。
    let v = do_something_that_might_fail(42).unwrap();
    println!("発見 {}", v);
    
    // パニックするでしょう！
    let v = do_something_that_might_fail(1).unwrap();
    println!("発見 {}", v);
    
    Ok(())
}
```

