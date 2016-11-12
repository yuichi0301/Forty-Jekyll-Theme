---
layout: post
title: JAXBの勉強・アンマーシャリングする
description: JAXBの勉強・アンマーシャリングする
---
1.weatherforecast.xmlをアンマーシャリングする
weatherforecast.xmlをアンマーシャリングしてみます。
つまり、weatherforecast.xmlを読み込んでオブジェクト化します。

まずは前回作ったクラスを全てプロジェクトの中に入れます。
階層は以下のようになります。

![image]({{site.baseurl}}/assets/images/2009_10_3/2-1.jpg)

とりあえず、天気予報でも使っている長崎南部の降水確率が
どれくらい簡単に取得できるかやってみます。

そして実行クラスは以下のように書きました。


```java
package weather.jaxb;

import generated.AreaType;
import generated.InfoType;
import generated.PeriodType;
import generated.PrefType;
import generated.RainfallchanceType;
import generated.Weatherforecast;
import java.io.File;
import java.util.List;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Unmarshaller;

public class Execute {
	public static void main(String[] args) throws Exception {
		try {
			JAXBContext context = JAXBContext.newInstance("generated");
			Unmarshaller unm = context.createUnmarshaller();
			Weatherforecast weatherforecast = (Weatherforecast)unm.unmarshal(new File("C:\\test\\weatherforecast.xml"));
			PrefType pref = weatherforecast.getPref();
			AreaType area = getArea(pref);
			InfoType info = getInfo(area);
			RainfallchanceType rainfall = info.getRainfallchance();
			List<PeriodType> periodList = rainfall.getPeriod();
			for(PeriodType period:periodList){
				System.out.println(period.getHour() + ":" + period.getValue());
			}
		} catch (JAXBException e) {
			e.printStackTrace();
		}
	}

	/**
	 * Areaを取得
	 *
	 * @param pref
	 * @return
	 * @throws Exception
	 */
	private static AreaType getArea(PrefType pref) throws Exception {
		List<AreaType> areaList = pref.getArea();
		for(AreaType area:areaList){
			if(area.getId().equals("南部")){
				return area;
			}
		}
		throw new Exception();
	}

	/**
	 * 2009/12/19の情報を取得
	 *
	 * @param area
	 * @return
	 * @throws Exception
	 */
	private static InfoType getInfo(AreaType area) throws Exception {
		List<InfoType> ifnoList = area.getInfo();
		for(InfoType info:ifnoList){
			if(info.getDate().equals("2009/12/20")){
				return info;
			}
		}
		throw new Exception();
	}
}
```

実行結果は以下のようになります。

00-06:60
06-12:60
12-18:50
18-24:30


2．クラスの具体的な内容

①JAXBContext context = JAXBContext.newInstance("generated");
newInstanceに渡す引数はパッケージ名になります。

②Weatherforecast weatherforecast = (Weatherforecast)unm.unmarshal(new File("C:\\test\\weatherforecast.xml"));
C:\testにあるweatherforecast.xml XMLを読み込んでWeatherforecastオブジェクトを生成します。

③PrefType pref = weatherforecast.getPref();
weatherforecast要素の中にpref要素は1つしかないのでgetメソッドでそのまま取得できます。

④List<AreaType> areaList = pref.getArea();
pref要素の中にarea要素は複数あるので戻り値はListになります。

![image]({{site.baseurl}}/assets/images/2009_10_3/3-1.jpg)

⑤List<InfoType> ifnoList = area.getInfo();
area要素の中にinfo要素は複数あるので戻り値はListになります。

![image]({{site.baseurl}}/assets/images/2009_10_3/4-2.jpg)

⑥List<PeriodType> periodList = rainfall.getPeriod();
period要素も複数になりますので、あとはListを回して表示させれば終わりです。

![image]({{site.baseurl}}/assets/images/2009_10_3/5-1.jpg)

この方法で取得するとコードは結構長くなります。
しかし、XMLをオブジェクトとして扱えるのはJavaの開発者としてはかなりやりやすいと思います。
