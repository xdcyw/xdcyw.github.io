---
title: "Androidスマホからhugoを更新する方法"
date: 2021-09-29T05:29:27+09:00
draft: false
categories: [tech]
---

今回は、hugoで書かれたサイトをAndroidスマホから更新する方法を紹介していこうと思います。

github pagesにホスティングされている事を前提として解説していきます。

また、すでにhugoのプロジェクトが作成されている前提です。

まずは、Androidスマホに[Termux](https://termux.com/)をインストールします。

インストールが完了したら、Termuxを開いて以下のコマンドを実行してください。

```sh
pkg update
pkg install git openssh hugo
```

これで必要なソフトウェアのインストールが完了です。

次にGitの初期設定をします。

```bash
$ git config --global user.name "Yourname"
$ git config --global user.email "example@example.com"
```

上記のコマンドで完了です。Yournameとexample@example.comには各自適当な情報を入力してください。

次に必須ではありませんが、公開鍵認証をしようしようと思うのでsshキーを作成します。

```bash
$ cd ~/.ssh
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/data/data/com.termux/files/home/.ssh/id_rsa): ←鍵の保存先
Enter passphrase (empty for no passphrase):　←パスフレーズを入力
Enter same passphrase again:  ←入力したパスフレーズの確認
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.
```
対話式で色々聞かれますが、基本的にはデフォルトのままで大丈夫だと思います。

```bash
$ ls
id_rsa  id_rsa.pub
```
id_rsaが秘密鍵、id_rsa.pubが公開鍵です。

秘密鍵は絶対に他社に公開しないでください。

cat等で公開鍵の中身を表示しコピーしgithubの設定の「SSH and GPG keys」に移動します。

緑の「New ssh key」というボタンを押すと以下のような画面が表示されると思います。

![github-screenshot](https://uploda1.ysklog.net/uploda/f406a459e5.png)

titleに任意の名前を入力してもらい、keyに先程コピーした公開鍵を入力します。

そして「Add SSH key」のボタンを押せばSSHキーの追加は完了です。

```
$ ssh -T git@github.com
Hi xdcyw! You've successfully authenticated, but GitHub does not provide shell access.
```
のような応答が返ってくればSSHキーは正しく設定できています。

失敗するような場合は今までの手順を見直してみてください。

では次にgithubからhugoのプロジェクトをクローンします。

```
$ git clone git@github.com:/[username]/[リポジトリ名].git
```


[username]と[リポジトリ名]は各自適当な情報を入力してください。

クローンが成功したら、そのディレクトリに移動します。


```bash
$ ls
[リポジトリ名]
$ cd [リポジトリ名]
```

これで基本的には終了です。

```bash
$ hugo server
```
などを実行して、localhost:1313にスマホのブラウザからhugoのサイトが見れるか確認してください。

あとは、PC等でhugoを使うときと同じように使えると思います。

最後にマークダウンをviやnanoで編集することもできますが、それでは不便かと思いますので
```bash
termux-setup-storage
```
を実行すると、ファイルマネージャーからアクセスができます。

そのため任意のAndroid用テキストエディタでマークダウンを編集できると思います。

質問等がありましたら、[このページ](/profile/profile)にある連絡先に連絡してもらえれば可能な限り回答します。

おわり。