---
layout: post
title: GAEの勉強・まずはHello World!
description: GAEの勉強・まずはHello World!
---
1.プロジェクトの作成
メニューのファイル→新規→Webアプリケーション・プロジェクトを選択します。

![image]({{site.baseurl}}/assets/images/2009_10_3/5.jpg)

下記の状態にして完了を押します。
プロジェクト名：HelloWorld
パッケージ：helloworld
Google Webツールキットを使用：チェックをはずす
Google Appエンジンを使用する：チェックをつける

![image]({{site.baseurl}}/assets/images/2009_10_3/6.jpg)

以下のようなディレクトリ構成が作成されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/7.jpg)

2.実行する
実行するために、メニューの実行→実行の構成を選択します。

![image]({{site.baseurl}}/assets/images/2009_10_3/8.jpg)

Web アプリケーションのHelloWorldを選択し実行をおします。

![image]({{site.baseurl}}/assets/images/2009_10_3/9.jpg)

http://localhost:8080/ にアクセスすると次のように動いてるアプリケーションが表示されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/10.jpg)

リンクをクリックしてhttp://localhost:8080/helloworld にアクセスすると
作成したHelloWorldアプリケーションが動いてHello,worldが表示されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/12.jpg)

3.世界にお披露目する
HelloWorldを世界にお披露目しても仕方ないですが、
ここまでしないと完了といえないのでここまでやります。

しかし、今現在アプリケーションは削除出来ず、最大10個まででその1つを
HelloWorldに費やすことになるらしいです。

http://appengine.google.com/ でグーグルにログインします。

Create an Applicationボタンをおします。

![image]({{site.baseurl}}/assets/images/2009_10_3/13.jpg)

後は手順に従ってアプリケーション識別子を取得すればOK
(途中で携帯のメールアドレスを入力したりするとこがあります。@より前の名称を入力してください。)

appengine-web.xmlを開きapplication要素に取得したアプリケーション識別子を入力します。

![image]({{site.baseurl}}/assets/images/2009_10_3/17.jpg)

メニューにある飛行機マークをおします。

![image]({{site.baseurl}}/assets/images/2009_10_3/18.jpg)

Googleに登録したメールアドレスとパスワードを入力し配置ボタンを押します。

![image]({{site.baseurl}}/assets/images/2009_10_3/19.jpg)

登録したURLにアクセスします。http://yuichi-helloworld.appspot.com/

![image]({{site.baseurl}}/assets/images/2009_10_3/20.jpg)

リンクをクリックしてHello,worldが表示されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/21.jpg)

予想以上に簡単に出来ました。
