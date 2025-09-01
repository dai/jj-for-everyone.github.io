# インストールとセットアップ

多くの方法でJujutsuをインストールできますが、最良のものはあなたのシステムによって異なります。
Jujutsuをインストールする方法についてまったく気にしない場合、すべてを飛ばしてJujutsuを手に入れたい場合は、これらのコマンドをコピーして貼り付けてください：

```sh
curl https://mise.run | sh
~/.local/bin/mise install-into jujutsu@latest /tmp/jj-install
mv /tmp/jj-install/jj ~/.local/bin
rm -rf /tmp/jj-install
exec $SHELL --login
```

```admonish info title="これらのコマンドの説明" collapsible=true
ソフトウェアのインストールは思ったよりも難しいです。
それはCPUアーキテクチャとオペレーティングシステムなどの多くの要因に依存します。
それが、任意のシステムでJujutsuをインストールする単一の簡単なコマンドがない理由です。
代わりに、ソフトウェアをインストールする専門のプログラムである `mise` を最初にインストールします。
（miseについては [そのウェブサイト](https://mise.jdx.dev/) で読むことができます。）
最初のコマンド `curl https://mise.run | sh` はインターネットからスクリプトをダウンロードして実行し、あなたのために `mise` をインストールします。
これは危険で、ダウンロード元のウェブサイトの所有者を信頼する場合にのみ行うべきです。
しかし、それは便利なテクニックです。

