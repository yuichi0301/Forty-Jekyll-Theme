---
layout: post
title: XQueryの勉強・複数のソートキーを指定したソート
description: XQueryの勉強・複数のソートキーを指定したソート
---
1.今回は複数のソートキーを指定した場合のソートを試してみます。
まずは今のデータでは複数のキーに指定してはっきりわかる項目がないので、
次のXMLに更新します。
number要素の003を3つにして、number要素とdate要素でソートしてみます。

コマンドは以下のコマンドになります。

```xquery
update othello.othello_management
set othello = '<othelloList>
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
<date>2009-03-02</date>
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
<number>003</number>
<date>2009-03-01</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>49</black_count>
<white_player>takesi</white_player>
<white_count>15</white_count>
<win>black</win>
</othello>
<othello>
<number>003</number>
<date>2009-03-03</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>49</black_count>
<white_player>takesi</white_player>
<white_count>15</white_count>
<win>black</win>
</othello>
</othelloList>'
where
id = '001'
```

2.複数のソートキーを指定してソートしてみる。
```xquery
<results>
{
for $result in
db2-fn:xmlcolumn("OTHELLO.OTHELLO_MANAGEMENT.OTHELLO")/othelloList/othello
order by $result/number,xs:date($result/date)
return $result
}
</results>
```


XMLはXMLスキーまで定義しているわけではないので、date関数を使ってdate型にして
ソートします。
ちゃんとnumberでソートされたあと、date要素でソートされた結果が出力されました。
