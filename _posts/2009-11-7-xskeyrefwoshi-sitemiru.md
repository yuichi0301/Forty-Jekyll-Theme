---
layout: post
title: XML Schemaの勉強・xs:keyrefを試してみる。
description: XML Schemaの勉強・xs:keyrefを試してみる。
---
1.スキーマ
スキーマは次のスキーマになります。
keyref.xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="othello" type="OthelloType">
		<xs:key name="placekey">
			<xs:selector xpath="placelist/place" />
			<xs:field xpath="@no" />
		</xs:key>
		<xs:keyref name="placekeyref" refer="placekey">
			<xs:selector xpath="playerlist/player" />
			<xs:field xpath="@placeno" />
		</xs:keyref>
	</xs:element>
	<xs:complexType name="OthelloType">
		<xs:sequence>
			<xs:element ref="placelist" maxOccurs="unbounded" />
			<xs:element ref="playerlist" maxOccurs="unbounded" />
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
	<xs:element name="playerlist" type="PlayerlistType" />
	<xs:complexType name="PlayerlistType">
		<xs:sequence>
			<xs:element ref="player" maxOccurs="unbounded" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="player">
		<xs:complexType>
			<xs:simpleContent>
				<xs:extension base="xs:string">
					<xs:attribute name="placeno" type="xs:string" use="required" />
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
	xsi:noNamespaceSchemaLocation="keyref.xsd">
	<placelist>
		<place no="1">nagasaki</place>
		<place no="2">tokyo</place>
		<place no="3">saitama</place>
		<place no="4">saga</place>
		<place no="5">nagano</place>
	</placelist>
	<playerlist>
		<player placeno="3">yuichi</player>
		<player placeno="2">takesi</player>
		<player placeno="1">cr</player>
		<player placeno="5">ryuichi</player>
		<player placeno="4">ryuichi</player>
		<player placeno="5">ryuichi</player>
	</playerlist>
</othello>
```


player要素のplaceno属性の属性値は
全てplace要素のno属性の属性値を参照しているため妥当です。

3.妥当でないXML
妥当ではないXMLは次のXMLになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="keyref.xsd">
	<placelist>
		<place no="1">nagasaki</place>
		<place no="2">tokyo</place>
		<place no="3">saitama</place>
		<place no="4">saga</place>
		<place no="5">nagano</place>
	</placelist>
	<playerlist>
		<player placeno="3">yuichi</player>
		<player placeno="2">takesi</player>
		<player placeno="1">cr</player>
		<player placeno="5">ryuichi</player>
		<player placeno="6">ryuichi</player>
		<player placeno="5">ryuichi</player>
	</playerlist>
</othello>
```

player要素のplaceno属性の属性値「6」は
place要素のno属性にない属性値になるためエラーになります。
検証の結果「要素 'othello' の識別制約に応じた値 '6' を持つキー 'placekeyref' が見つかりませんでした。」と出力されます。
