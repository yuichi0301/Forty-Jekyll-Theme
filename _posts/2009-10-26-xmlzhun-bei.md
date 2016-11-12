---
layout: post
title: XML Schemaの勉強・準備
description: XML Schemaの勉強・準備
---
1.はじめに
XMLSchemaのなんだか面倒だと思う部分について復習していこうと思います。

2.Javaのクラスの準備
基本的にはJavaでSAXを使って実行していこうと思います。
Javaのクラスの準備はとても簡単です。
こちら のサイトに書いてあるクラスをそのままコピーします。
あとはJavaの6ならもうおしまいで特に必要なjarファイルなどはありません。
もしコンパイルが通らないバージョンなら別途jarファイルを通す必要があります。

3.XMLの準備
準備するXMLは次のXMLです。

Test.xml
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



今回は名前空間とかは考慮したくなかったのでnoNamespaceSchemaLocation属性でスキーマの場所を指定しています。

4.XMLSchemaの準備
準備するXMLスキーマは次のXMLスキーマです。

Test.xsd

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
</xs:schema>
```

5.妥当性検証を実行する。

①Cドライブの直下にtestというフォルダを作って上記2つのファイルを置きます。

②ファイルメニューの実行を押下します。

![image]({{site.baseurl}}/assets/images/2009_10_3/XmlSchema01.jpg)

③構成の実行を押下します。

![image]({{site.baseurl}}/assets/images/2009_10_3/XmlSchema02.jpg)

④Javaアプリケーションを選択し、右クリックし新規を選択します。

![image]({{site.baseurl}}/assets/images/2009_10_3/XmlSchema03.jpg)

⑤引数タブを選択し、「C:\test\Test.xml」と入力します。

![image]({{site.baseurl}}/assets/images/2009_10_3/XmlSchema04.jpg)

⑥実行ボタンを押下します。

⑦コンソールに妥当性検証した結果が表示されます。

![image]({{site.baseurl}}/assets/images/2009_10_3/XmlSchema05.jpg)
