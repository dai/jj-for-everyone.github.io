# リポジトリの初期化

````admonish reset title="Reset your progress" collapsible=true
To reset your progress to the start of this chapter, run the following command:

```sh
curl https://jj-for-everyone.github.io/reset.sh | bash -s initialize
```
````

"リポジトリ" はJujutsuがファイルのすべてを追跡するディレクトリ（フォルダ）です。
リポジトリは通常プロジェクトに対応し、無関係なプロジェクトのバージョン履歴は互いに結びつきません。
リポジトリを作成するには、ファイルシステムに新しいフォルダを作成します。
このチュートリアルでは、`~/jj-tutorial/repo` を使用します。
そうしないと、後で実行するコマンドが動作しないかもしれません。
（ホームディレクトリにゴミが残るのが嫌なら、いつでも削除して [reset script](./introduction.md#reset-your-progress) を使用して続けてください。）
そのディレクトリで `jj git init --colocate` を実行して新しいリポジトリを初期化します。

コピーして貼り付けるコマンド：

```sh
mkdir -p ~/jj-tutorial/repo
cd ~/jj-tutorial/repo
jj git init --colocate
```

最初の `jj` コマンドを分解しましょう。
`git` はGit固有の互換性機能のためのサブコマンドです。
その一つは `init` コマンドで、新しいGit互換リポジトリを初期化します。
`--colocate` フラグについては説明しません、その詳細は重要ではなく、すぐにデフォルトになります。
今はフラグを使用してください。
バージョン `0.34` で省略できるようになるでしょう。

"リポジトリの初期化" とは何を意味するのでしょうか？
基本的に、Jujutsuは `.git` と `.jj` の2つのディレクトリを作成します。
これらにはバージョン履歴に関するすべての情報が含まれています。
なぜ2つのディレクトリ？
`.git` ディレクトリには重要なものがすべて含まれ、Git自体によって作成および管理されたかのように見える方法で保存されます。
`.jj` ディレクトリにはJujutsuの高度な機能を有効にする追加のメタデータが含まれます。

```admonish warning
これらのディレクトリ内のファイルを直接操作しないでください！
それらは構造化されたデータベースです。
データベース形式を破壊すると、リポジトリを完全に壊す可能性があります。
[remotes](./remotes.md) の章でバックアップの第2層について話します。
```

ドットで始まるファイルとディレクトリはデフォルトで隠されていますが、`ls -a` で作成されたことを確認できます：

```console
$ ls -a
.git  .jj
```
