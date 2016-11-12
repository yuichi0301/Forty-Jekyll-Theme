---
layout: post
title: JAXBの勉強・マーシャリングする
description: JAXBの勉強・マーシャリングする
---
# 1.はじめに
今回は前回作ったオブジェクトに値を入れて
逆にXMLを生成したいと思います。

生成するXMLの内容は単純にtitle要素にtestという文字列を入れただけのXMLです。

# 2.クラス

実際に書いたクラスは以下のものになります。

```java
package weather.marshal;

import generated.Weatherforecast;

import java.io.FileOutputStream;

import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;

public class Execute {
	public static void main(String[] args) throws Exception {
	    try {
	        JAXBContext context = JAXBContext.newInstance("generated");
	        Marshaller marshaller = context.createMarshaller();

	        Weatherforecast weatherforecast = new Weatherforecast();
	        weatherforecast.setTitle("test");

	        FileOutputStream stream = new FileOutputStream("C:\\test\\marshal_weatherforecast.xml");
	        marshaller.marshal(weatherforecast, stream);

	    } catch (JAXBException e) {
			e.printStackTrace();
	    }
	}
}
```


Cドライブのtestフォルダにmarshal_weatherforecast.xmlを出力させます。

# 3.出力結果

出力結果は以下のものになります。

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<weatherforecast>
	<title>test</title>
</weatherforecast>
```
