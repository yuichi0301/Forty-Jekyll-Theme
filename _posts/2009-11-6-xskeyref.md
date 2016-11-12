---
layout: post
title: XML Schemaの勉強・xs:keyref
description: XML Schemaの勉強・xs:keyref
---
1.前置き
keyrefはkey要素で定義したkeyに対しての参照を定義出来ます。
key要素で定義されていないものを参照しようとするとエラーになります。

2.定義仕方

以下のようにして定義します。

```xml
<xs:keyref name="キー参照の名前" ref="参照するキーの名前">
	<xs:selector xpath="キー参照元に指定するものの範囲" />
	<xs:field xpath="キー参照元になる項目" />
</xs:keyref>
```
