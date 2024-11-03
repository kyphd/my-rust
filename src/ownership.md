# 所有権

- Rustの各値は、所有者と呼ばれる変数と対応している。
- いかなる時も所有者は一つである。
- 所有者がスコープから外れたら、値は破棄される。

## スコープ

Rustでは、スコープの終わりをリソースのデストラクトと解放の場所として使用する。このデストラクトと解放のことをドロップ(drop)と呼ぶ。

```rust
{                      // sは、ここでは有効ではない。まだ宣言されていない
    let s = "hello";   // sは、ここから有効になる

    // sで作業をする
}                      // このスコープは終わり。もうsは有効ではない

```

構造体がドロップされると、まず構造体自体がドロップされ、次にその子要素が個別に削除される。

```rust
struct Bar {
    x: i32,
}

struct Foo {
    bar: Bar,
}

fn main() {
    let foo = Foo { bar: Bar { x: 42 } };
    println!("{}", foo.bar.x);
    // foo が最初にドロップ
    // 次に foo.bar がドロップ
}
```

## 所有権の移動 （move）

所有権は移動する。

```rust
fn main() {
    let x = 5;
    let y = x;
    println!("{} {}", x, y);    // スタック上のメモリはコピーされる。

    let s1 = String::from("hello")
    let s2 = s1;

    println!("{}, world!", s1); // エラー。ヒープ上のメモリの所有権は移動(move)する。
}
```

### 関数の場合も移動する

所有者が関数の実引数として渡されると、所有権は関数の仮引数に移動(move)する。

移動後は、元の関数内の変数は使用できなくなる。

```rust
fn main() {
    let s = String::from("hello");  // sがスコープに入る

    takes_ownership(s);             // sの値が関数にムーブされ...
                                    // ... ここではもう有効ではない

    let x = 5;                      // xがスコープに入る

    makes_copy(x);                  // xも関数にムーブされるが、
                                    // i32はCopyなので、この後にxを使っても
                                    // 大丈夫

} // ここでxがスコープを抜け、sもスコープを抜ける。ただし、sの値はムーブされているので、何も特別なことは起こらない。
  //

fn takes_ownership(some_string: String) { // some_stringがスコープに入る。
    println!("{}", some_string);
} // ここでsome_stringがスコープを抜け、`drop`が呼ばれる。後ろ盾してたメモリが解放される。
  // 

fn makes_copy(some_integer: i32) { // some_integerがスコープに入る
    println!("{}", some_integer);
} // ここでsome_integerがスコープを抜ける。何も特別なことはない。
```

所有権は関数から返すことができる。

```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownershipは、戻り値をs1に
                                        // ムーブする

    let s2 = String::from("hello");     // s2がスコープに入る

    let s3 = takes_and_gives_back(s2);  // s2はtakes_and_gives_backにムーブされ
                                        // 戻り値もs3にムーブされる
} // ここで、s3はスコープを抜け、ドロップされる。s2もスコープを抜けるが、ムーブされているので、
  // 何も起きない。s1もスコープを抜け、ドロップされる。

fn gives_ownership() -> String {             // gives_ownershipは、戻り値を
                                             // 呼び出した関数にムーブする

    let some_string = String::from("hello"); // some_stringがスコープに入る

    some_string                              // some_stringが返され、呼び出し元関数に
                                             // ムーブされる
}

// takes_and_gives_backは、Stringを一つ受け取り、返す。
fn takes_and_gives_back(a_string: String) -> String { // a_stringがスコープに入る。

    a_string  // a_stringが返され、呼び出し元関数にムーブされる
}
```

## clone

ヒープデータのdeep copyが必要ならば、 `clone`と呼ばれるメソッドを使う。

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

## 所有権の借用（参照）

参照は、`&`演算子を使ってリソースへのアクセスを借用できるようにしてくれる。

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    // '{}'の長さは、{}です
    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
} // ここで、sはスコープ外になる。けど、参照しているものの所有権を持っているわけではないので何も起こらない。
```

### 可変な参照

参照先で値を変更したい場合、`&mut`をつける。

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

## 参照外し

`&mut`による参照では、`*`演算子によって参照を外す(dereference)ことで、所有者の値を設定できる。

```rust
fn main() {
    let mut foo = 42;
    let f = &mut foo;
    let bar = *f; // 所有者の値を取得
    *f = 13;      // 参照の所有者の値を設定
    println!("{}", bar);
    println!("{}", foo);
}
```



