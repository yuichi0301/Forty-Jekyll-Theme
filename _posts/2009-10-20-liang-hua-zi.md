---
layout: post
title: XQueryの勉強・量化子
description: XQueryの勉強・量化子
---
1.前置き
今回は量化子(Quantified Expression)の勉強をしてみます。
量化子は２つの式を評価し、条件を満たす場合にブール値を返すというものです。

2.量化子の種類
量化子は存在量化子を使った式と全称量化子を使った式の２種類があります。
①存在量化子を使った式は、シーケンスのうち１つでも条件に一致すればture、そうでなければfalseを返します。(someを使う。)
②全称量化子を使った式は、シーケンスのうち全てが一致すえばtrue、そうでなければfalseを返します。(everyを使う。)

3.準備
次のXMLを準備します。
test4.xml

```xml
<othelloList>
	<othello name="takeshi">
		<result>win</result>
		<result>lose</result>
		<result>win</result>
	</othello>
	<othello name="yuichi">
		<result>win</result>
		<result>win</result>
		<result>win</result>
	</othello>
	<othello name="tetu">
		<result>lose</result>
		<result>lose</result>
		<result>lose</result>
	</othello>
</othelloList>
```




4.存在量化子を使ったXQueryの実行
存在量化子を使ったXQueryは以下のクエリになります。

```xquery
for $result in doc("test4.xml")/othelloList/othello[some $d in result
satisfies $d eq "win"]
return
<result>{$result}</result>
```



5.存在量化子を使ったXQueryの実行結果
以下のようになりました。
winが１つでも含まれれば出力され、１つも含まない場合は出力されませんでした。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<result>
	<othello name="takeshi">
		<result>win</result>
		<result>lose</result>
		<result>win</result>
	</othello>
</result>
<result>
	<othello name="yuichi">
		<result>win</result>
		<result>win</result>
		<result>win</result>
	</othello>
</result>
```



6.全称量化子を使ったXQueryの実行
存在量化子を使ったXQueryは以下のクエリになります。

```xquery
for $result in doc("test4.xml")/othelloList/othello[every $d in result
satisfies $d eq "win"]
return
<result>{$result}</result>
```



7.全称量化子を使ったXQueryの実行結果
以下のようになりました。
全てがwinになっているものしか出力されませんでした。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<result>
	<othello name="yuichi">
		<result>win</result>
		<result>win</result>
		<result>win</result>
	</othello>
</result>
```
