---
layout: post
title: JAXBの勉強・xjc実行！
description: JAXBの勉強・xjc実行！
---
# 1.Java6でアプリケーションを作成する
Java6からJAXBの機能が標準で入っていますので、そのまま実行できます。

C:\testにweatherforecast.xsdを配置し、コマンドプロンプトを立ち上げます。
コマンドプロンプトで次のコマンドを実行します。

まずはC:\testに移動します。

cd C:\test

xjcコマンドを実行します。
xjc weatherforecast.xsd

C:\testにgeneratedディレクトリが作成され、その中にいくつかのJavaのクラスが作成されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/1-2.jpg)
