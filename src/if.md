# if

```rust
fn main() {
    let x = 42;
    if x < 42 {
        println!("42 より小さい");
    } else if x == 42 {
        println!("42 に等しい");
    } else {
        println!("42 より大きい");
    }
}
```

## 比較演算子

| 演算子 | 例                                                      | 説明                         | オーバーロードできる？ | 
| ------ | ------------------------------------------------------- | ---------------------------- | ---------------------- | 
| ==     | expr == expr                                            | 等価比較                     | PartialEq              | 
| !=     | var != expr                                             | 非等価比較                   | PartialEq              | 
| \<     | expr \< expr                                            | 未満比較                     | PartialOrd             |  
| \>     | expr \> expr                                            | より大きい比較               | PartialOrd             | 
| \<=    | expr \<= expr                                           | 以下比較                     | PartialOrd             | 
| \>=    | expr \>= expr                                           | 以上比較                     | PartialOrd             |
| !      | !expr                                                   | ビット反転、または論理反転   | Not                    | 
| &&     | expr && expr                                            | 論理AND                      |                        | 
| &#124;&#124; | expr &#124;&#124; expr                            | 論理OR                       |                        | 

## match

値が取り得るすべての条件にマッチさせて、マッチが真であればコードパスを実行する。

```rust
fn main() {
    let x = 42;

    match x {
        0 => {
            println!("found zero");
        }
        // 複数の値にマッチ
        1 | 2 => {
            println!("found 1 or 2!");
        }
        // 範囲にマッチ
        3..=9 => {      //  ..= は、開始番号から終了番号までの数値を生成するイテレータを作成
            println!("found a number 3 to 9 inclusively");
        }
        // マッチした数字を変数に束縛
        matched_num @ 10..=100 => {
            println!("found {} number between 10 to 100!", matched_num);
        }
        // どのパターンにもマッチしない場合のデフォルトマッチが必須
        _ => {
            println!("found something else!");
        }
    }
}
```

## ブロック式から値を返す。

`if`、`match`、関数、ブロックの最後が`;`のない式であれば、戻り値として使用される。

```rust
fn example() -> i32 {
    let x = 42;
    // Rust の三項式
    let v = if x < 42 { -1 } else { 1 };        // if文を三項演算子のように使用できる
    println!("if より: {}", v);

    let food = "ハンバーガー";
    let result = match food {
        "ホットドッグ" => "ホットドッグです",
        // 単一の式で値を返す場合、中括弧は省略可能
        _ => "ホットドッグではありません",
    };
    println!("食品の識別: {}", result);

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

