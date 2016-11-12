---
layout: post
title: VosaoからGhostに移行しました！
description: VosaoからGhostに移行しました！
---
1.Ghostとは
GhostとはNode.jsでできたブログシステムになります。

2.GAEで使えるvosaoから移行しました。
![image]({{site.baseurl}}/assets/images/2009_10_3/vosao.png)


3.Ghostのいい点

- markdownで書けるのでサクサク書ける
- Node.js
- かっこいい
- シンプルなのに不便に感じない
- コントロール+sで保存できる

4.構築手順

1)AWSでインスタンスを作ります。
Dockerの人が勧めているのがubuntuらしいのでubuntuにしました。

2)Dockerのサイトに書いてあるインストール手順にそってDockerをインストールします。
https://docs.docker.com/installation/ubuntulinux/

```shell
sudo apt-get update
sudo apt-get install docker.io
source /etc/bash_completion.d/docker.io
sudo sh -c "echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
sudo apt-get update
sudo apt-get install lxc-docker
```

3)次にGhostをpullします。
```shell
sudo docker pull dockerfile/ghost
```

4)Ghostを起動します。
```shell
sudo docker run -v /home/ubuntu/shared:/shared -d -p 80:2368 dockerfile/ghost
```

ここで重要なのが`-v /home/ubuntu/shared:/shared`この部分

これを入れておくとホストの`/home/ubuntu/shared`とコンテナの`/shared`を共有してくれます。

以上で作成完了です！
