---
layout: post
title: XQueryの勉強・重複排除
description: XQueryの勉強・重複排除
---
1.今回はSQLでよく使うDISTINCT、重複排除を勉強してみます。
用意するのは次のXMLファイルになります。

test2.xml

```xml
<?xml version="1.0" encoding="utf-8" ?>
<othello>
	<taisenkansou aite="たけし">
		<kansou>強い</kansou>
		<kansou>うまい</kansou>
		<kansou>虎定石</kansou>
	</taisenkansou>
	<taisenkansou aite="ゆういち">
		<kansou>強い</kansou>
		<kansou>うまい</kansou>
		<kansou>ねずみ定石</kansou>
	</taisenkansou>
</othello>
```


2.XQueryの実行
実行するのは以下のXQueryになります。

```xquery
for $x in distinct-values(doc("test2.xml")/othello/taisenkansou/kansou)
return $x
```


3.実行結果
実行結果は次のように重複が排除された状態になります。

```xml
<?xml version="1.0" encoding="UTF-8"?>強い うまい 虎定石 ねずみ石
```

4.応用例
これは子要素により親要素を集約する際に使うことが出来ます。

```xquery
for $kansou in
distinct-values(doc("test2.xml")/othello/taisenkansou/kansou)
return
```



```xquery
for $taisenkansou in doc("test2.xml")/othello/taisenkansou[kansou =
$kansou]
return <kansou naiyou="{$kansou}"
aite="{$taisenkansou/@aite}"></kansou>
```



実行結果

```xml
<?xml version="1.0" encoding="UTF-8"?>
<kansou aite="たけし" naiyou="強い"/>
<kansou aite="ゆういち" naiyou="強い"/>
<kansou aite="たけし" naiyou="うまい"/>
<kansou aite="ゆういち" naiyou="うまい"/>
<kansou aite="たけし" naiyou="虎定石"/>
<kansou aite="ゆういち" naiyou="ねずみ石"/>
```
