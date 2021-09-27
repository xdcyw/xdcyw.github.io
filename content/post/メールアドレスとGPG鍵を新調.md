---
title: "メールアドレスとGPG鍵を新調"
date: 2021-09-28T02:47:59+09:00
draft: false
---

メールアドレスを新調しました。

新しいメールアドレスは[mail@xdcyw.jp]です。

また、メールアドレスの新調に合わせてGPG鍵も新調しました。以下のコマンドでインポート可能です。

```git
gpg --fetch-keys https://github.com/xdcyw.gpg
or
curl https://github.com/xdcyw.gpg | gpg --import
```
