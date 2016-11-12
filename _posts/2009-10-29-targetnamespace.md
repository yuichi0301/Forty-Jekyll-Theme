---
layout: post
title: XML Schemaの勉強・##targetNamespace
description: XML Schemaの勉強・##targetNamespace
---
1.##targetNamespaceを試してみる
このキーワードを指定すると対象名前空間に属さないとエラーになります。

2.まずは対象名前空間に属する場合

用意するXMLは以下のものです。

xml1.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<tn:othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="urn:nagasaki:yuichi:othello schema1.xsd" xmlns:tn="urn:nagasaki:yuichi:othello">
	<tn:game>
		<tn:player>yuichi</tn:player>
	</tn:game>
</tn:othello>
```

XMLスキーマは以下のものです。
schema1.xsd

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
	targetNamespace="urn:nagasaki:yuichi:othello" xmlns:tn="urn:nagasaki:yuichi:othello">
	<xs:element name="othello" type="tn:OthelloType" />
	<xs:complexType name="OthelloType">
		<xs:sequence>
			<xs:element ref="tn:game" maxOccurs="unbounded" />
		</xs:sequence>
	</xs:complexType>
	<xs:element name="game" type="tn:GameType" />
	<xs:complexType name="GameType">
		<xs:sequence>
			<xs:any namespace="##targetNamespace" processContents="skip" />
		</xs:sequence>
	</xs:complexType>
</xs:schema>
```

player要素をanyの対象にします。
上記のXMLではplayer要素は対象名前空間に属するため、この妥当性検証は通ります。

3.対象名前空間に属さない場合

```xml
<?xml version="1.0" encoding="UTF-8"?>
<tn:othello xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="urn:nagasaki:yuichi:othello schema1.xsd" xmlns:tn="urn:nagasaki:yuichi:othello">
	<tn:game>
		<player>yuichi</player>
	</tn:game>
</tn:othello>
```

player要素からtn:をはずして実行します。

この場合やはりエラーになります。
