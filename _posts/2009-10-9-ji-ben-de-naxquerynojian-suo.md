---
layout: post
title: XQueryの勉強・基本的なXQueryの検索
description: XQueryの勉強・基本的なXQueryの検索
---
それでは前回作成したテーブルを検索してみたいと思います。
検索を実行するにはコントロールセンターが便利です。
全てのプログラムのIBM DB2の中にあるので起動します。
スプラッシュの画面は結構かっこいいです。

![image]({{site.baseurl}}/assets/images/2009_10_3/control_center.jpg)

起動したら今度はコマンドエディタを開きます。

![image]({{site.baseurl}}/assets/images/2009_10_3/command_editor_menu.jpg)

コマンドエディタが起動したらTEST_DBに接続するために下の画像にある追加ボタンを押下します。

![image]({{site.baseurl}}/assets/images/2009_10_3/command_editor_add-1.jpg)

TEST_DBを選択してOKボタンを押下します。
特にパスワード等は設定していないので入力する必要はないです。

![image]({{site.baseurl}}/assets/images/2009_10_3/db_connect.jpg)

上のテキスト入力欄に次のように入力し、実行ボタンを押下します。

xquery

```xquery		
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othello
return $result
```

![image]({{site.baseurl}}/assets/images/2009_10_3/select1.jpg)
