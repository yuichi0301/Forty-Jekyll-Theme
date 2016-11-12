---
layout: post
title: XQueryの勉強・コンストラクタ
description: XQueryの勉強・コンストラクタ
---
1.前置き
今回はXQueryのコンストラクタの勉強をしてみます。
コンストラクタはノードを生成する式のことです。


```xquery
for $result in doc("test4.xml")/othelloList/othello
return
<result>{$result}</result>
```

↑ ↑ 上記のクエリではこの中かっこの部分になります。

2.要素ノードを作るコンストラクタ
要素ノードを作るコンストラクタは次のような書き方になります。
```xquery
element 要素名{}
```

3.属性ノードを作るコンストラクタ
属性ノードを作るコンストラクタは次のような書き方になります。
```xquery
attribute 属性名{}
```

4.実際に試してみる。
実際に試してみます。
実行するクエリは下記のクエリになります。

```xquery
element othelloList{
	element othello{
		attribute date{"2009.05.28"},
		"othello date"
	}
}
```




5.実行結果
次のようにノード、属性が生成され、XMLが出力されました。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othelloList>
	<othello date="2009.05.28">othello date</othello>
</othelloList>
```
