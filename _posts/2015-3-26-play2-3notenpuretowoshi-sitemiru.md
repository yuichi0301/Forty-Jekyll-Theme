---
layout: post
title: Play2.3のテンプレートを試してみる
description: Play2.3のテンプレートを試してみる
---
Playframeworkでテンプレートを試してみたら、すごく使いやすかったので手順を書いていきます。

#1.プロジェクト作成コマンドの実行


    $ activator new

どのテンプレートにするか聞かれます。
以下のサイトから使いたいテンプレートを探します。
(チャットなど使ってみたいテンプレートがたくさんあります。)

http://typesafe.com/activator/templates

今回は「computer-database-scala」を使ってみます。

    $ computer-database-scala


Enter a name for your application (just press enter for 'computer-database-scala')

名前を聞かれるので適当に入力します。


    $ computers


#2.実行してみる

    $ cd computers
    $ activator
    $ run

以下のURLをブラウザで開きます。

http://localhost:9000/

こういう画面が表示されます。
「Apply this script now!」を押すと表示されている必要なテーブルやデータをH2データベースに登録してくれるみたいです。

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-34-46.png)

「Apply this script now!」を押すと最終的な画面が表示されます。

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-36-46.png)

#3.InteliJで開いてみる

import Projectを押下します。

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-39-19.png)

先ほど作成したプロジェクトを選択します。

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-40-16.png)

Import project from external modelを選択し、SBTを選択しNEXT

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-40-53.png)

Finishを押下します。

これでデータベース関連のソースを参考にできます！

![image]({{site.baseurl}}/assets/images/2015_3_26/----------2015-03-26-1-44-40.png)
