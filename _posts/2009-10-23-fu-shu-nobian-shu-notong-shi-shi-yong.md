---
layout: post
title: XQueryの勉強・複数の変数の同時使用
description: XQueryの勉強・複数の変数の同時使用
---
1.今回はfor節で複数の変数を同時に宣言した場合の動作について勉強してみます。
複数の変数を同時に宣言した場合は変数にバインドされたシーケンスの全ての組み合わせになります。

2.実行してみる。
実行するクエリは以下のクエリになります。

```xquery
for $res1 in ("a","b"),$res2 in ("c","d")
return
<result>{$res1,$res2}</result>
```



3.結果
実行結果は以下のようになりました。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<result>a c</result>
<result>a d</result>
<result>b c</result>
<result>b d</result>
```



ちなみにこれは次のクエリを実行した場合と同じ意味になります。

```xquery
for $res1 in ("a","b")
for $res2 in ("c","d")
return
<result>{$res1,$res2}</result>
```



つまり、
①res1のシーケンスの１つ目を取り出す。
②res2のシーケンスの１つ目を取り出す。
③returnでres1のシーケンスの１つ目とres2のシーケンスの１つ目を表示する。
④res2のシーケンスの２つめを取り出す。
⑤returnでres1のシーケンスの１つ目とres2のシーケンスの２つ目を表示する。
⑥res1のシーケンスの２つ目を取り出す。
⑦res2のシーケンスの１つ目を取り出す。
⑧returnでres1のシーケンスの２つ目とres2のシーケンスの１つ目を表示する。
・・・。
という流れになっていきます。
