---
layout: post
title: XQueryの勉強・XPathの比較式で面倒な部分
description: XQueryの勉強・XPathの比較式で面倒な部分
---
今回はXPathの比較式でめんどくさい部分をまとめてみます。
1.値比較式
単一の値同士の比較を行う式です。
```xquery
eq ne lt le gt ge
```

2.一般比較式
単一の値を含めたシーケンス同士の比較を行う式です。
```xquery
= != < <= > >=
```

3.めんどくさい部分
値比較式の場合、比較するオペランドが数値型の場合でも型変換はされず比較されるので、文字列の場合はエラーになります。
一般比較式の場合、比較するオペランドが数値型の場合double型に変換し比較され正常に比較されます。

4.試してみる
値比較式を含んだXQueryは以下のクエリになります。

```xquery
for $res in doc("test1.xml")/othello[white_count lt 29]
return $res
```



実行するとエラーになります。
```log
Warning: on line 1 of *module with no systemId*:
Comparison of xs:untypedAtomic? to xs:integer will fail unless the first operand is empty
Warning: on line 1 of *module with no systemId*:
Comparison of xs:untypedAtomic? to xs:integer will fail unless the first operand is empty
Error on line 1 of *module with no systemId*:
XPTY0004: Cannot compare xs:untypedAtomic to xs:integer
net.sf.saxon.trans.XPathException: Cannot compare xs:untypedAtomic to xs:integer
```
一般比較式を含んだXQueryは以下のクエリになります。

```xquery
for $res in doc("test1.xml")/othello[white_count < 29]
return $res
```



実行するとこちらはdouble型に変換され数値として比較した結果が返ります。
