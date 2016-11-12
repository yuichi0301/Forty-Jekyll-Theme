---
layout: post
title: XQueryの勉強・forとletで面倒な部分
description: XQueryの勉強・forとletで面倒な部分
---
1.前置き
今回はfor節とlet節の面倒な部分の紹介です。
for節とlet節の違いは以前紹介しましたが、他に忘れやすい違いがあります。
それはシーケンスがない場合return節まで実行されるかどうかです。

2.for節の場合
実行するクエリは以下のクエリになります。


```xquery
for $res1 in fn:doc("test1.xml")/test
return
<result>{$res1}</result>
```

ここでtestというノードを指定していますが、このノードはXML中にはありません、
つまりこのパスによっては何も取得されません。
(SQLではない項目を指定するとエラーになりますがXQueryの場合はなりません。これは大きな違い。)
このクエリの実行結果は以下のようになりました。

```xml
<?xml version="1.0" encoding="UTF-8"?>
```


XML宣言のみです、つまりreturn節は実行されませんでした。

3.let節の場合
実行するクエリは以下のクエリになります。


```xquery
let $res1 := fn:doc("test1.xml")/test
return
<result>{$res1}</result>
```




このクエリの実行結果は以下のようになりました。


```xml
<?xml version="1.0" encoding="UTF-8"?>
<result/>
```


```<result/>```まで出力されました。
つまりreturn節まで実行されています。
理由はわからないけどこういう微妙な違いもあります。
