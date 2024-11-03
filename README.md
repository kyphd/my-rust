# My Rust

Rust/mdBookで作ってます。

## mdBook のコマンド

- `mdbook init` プロジェクトのひな形を生成
- `mdbook build --open` ビルドしてブラウザで開く
- `mdbook watch --open` ファイルの変更を監視して自動ビルド
- `mdbook serve -p 9090 --open` ローカルサーバをポート9090で起動してドキュメントを表示(デフォルトで自動ビルド)
- `mdbook clean` ビルドしたファイルをクリーン

大抵の場合、`mdbook serve -o`でサーバーを起動させておき、作業する。編集して保存するとブラウザで自動的にリロードされるため、執筆しながら出力結果をシームレスに確認できる。また、新しいチャプターが必要になれば`SUMMARY.md`に追加することで自動的にファイルが作成される。

## Deployment

Github Actionsでデプロイできるので、git pushするだけ。