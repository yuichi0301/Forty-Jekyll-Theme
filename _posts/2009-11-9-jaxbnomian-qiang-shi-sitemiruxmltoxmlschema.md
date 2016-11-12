---
layout: post
title: JAXBの勉強・試してみるXMLとXMLSchema
description: JAXBの勉強・試してみるXMLとXMLSchema
---
# 1.XMLSchemaの作成
このホームページでも使っている。
Drk7jpさんの長崎の天気予報XML、http://www.drk7.jp/weather/xml/42.xmlを
データバインディングで利用してみます。

天気予報XMLのXMLSchemaがあるのかと思ったのですが、なかったので自分で作ってみます。

# 2.天気予報XMLのXMLSchema
そして作ったXMLSchemaが次のものになります。

weatherforecast.xsd

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="weatherforecast">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="title" type="xs:string" minOccurs="1"
					maxOccurs="1" />
				<xs:element name="link" type="xs:string" minOccurs="1"
					maxOccurs="1" />
				<xs:element name="description" type="xs:string"
					minOccurs="1" maxOccurs="1" />
				<xs:element name="pubDate" type="xs:string" minOccurs="1"
					maxOccurs="1" />
				<xs:element name="author" type="xs:string" minOccurs="1"
					maxOccurs="1" />
				<xs:element name="managingEditor" type="xs:string"
					minOccurs="1" maxOccurs="1" />
				<xs:element name="pref" type="prefType" minOccurs="1"
					maxOccurs="1" />
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:complexType name="prefType">
		<xs:sequence>
			<xs:element name="area" type="areaType" maxOccurs="unbounded" />
		</xs:sequence>
		<xs:attribute name="id" type="xs:string" use="required" />
	</xs:complexType>
	<xs:complexType name="areaType">
		<xs:sequence>
			<xs:element name="geo" type="geoType" />
			<xs:element name="info" type="infoType" maxOccurs="unbounded" />
		</xs:sequence>
		<xs:attribute name="id" type="xs:string" use="required" />
	</xs:complexType>
	<xs:complexType name="geoType">
		<xs:sequence>
			<xs:element name="long" type="longType" />
			<xs:element name="lat" type="latType" />
		</xs:sequence>
	</xs:complexType>
	<xs:simpleType name="longType">
		<xs:restriction base="xs:decimal">
			<xs:totalDigits value="7" />
			<xs:fractionDigits value="4" />
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="latType">
		<xs:restriction base="xs:decimal">
			<xs:totalDigits value="6" />
			<xs:fractionDigits value="4" />
		</xs:restriction>
	</xs:simpleType>
	<xs:complexType name="infoType">
		<xs:sequence>
			<xs:element name="weather" type="xs:string" nillable="true" />
			<xs:element name="img" type="xs:string" />
			<xs:element name="weather_detail" type="xs:string" />
			<xs:element name="wave" type="xs:string" />
			<xs:element name="temperature" type="temperatureType" />
			<xs:element name="rainfallchance" type="rainfallchanceType" />
		</xs:sequence>
		<xs:attribute name="date" type="dateType" use="required" />
	</xs:complexType>
	<xs:simpleType name="dateType">
		<xs:restriction base="xs:string">
			<xs:pattern value="\d{4}/\d{2}/\d{2}" />
		</xs:restriction>
	</xs:simpleType>
	<xs:complexType name="temperatureType">
		<xs:sequence>
			<xs:element name="range" type="rangeType" maxOccurs="2"
				nillable="true" />
		</xs:sequence>
		<xs:attribute name="unit" type="xs:string" use="required" />
	</xs:complexType>
	<xs:complexType name="rangeType">
		<xs:simpleContent>
			<xs:extension base="xs:string">
				<xs:attribute name="centigrade" type="xs:string" use="required" />
			</xs:extension>
		</xs:simpleContent>
	</xs:complexType>
	<xs:complexType name="rainfallchanceType">
		<xs:sequence>
			<xs:element name="period" type="periodType" maxOccurs="4" />
		</xs:sequence>
		<xs:attribute name="unit" type="xs:string" use="required" />
	</xs:complexType>
	<xs:complexType name="periodType">
		<xs:simpleContent>
			<xs:extension base="xs:string">
				<xs:attribute name="hour" type="xs:string" use="required" />
			</xs:extension>
		</xs:simpleContent>
	</xs:complexType>
