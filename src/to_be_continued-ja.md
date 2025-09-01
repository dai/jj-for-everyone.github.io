# レベル1

このレベルでは、単独で作業する場合にのみ十分な、最もシンプルなユースケースのための最低限のスキルを提供します。例えば、Gitリポジトリで宿題を追跡して提出する学生は、これ以上必要ありません。

レベル1のチートシートはこちらです。[レベル1のチートシート](./level_1.md) も復習しておくと良いでしょう。

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
最新のコミットを "main" ブックマークにプッシュする
```sh
jj bookmark move main --to @-
jj git push
```
````
