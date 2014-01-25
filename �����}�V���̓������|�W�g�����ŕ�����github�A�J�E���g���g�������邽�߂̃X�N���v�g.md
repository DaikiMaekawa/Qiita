##はじめに
私の所属する組織ではロボット内の共有アカウントで複数のプログラマが開発しています。

最近GitHubでソースコードを管理し始めたのですが、ロボット内の同じリポジトリ内で開発しているとコミットする時のユーザ管理が少しめんどうだったのでメモ。

同じリポジトリ内で複数のアカウントを切り替えたいのですが、調べてもリポジトリ毎に設定する方法しか見当たりませんでした。

使用者は頻繁に入れ替わるのでgitconfigをその都度書き直すのもめんどうですし、忘れそうです。

##解決策
コミット前にコミッタをチェックするスクリプトを書きました。

ソースコードは[GitHub](https://github.com/DaikiMaekawa/git-check-committer)にあります。

##使用方法

普通にコミットする。

    $ git commit -m "msg"

アカウントの情報が表示され

 * yを入力すると通常通りコミットされる。
 * nを入力するとアカウントを再設定できる。

    Author = USER_NAME <USER_EMAIL>
    Do you want to me to keep it this way? [y/n] n

新しいアカウントを設定する。

    Username:NEW_USER_NAME
    Email:NEW_USER_EMAIL
    Please commit that again...

もう一度コミットを求められる。

    $ git commit -m "msg"

更新されたアカウントの情報を確認し、問題なければyを入力する。

    Author = NEW_USER_EMAIL <NEW_USER_EMAIL>
