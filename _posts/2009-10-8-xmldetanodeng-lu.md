---
layout: post
title: XQueryの勉強・XMLデータの登録
description: XQueryの勉強・XMLデータの登録
---
1.登録するXML
とりあえずなんでもいいんですがよくオセロをやっていたので、
オセロの対戦データのXMLを登録することにしてみます。
以下が登録するXMLです。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE othello SYSTEM "othello.dtd">
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
```

2.DTD
1.で作成したXMLのDTDは以下のようになります。

```dtd
<!ELEMENT othello
((number)+,(date)+,(place)+,(black_player)+,(black_count)+,(white_player)+,(white_count)+,(win)+)>
<!ELEMENT number (#PCDATA)>
<!ELEMENT date (#PCDATA)>
<!ELEMENT place (#PCDATA)>
<!ELEMENT black_player (#PCDATA)>
<!ELEMENT black_count (#PCDATA)>
<!ELEMENT white_player (#PCDATA)>
<!ELEMENT white_count (#PCDATA)>
<!ELEMENT win (#PCDATA)>
```



3.テーブルを作る
XMLを格納する用のテーブルを作成します。
カラムはXMLのIDとXMLです。
まずはコマンド行プロセッサーを起動します。
TEST_DBに接続します。
```sql
connect to TEST_DB
```
テーブルを作ります。

```sql
create table othello.othello_management (id char(3) NOT NULL,
othello
xml,primary key (id))
```




4.データを登録する。
その前にDB2で改行のあるコマンドを実行するにはDB2コマンドの段階でオプションを指定する必要があります。
まずはquitでいったん抜けます。

```sql
db2 -t -v
connect to TEST_DB;
insert into othello.othello_management values ('000', '
<othello>
<number>001</number>
<date>2009-03-07</date>
<place>長崎</place>
<black_player>yuichi</black_player>
<black_count>36</black_count>
<white_player>takesi</white_player>
<white_count>28</white_count>
<win>black</win>
</othello>');
```
