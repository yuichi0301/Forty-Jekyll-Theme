---
layout: post
title: XML Schemaの勉強・要素の置き換え(substitutionGroup)
description: XML Schemaの勉強・要素の置き換え(substitutionGroup)
---
1.今回はsubstitutionGroup属性を使った要素の置き換えについて勉強してみます。
substitutionGroup属性を使うことで既にある要素に対してそれを置き換える要素を
定義することが出来ます。

2.XmlSchema
今回使用するXmlSchemaは以下のXmlSchemaになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="othello" type="OthelloType" />
	<xs:complexType name="OthelloType">
		<xs:sequence>
			<xs:element ref="game" maxOccurs="unbounded" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="game" type="GameType" />
	<xs:complexType name="GameType">
		<xs:sequence>
			<xs:element name="date" type="xs:date" />
			<xs:element name="place" type="xs:string" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="reversi" type="OthelloType"
		substitutionGroup="othello" />
</xs:schema>
```

3.XmlSchemaの意味
下記の赤枠部のreversi要素がsubstitutionGroup属性でothello要素を指定することで、
othello要素はreversi要素との置き換えが可能になります。

![image]({{site.baseurl}}/assets/images/2009_10_3/SubstitutionGroup.jpg)

4.試してみる
まずは普通にothello要素で試してみます。
SubstitutionGroup.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="Test.xsd">
	<game>
		<date>2009-01-01</date>
		<place>nagasaki</place>
	</game>
	<game>
		<date>2008-01-01</date>
		<place>saga</place>
	</game>
</othello>
```

これは当然問題なく妥当性検証通過します。

次にothello要素をreversi要素に置き換えたXMLで実行してみます。
SubstitutionGroup2.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<reversi xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="Test.xsd">
	<game>
		<date>2009-01-01</date>
		<place>nagasaki</place>
	</game>
	<game>
		<date>2008-01-01</date>
		<place>saga</place>
	</game>
</reversi>
```

こちらも問題なく妥当性検証を通りました。
ということで置き換えは成功しました。

ちなみにこの置き換えを実行する際、置き換える要素、置き換えられる要素の両方がグローバル宣言されている必要があります。