</xs:schema>
```

XMLも空要素があったのでnil属性を追加します。

weatherforecast.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<weatherforecast xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="weatherforecast.xsd">
	<title>weather forecast xml</title>
	<link>http://www.drk7.jp/weather/xml/42.xml</link>
	<description>気象庁の天気予報情報を XML で配信。1日1回 AM 6:00
		ごろ更新。</description>
	<pubDate>Sat, 19 Dec 2009 18:00:03 +0900</pubDate>
	<author>気象庁</author>
	<managingEditor>drk7.jp</managingEditor>
	<pref id="長崎県">
		<area id="五島">
			<geo>
				<long>128.8166</long>
				<lat>32.6909</lat>
			</geo>
			<info date="2009/12/19">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/200.gif</img>
				<weather_detail>北西の風海上では北西の風強くくもり</weather_detail>
				<wave>波3メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max" xsi:nil="true"></range>
					<range centigrade="min" xsi:nil="true"></range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">--</period>
					<period hour="06-12">--</period>
					<period hour="12-18">--</period>
					<period hour="18-24">40</period>
				</rainfallchance>
			</info>
			<info date="2009/12/20">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/201.gif</img>
				<weather_detail>北西の風やや強くくもり時々晴れ</weather_detail>
				<wave>波3メートルのち2メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max">8</range>
					<range centigrade="min">4</range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">50</period>
					<period hour="06-12">50</period>
					<period hour="12-18">50</period>
					<period hour="18-24">30</period>
				</rainfallchance>
			</info>
		</area>
		<area id="北部">
			<geo>
				<long>129.7724</long>
				<lat>33.2072</lat>
			</geo>
			<info date="2009/12/19">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/200.gif</img>
				<weather_detail>北西の風海上では北西の風やや強くくもり</weather_detail>
				<wave>波3メートルのち2.5メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max" xsi:nil="true"></range>
					<range centigrade="min" xsi:nil="true"></range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">--</period>
					<period hour="06-12">--</period>
					<period hour="12-18">--</period>
					<period hour="18-24">30</period>
				</rainfallchance>
			</info>
			<info date="2009/12/20">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/202.gif</img>
				<weather_detail>北西の風やや強くくもり一時雨か雪</weather_detail>
				<wave>波2.5メートルのち2メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max">7</range>
					<range centigrade="min">3</range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">50</period>
					<period hour="06-12">60</period>
					<period hour="12-18">50</period>
					<period hour="18-24">30</period>
				</rainfallchance>
			</info>
		</area>
		<area id="南部">
			<geo>
				<long>129.8878</long>
				<lat>32.7510</lat>
			</geo>
			<info date="2009/12/19">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/200.gif</img>
				<weather_detail>北西の風海上では北西の風やや強くくもり</weather_detail>
				<wave>波2.5メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max" xsi:nil="true"></range>
					<range centigrade="min" xsi:nil="true"></range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">--</period>
					<period hour="06-12">--</period>
					<period hour="12-18">--</period>
					<period hour="18-24">30</period>
				</rainfallchance>
			</info>
			<info date="2009/12/20">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/202.gif</img>
				<weather_detail>北西の風やや強くくもり一時雨か雪</weather_detail>
				<wave>波2.5メートルのち2メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max">7</range>
					<range centigrade="min">3</range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">60</period>
					<period hour="06-12">60</period>
					<period hour="12-18">50</period>
					<period hour="18-24">30</period>
				</rainfallchance>
			</info>
		</area>
		<area id="壱岐・対馬">
			<geo>
				<long>129.2670</long>
				<lat>34.2216</lat>
			</geo>
			<info date="2009/12/19">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/700.gif</img>
				<weather_detail>北西の風やや強く海上では北西の風強く晴れ</weather_detail>
				<wave>波3メートルのち2.5メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max" xsi:nil="true"></range>
					<range centigrade="min" xsi:nil="true"></range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">--</period>
					<period hour="06-12">--</period>
					<period hour="12-18">--</period>
					<period hour="18-24">10</period>
				</rainfallchance>
			</info>
			<info date="2009/12/20">
				<weather xsi:nil="true"></weather>
				<img>http://www.drk7.jp/MT/images/MTWeather/201.gif</img>
				<weather_detail>北西の風やや強くくもり時々晴れ</weather_detail>
				<wave>波3メートルのち2メートル</wave>
				<temperature unit="摂氏">
					<range centigrade="max">7</range>
					<range centigrade="min">2</range>
				</temperature>
				<rainfallchance unit="％">
					<period hour="00-06">20</period>
					<period hour="06-12">20</period>
					<period hour="12-18">20</period>
					<period hour="18-24">10</period>
				</rainfallchance>
			</info>
		</area>
	</pref>
</weatherforecast>
```


これは妥当性検証を通ります。
