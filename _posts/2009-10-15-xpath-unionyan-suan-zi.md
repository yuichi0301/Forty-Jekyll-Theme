---
layout: post
title: XQueryの勉強・XPath Union演算子
description: XQueryの勉強・XPath Union演算子
---
1.今回はXPathのunion演算子の勉強をしてみます。
union演算子はシーケンスの和を返します。
ただ単にシーケンスの和を返すのではなく重複を排除します。

2.union演算子を含むXPathを含んだXQueryの実行。
XQueryは次のものになります。

```xquery
for $res in doc("test1.xml")/othello/number
union doc("test1.xml")/othello/place
return $res
```




3.実行結果
ちゃんとnumber要素とplace要素をを合わせたシーケンスが返ってきました。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<number>001</number>
<place>長崎</place>
```


4.要素が重複する場合のXQuery
要素が重複するXQueryは次のものになります。


```xquery
for $res in doc("test1.xml")/othello/*[. << ../white_count]
union doc("test1.xml")/othello/*[. >> ../date]
return $res
```




①white_count要素より先に現れる全ての要素

```xquery
for $res in doc("test1.xml")/othello/*[. << ../white_count]
return $res
```




```xml
<?xml version="1.0" encoding="UTF-8"?>
<number>001</number>
<date>2009-03-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
```


②date要素より後に現れる全ての要素

```xquery
for $res in doc("test1.xml")/othello/*[. >> ../date]
return $res
```



```xml
<?xml version="1.0" encoding="UTF-8"?>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
<white_count>28</white_count>
<win>black</win>
```



これら二つのクエリの実行結果をunionで結合します。

![image]({{site.baseurl}}/assets/images/2009_10_3/XPathUnion1.jpg)

5.実行結果
きちんと重複が排除されてセレクトされました。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<number>001</number>
<date>2009-03-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
<white_count>28</white_count>
<win>black</win>
```
