# GitHubの使用（オプション）

````admonish reset title="Reset your progress" collapsible=true
To reset your progress to the start of this chapter, run the following command:

```sh
curl https://jj-for-everyone.github.io/reset.sh | bash -s github
cd ~/jj-tutorial/repo
```
````

約束通り、[GitHub](https://github.com/) の使用に関するいくつかのヒントです。
興味がない場合は、次の章に進んでください、後で関連しません。

GitHubは最も人気のあるGitホスティングプロバイダーですが、唯一のものではありません。
他には [GitLab](https://about.gitlab.com/) と [Codeberg](https://codeberg.org/) があります。
Codebergは [Forgejo](https://forgejo.org/) の無料インスタンスで、オープンソースソフトウェアです、自分でホストできます。

これらのプロバイダーはすべて非常に似ていますので、他のプロバイダーに適応するのは簡単です。

## SSHキーで認証する

JujutsuはあなたのGitHubユーザーを認証して、あなたの代わりにコミットを受信する必要があります。
ユーザー名とパスワードでそれを行うことは可能ですが、とても面倒で推奨しません。
バックアップを作成するのが面倒だと、**あまり頻繁に**行いません。
バックアップが少ないと、リスクが高くなります！
認証を可能な限りシームレスにしましょう。

最良の認証方法はSSHキーを使用することです。
それはパスワードよりも便利で安全です。
GitHubにはそれを設定するための素晴らしいドキュメントがありますので、この指示に従ってください：
- [新しいSSHキーを生成する](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [SSHキーをアカウントに追加する](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

このコマンドでセットアップを確認できます：

```sh
ssh -T git@github.com
```

期待される出力は：

```
Hi user! You've successfully authenticated, but GitHub does not provide shell access.
```

## GitHubで新しいリポジトリを作成する

既存のリポジトリを使用する場合は、先に進んでください。

GitHubで新しいリポジトリを作成するには、[ここをクリック](https://github.com/new) してフォームに記入します。
必要なのは所有者（おそらくあなたのユーザー名）とリポジトリ名だけです。
可視性もあなたが望むものに一致するようにチェックしてください（後で変更可能）。

既存のリポジトリにプッシュしたいコンテンツがローカルにある場合、**リポジトリにコンテンツを初期化しない**ことを確認してください。
つまり、テンプレート、README、`.gitignore`、ライセンスなしです。

最後に、"Create repository" をクリックします。

## 既存のリポジトリをクローンする

ブラウザで既存のリポジトリのページに移動します。
緑色の "Code" ボタンをクリックします。
**SSH** をドロップダウンで選択してください（上記のSSHキーを設定したと仮定）。
表示されたURLをコピーします。

![](./github_ssh_url.png)

最後に、URLをJujutsuのクローンコマンドに貼り付けます：

```sh
jj git clone --colocate <COPIED_URL>
```
