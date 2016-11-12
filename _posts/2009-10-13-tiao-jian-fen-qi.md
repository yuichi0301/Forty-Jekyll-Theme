---
layout: post
title: XQueryの勉強・条件分岐
description: XQueryの勉強・条件分岐
---
1.今回は条件分岐を試してみます。
オセロの勝敗のXMLを出力してみます。
othello要素の子要素win要素がblackならwin要素の中に黒、whiteなら白を出力してみます。

実行するコマンドは以下のコマンドになります。

```xquery
<results>
{
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othelloList/othello
return
<win>
{
if($result/win="black")
then "黒"
else
if($result/win="white")
then "白"
else ""
}
</win>
}
</results>
```

条件式はif then elseによって作ります。
elseifはないため、elseの中にさらに条件式を書くことでelseifを作ります。
結果は次のようになりました。

```xml
<results>
	<win>
		黒
	</win>
	<win>
		黒
	</win>
	<win>
		白
	</win>
	<win>
		黒
	</win>
	<win>
		黒
	</win>
	<win>
		黒
	</win>
</results>
```

1 レコードが選択されました。
