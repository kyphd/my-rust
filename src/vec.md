# ベクタ型

ベクタは構造体`Vec`で表される可変サイズのリスト。

マクロ`vec!`を使えば、手動で構築するよりも簡単にベクタを生成できる。

`Vec`にはメソッド`iter()`がある。これによってベクタからイテレータを生成すれば、ベクタを簡単に`for`ループに入れることができる。

メモリに関する詳細：

- `Vec`は構造体であるが、内部的にはヒープ上の固定リストへの参照を含んでいる。
- ベクタはデフォルトの容量で始まる。容量よりも多くの項目が追加された場合、ヒープ上により大きな容量の固定リストを生成し、データを再割り当てする。

```rust
fn main() {
    // 型を明示的に指定
    let mut i32_vec = Vec::<i32>::new(); // turbofish <3
    i32_vec.push(1);
    i32_vec.push(2);
    i32_vec.push(3);

    // もっと賢く、型を自動的に推論
    let mut float_vec = Vec::new();
    float_vec.push(1.3);
    float_vec.push(2.3);
    float_vec.push(3.4);

    // きれいなマクロ！
    let string_vec = vec![String::from("Hello"), String::from("World")];

    for word in string_vec.iter() {
        println!("{}", word);
    }
}
```
