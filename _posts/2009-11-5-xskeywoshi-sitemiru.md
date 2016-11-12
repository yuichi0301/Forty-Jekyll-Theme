---
layout: post
title: XML Schemaの勉強・xs:keyを試してみる
description: XML Schemaの勉強・xs:keyを試してみる
---
1.スキーマ
スキーマは次のスキーマになります。

key.xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="othello" type="OthelloType">
		<xs:key name="placekey">
			<xs:selector xpath="placelist/place" />
			<xs:field xpath="@no" />
		</xs:key>
	</xs:element>
	<xs:complexType name="OthelloType">
		<xs:sequence>
			<xs:element ref="placelist" maxOccurs="unbounded" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="placelist" type="PlacelistType" />
	<xs:complexType name="PlacelistType">
		<xs:sequence>
			<xs:element ref="place" maxOccurs="unbounded" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="place">
		<xs:complexType>
			<xs:simpleContent>
				<xs:extension base="xs:string">
					<xs:attribute name="no" type="xs:string" use="required" />
				</xs:extension>
			</xs:simpleContent>
		</xs:complexType>
	</xs:element>
</xs:schema>
```

2.妥当なXML
妥当なXMLは次のXMLになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="key.xsd">
	<placelist>
		<place no="1">nagasaki</place>
		<place no="2">tokyo</place>
		<place no="3">saitama</place>
		<place no="4">saga</place>
		<place no="5">nagano</place>
	</placelist>
</othello>
```

place要素のno属性は一意になっており、妥当性検証を通過します。

3.妥当でないXML
妥当ではないXMLは次のXMLになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="key.xsd">
	<placelist>
		<place no="1">nagasaki</place>
		<place no="2">tokyo</place>
		<place no="2">saitama</place>
		<place no="4">saga</place>
		<place no="5">nagano</place>
	</placelist>
</othello>
```


place要素のno属性で2が2回指定してあるため重複しています。
検証の結果「要素 "othello" の識別制約に宣言されたキー値 [2] が重複しています。」と出力されます。
