---
layout: post
title: XML Schemaの勉強・strict
description: XML Schemaの勉強・strict
---
1.strictを試してみる
このキーワードを指定するとanyの対象となる定義は存在する必要があり、
かつその定義について妥当である必要があります。

2.スキーマ
スキーマは以下のスキーマになります。
schema4.xsd

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
			<xs:any namespace="##local" processContents="strict" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="player" type="xs:string" />
</xs:schema>
```


3.妥当なXML
妥当なXMLは以下のXMLになります。
xml4.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="schema4.xsd">
	<game>
		<player>yuichi</player>
	</game>
</othello>
```

game要素の中にはplayer要素があり、その定義は存在しかつ
定義に対して妥当なため、妥当性検証を通過します。

4.定義が存在しない場合
定義が存在しない場合のスキーマは以下のスキーマになります。
schema4.xsd(内容変更版)

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
			<xs:any namespace="##local" processContents="strict" />
		</xs:sequence>
	</xs:complexType>
</xs:schema>
```



player要素の定義が存在しないためエラーになります。
次のように出力されました。
「cvc-complex-type.2.4.c: 一致している wildcard は strict ですが、要素 'player' の宣言が見つかりません。」

5.定義されている内容に対して妥当でない場合
定義は存在しているが、それに対して妥当でないスキーマは以下のスキーマになります。
schema4.xsd(内容変更版)

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
			<xs:any namespace="##local" processContents="strict" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="player" type="xs:date" />
</xs:schema>
```

player要素は日付型で定義されているのに、文字列型のXMLであるため
エラーになります。

次のように出力されました。
「エラー: 5行目
cvc-datatype-valid.1.2.1: 'yuichi' は 'date' の有効な値ではありません。
エラー: 5行目
cvc-type.3.1.3: 要素 'player' の値 'yuichi' が無効です。」
