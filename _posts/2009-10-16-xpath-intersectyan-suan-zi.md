---
layout: post
title: XQueryの勉強・XPath Intersect演算子
description: XQueryの勉強・XPath Intersect演算子
---
1.今回はXPathのintersect演算子の勉強をしてみます。
intersect演算子はシーケンスの積を返します。

2.intersect演算子を含むXPathを含んだXQueryの実行。
要素が重複するXQueryは次のものになります。

```xquery
for $res in doc("test1.xml")/othello/*[. << ../white_count]
intersect doc("test1.xml")/othello/*[. >> ../date]
return $res
```

![image]({{site.baseurl}}/assets/images/2009_10_3/XPathUnion1-1.jpg)


3.実行結果
きちんと二つのシーケンスに同じように含まれる要素が出力されました。


```xml
<?xml version="1.0" encoding="UTF-8"?>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
```
