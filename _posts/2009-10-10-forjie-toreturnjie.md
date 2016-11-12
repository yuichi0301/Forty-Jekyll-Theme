---
layout: post
title: XQueryの勉強・for節とreturn節
description: XQueryの勉強・for節とreturn節
---
前回のXQueryの解説です。
XQueryの基本構文はフラワー式と呼ばれています。
これはSQLでいうSELECT,FROM,WHERE,ORDER BYに相当します。

```xquery
for $変数 in シーケンス
let $変数 in シーケンス
where 条件式
order by ソート条件
return 出力式
```


前回のXQueryは下記のような内容でした。



```xquery
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othello
return $result
```


これは次のような意味になります。

![image]({{site.baseurl}}/assets/images/2009_10_3/for_and_return.jpg)

1.①のXPathを評価した結果のシーケンス。
2.1.の結果の先頭のアイテムが②の変数にバインドされます。
3.変数を含んだ③のコンストラクタが評価されます。
4.これ以降1.～3.を繰り返しフラワー式の評価結果になります。

※ちなみに、OTHELLO.OTHELLO_MANAGEMENT.OTHELLOの部分は大文字でないといけません。