2番目のコマンドは `mise` を実行してJujutsuを一時ディレクトリにダウンロードします。
`mise` があなたのオペレーティングシステムとCPUアーキテクチャに適したバイナリをダウンロードするように指定する必要があります。
`~/.local/bin/mise` の完全パスを指定します、なぜならこの時点で `~/.local/bin` があなたの `PATH` 変数に含まれているかどうかわからないからです。
（["Terminal basics"](./terminal_basics.md#the-path-variable) の章でそれについて説明します。）
`mise` はダウンロードしたバイナリを `~/.local/bin` に移動します、これはユーザー固有のプログラムの慣習的な場所です。
`rm -rf /tmp/jj-install` ("remove recursive force") は一時ダウンロードディレクトリとその内容を削除します。

最後に、`exec $SHELL --login` はあなたのシェルを再起動し、そのスタートアップスクリプトを実行します。
一部のLinuxディストリビューション（Ubuntuなど）は、`~/.local/bin` が存在する場合にのみそれを `PATH` 変数に追加します。
Jujutsuをインストールした後にターミナルを再起動することで、システムが新しいプログラムを見つけることを確実にします。

一部のディストリビューションが `~/.local/bin` を `PATH` に**まったく**追加しない場合があるかもしれませんが、私はそのようなものを知りません。
（そのような関連するものを知っている場合、[issueを開いてください](https://github.com/jj-for-everyone/jj-for-everyone.github.io/issues/new)！）
あなた自身でその問題を修正するには、[shell startup script](http://localhost:3210/terminal_basics.html#startup-scripts) で `PATH` 変数を拡張します。
```

````admonish info title="他のインストール方法" collapsible=true
公式のインストール手順はさまざまなプラットフォームで [ここ](https://jj-vcs.github.io/jj/latest/install-and-setup/) にあります。
私が重要なものとして言及するいくつかの方法があります。

[cargo-binstall](https://github.com/cargo-bins/cargo-binstall) を使用する場合、これは素晴らしいです：

```sh
cargo-binstall jj-cli
```

Mac & Homebrewユーザーなら、これがあなたのためです：

```sh
brew install jj
```

Rustツールチェーンがインストールされている場合、ソースからコンパイルできます：

```sh
cargo install --locked --bin jj jj-cli
```

[release page](https://github.com/jj-vcs/jj/releases/latest) から直接バイナリをダウンロードすることもできます。
"Assets" までスクロールし、名前でアーカイブをダウンロードします。
それは2つのものに依存します：あなたのオペレーティングシステムとあなたのCPUアーキテクチャ。
名前であなたのシステムに一致する文字列を探してください。

オペレーティングシステムを識別する方法：

| オペレーティングシステム | 探す文字列 |
| --- | --- |
| Linux | unknown-linux-musl |
| Mac | apple-darwin |
| Windows | pc-windows-msvc |

CPUアーキテクチャを識別する方法：

| CPUブランド | 探す文字列 |
| --- | --- |
| Intel | x86_64 |
| AMD | x86_64 |
| Apple | aarch64 |
| ARM | aarch64 |
| Qualcom (Snapdragon) | aarch64 |

適切なアーカイブをダウンロードしたら、それを抽出する必要があります。
ファイルエクスプローラーでダウンロードしたアーカイブを右クリックし、"extract" または同様のものを選択できます。
抽出されたフォルダにはドキュメントと "jj" というファイルが含まれます。
それを `~/.local/bin/` ディレクトリに移動する必要があります。
（プログラムを保持する他の場所を知っている場合、それを使用してください。）
````

`jj -h` を実行してインストールを確認します。
利用可能なコマンドのリストを表示します。
出力が `bash: jj: command not found...` のような場合、インストールは成功していません。

## 初期設定

Jujutsuは非常に設定可能です、しかし今はほとんどのノブとダイヤルを気にしません。
**必須**なのはあなたの名前とメールだけです。
これは必須のメタデータで、これなしでは一部のものが正しく動作しません。
しかし、あなたの_本当の_名前とメールを入力する必要はありません、もしそれをリポジトリに保存することに不快を感じる場合。
（学校や仕事のプロジェクトに取り組んでいる場合、あなたの学校/仕事のメールで本当の名前を使用するのは通常問題ありません。
これらのリポジトリは通常公開アクセスされません。）

オープンソースプロジェクトに取り組む予定の場合、より注意が必要です。
GitHubハンドルをユーザー名として使用できますが、多くの人は本当の名前を使用しても快適です。
メールアドレスはより重要です。
通常のプライベートメールアドレスを使用すると、そのアドレスに望ましくないメールが届くリスクがあります。
オープンソース専用のアドレスを使用することを検討するか、GitHubが提供するアドレスを使用します。
それはあなたのGitHubアカウントを識別しますが、それを通じてメールを受信することはできません。
[GitHubのメール設定](https://github.com/settings/emails) に移動し、"Keep my email address private" を選択すると、トップにあなたのプライベートメールアドレスが表示されます。

ユーザー名とメールを設定するコマンドはこちら：

```sh
jj config set --user user.name "Anonymous"
jj config set --user user.email "anon@local"
```

シェル補完が必要な場合、[ここ](https://jj-vcs.github.io/jj/latest/install-and-setup/#command-line-completion) の指示に従ってください。
シェル補完とは何かわからない場合、無視してください。

## シンプルなテキストエディタのインストール

Jujutsuは時々テキストファイルを編集するよう求めます。
それをあなたのためにテキストエディタを開きます。
どのテキストエディタが開かれるかは設定可能です。
ターミナルで興味深いテキストエディタのオプションがたくさんありますが、初心者には最もシンプルで直感的なものをインストールするよう勧めます：

```sh
mise install-into edit@latest /tmp/edit-install
mv /tmp/edit-install/edit ~/.local/bin
rm -rf /tmp/edit-install
```

これらのコマンドを実行すると、`edit` というテキストエディタがインストールされます。
次に、Jujutsuにその特定のものをテキストファイルを開くときに使用するよう指示する必要があります：

```sh
jj config set --user ui.editor edit
```

これから、Jujutsuがあなたのためにテキストファイルを開くとき、`edit` を使用します。
編集が完了したら、メニューバーの "File" をクリックし、"Exit" をクリックするか、<kbd>Ctrl+Q</kbd> を押してテキストエディタを終了します。
ファイルを保存するかどうかを確認し、<kbd>Enter</kbd> を押して確認します。
それだけです！
初めて必要になったときに思い出せるようにします。
