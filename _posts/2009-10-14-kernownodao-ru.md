---
layout: post
title: XQueryの勉強・Kernowの導入
description: XQueryの勉強・Kernowの導入
---
なんだかXQueryやXPathの勉強をするだけでXMLDBを使うのはめんどうになってきたので、
KernowというXMLを読み込んでXQueryを実行したり出来るツールを使って勉強していくことにします。

1.ダウンロード
ダウンロードは [こちら](http://sourceforge.net/project/showfiles.php?group_id=161018) からダウンロードして下さい。
ダウンロードが完了したら適当なディレクトリに解凍したら完了です。

2.使ってみる
なぜか日本語のディレクトリがパスに入るとエラーになったり、ディレクトリをはさむとエラーになったので、
Kernow.exeのあるディレクトリに直接test1.xmlファイルを作ります。
XMLファイルの内容は以下のものにします。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<othello>
	<number>001</number>
	<date>2009-03-07</date>
	<place>長崎</place>
	<black_player>yuichi</black_player>
	<black_count>36</black_count>
	<white_player>takesi</white_player>
	<white_count>28</white_count>
	<win>black</win>
</othello>
```


実行するXQueryは次のXQueryにします。

```xquery
for $res in doc("test1.xml")/othello/number
return $res
```

![image]({{site.baseurl}}/assets/images/2009_10_3/kernow1.jpg)

きちんとセレクトされました。
