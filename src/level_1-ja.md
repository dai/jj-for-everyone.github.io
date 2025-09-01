# レベル1

このレベルでは、作業を進めるために必要な最低限のスキルを身につけます。
これは最もシンプルなユースケースで、単独で作業する場合にのみ十分です。
例えば、Gitリポジトリで宿題を追跡して提出する学生は、これ以上必要ありません。

以下の「チートシート」には、レベル1で最も重要なコマンドが含まれています。
始める前に脳にインプットし、後で忘れたときに思い出すために使ってください。

````admonish info title="チートシート"
著者情報を設定する
```sh
jj config set --user user.name "Alice"
jj config set --user user.email "alice@local"
```
リポジトリを初期化する
```sh
jj git init --colocate
```
既存のリポジトリをクローンする
```sh
jj git clone --colocate <PATH_OR_URL>
```
変更をコミットする
```sh
jj commit
```
最新のコミットを「main」ブックマークにプッシュする
```sh
jj bookmark move main --to @-
jj git push
```
````
