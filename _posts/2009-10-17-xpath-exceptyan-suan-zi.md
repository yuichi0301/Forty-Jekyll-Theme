---
layout: post
title: XQueryの勉強・XPath Except演算子
description: XQueryの勉強・XPath Except演算子
---
1.今回はXPathのexcept演算子の勉強をしてみます。
except演算子はシーケンスの差を返します。

2.except演算子を含むXPathを含んだXQueryの実行。
XQueryは次のものになります。

```xquery
for $res in doc("test1.xml")/othello/*[. << ../white_count]
except doc("test1.xml")/othello/*[. << ../place]
return $res
```


このクエリの実行によるシーケンスから

```xquery
for $res in doc("test1.xml")/othello/*[. << ../white_count]
return $res
```


このクエリの実行によるシーケンスの差が結果のシーケンスになります。

```xquery
for $res in doc("test1.xml")/othello/*[. << ../place]
return $res
```

![image]({{site.baseurl}}/assets/images/2009_10_3/xpathExcept-1.jpg)


3.実行結果
きちんと二つのシーケンスに同じように含まれる要素が出力されました。


```xml
<?xml version="1.0" encoding="UTF-8"?>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
```
