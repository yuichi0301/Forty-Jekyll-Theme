---
layout: post
title: XQueryの勉強・order by節
description: XQueryの勉強・order by節
---
1.データの登録の準備 今回はソートを試してみます。
ソートを試すにはデータがいるので次のXMLを追加して登録します。

```xml
<othelloList>
	<othello>
		<number>001</number>
		<date>2009-03-07</date>
		<place>長崎</place>
		<black_player>yuichi</black_player>
		<black_count>36</black_count>
		<white_player>takesi</white_player>
		<white_count>28</white_count>
		<win>black</win>
	</othello>
	<othello>
		<number>003</number>
		<date>2009-03-01</date>
		<place>長崎</place>
		<black_player>yuichi</black_player>
		<black_count>64</black_count>
		<white_player>takesi</white_player>
		<white_count>0</white_count>
		<win>black</win>
	</othello>
	<othello>
		<number>002</number>
		<date>2010-04-07</date>
		<place>長崎</place>
		<black_player>yuichi</black_player>
		<black_count>28</black_count>
		<white_player>takesi</white_player>
		<white_count>36</white_count>
		<win>white</win>
	</othello>
	<othello>
		<number>005</number>
		<date>2009-06-07</date>
		<place>長崎</place>
		<black_player>yuichi</black_player>
		<black_count>54</black_count>
		<white_player>takesi</white_player>
		<white_count>10</white_count>
		<win>black</win>
	</othello>
	<othello>
		<number>006</number>
		<date>2009-10-07</date>
		<place>長崎</place>
		<black_player>yuichi</black_player>
		<black_count>49</black_count>
		<white_player>takesi</white_player>
		<white_count>15</white_count>
		<win>black</win>
	</othello>
</othelloList>
```

2.コマンドの実行 登録コマンドの実行はコントロールセンターのコマンドエディターからやります。

```xquery
insert into othello.othello_management values ('001', '
<othelloList>
<othello>
<number>001</number>
<date>2009-03-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
<white_count>28</white_count>
<win>black</win>
</othello>
<othello>
<number>003</number>
<date>2009-03-01</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>64</black_count>
<white_player>takesi</white_player>
<white_count>0</white_count>
<win>black</win>
</othello>
<othello>
<number>002</number>
<date>2010-04-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>28</black_count>
<white_player>takesi</white_player>
<white_count>36</white_count>
<win>white</win>
</othello>
<othello>
<number>005</number>
<date>2009-06-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>54</black_count>
<white_player>takesi</white_player>
<white_count>10</white_count>
<win>black</win>
</othello>
<othello>
<number>006</number>
<date>2009-10-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>49</black_count>
<white_player>takesi</white_player>
<white_count>15</white_count>
<win>black</win>
</othello>
</othelloList>
');
```

![image]({{site.baseurl}}/assets/images/2009_10_3/insert1.jpg)


3.ソート条件の入った検索の実行
number要素をソート条件にしてみたいと思います。
①その前に普通の検索を実行してみます。
コマンドは以下のコマンドになります。(実行結果が整形式にならないためコンストラクタの中に入れて整形式にしています。)

```xquery
{
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othelloList/othello
return $result
}
```




見事number要素はソートされずに出てきました。
②number要素をソート条件に指定して実行してみます。
コマンドは以下のコマンドになります。


```xquery
<results>
{
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othelloList/othello
order by $result/number
return $result
}
</results>
```



number要素によってソートされました。 ③降順でソートしてみる。 コマンドは以下のコマンドになります。
ソート条件の後ろにdescendingをつけるだけです。


```xquery
<results>
{
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othelloList/othello
order by $result/number descending
return $result
}
</results>
```
