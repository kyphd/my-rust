# 演算子


| 演算子 | 例                                                      | 説明                         | オーバーロードできる？ | 
| ------ | ------------------------------------------------------- | ---------------------------- | ---------------------- | 
| !      | ident!(...), ident!\{...\}, ident\![...]                   | マクロ展開                   |                        | 
| !      | !expr                                                   | ビット反転、または論理反転   | Not                    | 
| !=     | var != expr                                             | 非等価比較                   | PartialEq              | 
| %      | expr % expr                                             | 余り演算                     | Rem                    | 
| %=     | var %= expr                                             | 余り演算後に代入             | RemAssign              | 
| &      | &expr, &mut expr                                        | 借用                         |                        | 
| &      | &type, &mut type, &'a type, &'a mut type                | 借用されたポインタ型         |                        | 
| &      | expr & expr                                             | ビットAND                    | BitAnd                 | 
| &=     | var &= expr                                             | ビットAND後に代入            | BitAndAssign           | 
| &&     | expr && expr                                            | 論理AND                      |                        | 
| *      | expr * expr                                             | 掛け算                       | Mul                    | 
| *      | *expr                                                   | 参照外し                     |                        | 
| *      | *const type, *mut type                                  | 生ポインタ                   |                        | 
| *=     | var *= expr                                             | 掛け算後に代入               | MulAssign              | 
| +      | trait + trait, 'a + trait                               | 型制限の複合化               |                        | 
| +      | expr + expr                                             | 足し算                       | Add                    | 
| +=     | var += expr                                             | 足し算後に代入               | AddAssign              | 
| ,      | expr, expr                                              | 引数と要素の区別             |                        | 
| -      | - expr                                                  | 算術否定                     | Neg                    | 
| -      | expr - expr                                             | 引き算                       | Sub                    | 
| -=     | var -= expr                                             | 引き算後に代入               | SubAssign              | 
| ->     | fn(...) -> type, &#124;...&#124; -> type                | 関数とクロージャの戻り値型   |                        | 
| .      | expr.ident                                              | メンバーアクセス             |                        | 
| ..     | .., expr.., ..expr, expr..expr                          | 未満範囲リテラル             |                        | 
| ..     | ..expr                                                  | 構造体リテラル更新記法       |                        | 
| ..     | variant(x, ..), struct_type \{ x, .. \}                   | 「残り全部」パターン束縛     |                        | 
| ...    | expr...expr                                             | パターンで: 以下範囲パターン |                        | 
| /      | expr / expr                                             | 割り算                       | Div                    | 
| /=     | var /= expr                                             | 割り算後に代入               | DivAssign              | 
| :      | pat: type, ident: type                             | 型制約                       |                        | 
| :      | ident: expr                                             | 構造体フィールド初期化子     |                        | 
| :      | 'a: loop \{...\}                                          | ループラベル                 |                        | 
| ;      | expr;                                                   | 文、要素終端子               |                        | 
| ;      | [...; len]                                              | 固定長配列記法の一部         |                        | 
| \<\<     | expr \<\< expr                                            | 左シフト                     | Shl                    | 
| \<\<=    | var \<\<= expr                                            | 左シフト後に代入             | ShlAssign              | 
| \<      | expr \< expr                                             | 未満比較                     | PartialOrd             | 
| \<=     | expr \<= expr                                            | 以下比較                     | PartialOrd             | 
| =      | var = expr, ident = type                           | 代入/等価                    |                        | 
| ==     | expr == expr                                            | 等価比較                     | PartialEq              | 
| =\>     | pat =\> expr                                             | matchアーム記法の一部        |                        | 
| \>      | expr \> expr                                             | より大きい比較               | PartialOrd             | 
| \>=     | expr \>= expr                                            | 以上比較                     | PartialOrd             | 
| \>\>     | expr \>\> expr                                            | 右シフト                     | Shr                    | 
| \>\>=    | var \>\>= expr                                            | 右シフト後に代入             | ShrAssign              | 
| @      | ident @ pat                                             | パターン束縛                 |                        | 
| ^      | expr ^ expr                                             | ビットXOR                    | BitXor                 | 
| ^=     | var ^= expr                                             | ビットXOR後に代入            | BitXorAssign           | 
| &#124; | pat &#124; pat                                          | パターンOR                   |                        | 
| &#124; | &#124;…&#124; expr                                      | クロージャ                   |                        | 
| &#124; | expr &#124; expr                                        | ビットOR                     | BitOr                  | 
| &#124;= | var &#124;= expr                                       | ビットOR後に代入             | BitOrAssign            | 
| &#124;&#124; | expr &#124;&#124; expr                            | 論理OR                       |                        | 
| ?      | expr?                                                   | エラー委譲                   |                        | 

