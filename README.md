Elasticsearch
=============

- [Elasticsearchチュートリアル - 不可視点 id:code46](http://code46.hatenablog.com/entry/2014/01/21/115620)

- [ld-gourmet-datasets](https://github.com/livedoor/datasets)

## Install

```bash
$ brew install elasticsearch

$ elasticsearch --version
Version: 2.4.0, Build: ce9f0c7/2016-08-29T09:14:17Z, JVM: 1.8.0_25

$ brew install logstash

$ logstash --version
logstash 2.4.0

$ logstash-plugin list | grep csv
logstash-filter-csv
logstash-output-csv

$ brew install kibana

$ kibana --version
4.5.1
```

## Start Elasticsearch

```bash
# start elasticsearch
$ elasticsearch
```

## Start Kibana (option)

```bash
# start kibana
$ kibana
```

## Create/Delete index

```bash
# create index with mapping
$ curl -XPOST localhost:9200/ldgourmet -d @./conf/elasticsearch/mapping.json

# delete index
$ curl -XDELETE localhost:9200/ldgourmet
```

## Register data to index by logstash

```bash
$ cat datastore/csv/ldgourmet/restaurants100.csv | logstash -f conf/logstash/restaurant.conf
Settings: Default pipeline workers: 4
Pipeline main started
Pipeline main has been shutdown
stopping pipeline {:id=>"main"}

```

## Search request

```bash
$ curl -XGET localhost:9200/ldgourmet/_search?pretty=true -d '
{
  "query" : {
    "simple_query_string" : {
      "query": "武蔵野文庫",
      "fields": ["_all"],
      "default_operator": "and"
    }
  }
}
'
```


## Result of search

```json
{
  "took" : 110,
  "timed_out" : false,
  "_shards" : {
    "total" : 5,
    "successful" : 5,
    "failed" : 0
  },
  "hits" : {
    "total" : 2,
    "max_score" : 0.7342101,
    "hits" : [ {
      "_index" : "ldgourmet",
      "_type" : "logs",
      "_id" : "AVc31CMGkaSQR-wfQ41E",
      "_score" : 0.7342101,
      "_source" : {
        "message" : "73,\"茶房 武蔵野文庫\",,,\"さぼうむさしのぶんこ\",13,16,1978,6,488,1605,17,1378,3072,23,1871,602,408,0,0,0,180-0004,\"武蔵野市吉祥寺本町2-13-4\",35.42.06.937,139.34.48.598,\"東急の裏。    電話番号を変更しました。   (from 東京グルメ 2005/11/15)\",\"1,2,4\",0,1,0,3,0,1,2,5381,\"2000-09-10 11:22:02\",\"2011-04-22 01:20:04\",0",
        "@version" : "1",
        "@timestamp" : "2016-09-17T11:07:11.541Z",
        "host" : "BHMBP.local",
        "id" : "73",
        "name" : "茶房 武蔵野文庫",
        "property" : null,
        "alphabet" : null,
        "name_kana" : "さぼうむさしのぶんこ",
        "pref_id" : "13",
        "area_id" : "16",
        "station_id1" : "1978",
        "station_time1" : "6",
        "station_distance1" : "488",
        "station_id2" : "1605",
        "station_time2" : "17",
        "station_distance2" : "1378",
        "station_id3" : "3072",
        "station_time3" : "23",
        "station_distance3" : "1871",
        "category_id1" : "602",
        "category_id2" : "408",
        "category_id3" : "0",
        "category_id4" : "0",
        "category_id5" : "0",
        "zip" : "180-0004",
        "address" : "武蔵野市吉祥寺本町2-13-4",
        "north_latitude" : "35.42.06.937",
        "east_longitude" : "139.34.48.598",
        "description" : "東急の裏。    電話番号を変更しました。   (from 東京グルメ 2005/11/15)",
        "purpose" : "1,2,4",
        "open_morning" : "0",
        "open_lunch" : "1",
        "open_late" : "0",
        "photo_count" : "3",
        "special_count" : "0",
        "menu_count" : "1",
        "fan_count" : "2",
        "access_count" : "5381",
        "created_on" : "2000-09-10 11:22:02",
        "modified_on" : "2011-04-22 01:20:04",
        "closed" : "0"
      }
    }, {
      "_index" : "ldgourmet",
      "_type" : "logs",
      "_id" : "AVc30xqmkaSQR-wfQ4zh",
      "_score" : 0.69349575,
      "_source" : {
        "message" : "73,\"茶房 武蔵野文庫\",,,\"さぼうむさしのぶんこ\",13,16,1978,6,488,1605,17,1378,3072,23,1871,602,408,0,0,0,180-0004,\"武蔵野市吉祥寺本町2-13-4\",35.42.06.937,139.34.48.598,\"東急の裏。    電話番号を変更しました。   (from 東京グルメ 2005/11/15)\",\"1,2,4\",0,1,0,3,0,1,2,5381,\"2000-09-10 11:22:02\",\"2011-04-22 01:20:04\",0",
        "@version" : "1",
        "@timestamp" : "2016-09-17T11:06:03.821Z",
        "host" : "BHMBP.local",
        "id" : "73",
        "name" : "茶房 武蔵野文庫",
        "property" : null,
        "alphabet" : null,
        "name_kana" : "さぼうむさしのぶんこ",
        "pref_id" : "13",
        "area_id" : "16",
        "station_id1" : "1978",
        "station_time1" : "6",
        "station_distance1" : "488",
        "station_id2" : "1605",
        "station_time2" : "17",
        "station_distance2" : "1378",
        "station_id3" : "3072",
        "station_time3" : "23",
        "station_distance3" : "1871",
        "category_id1" : "602",
        "category_id2" : "408",
        "category_id3" : "0",
        "category_id4" : "0",
        "category_id5" : "0",
        "zip" : "180-0004",
        "address" : "武蔵野市吉祥寺本町2-13-4",
        "north_latitude" : "35.42.06.937",
        "east_longitude" : "139.34.48.598",
        "description" : "東急の裏。    電話番号を変更しました。   (from 東京グルメ 2005/11/15)",
        "purpose" : "1,2,4",
        "open_morning" : "0",
        "open_lunch" : "1",
        "open_late" : "0",
        "photo_count" : "3",
        "special_count" : "0",
        "menu_count" : "1",
        "fan_count" : "2",
        "access_count" : "5381",
        "created_on" : "2000-09-10 11:22:02",
        "modified_on" : "2011-04-22 01:20:04",
        "closed" : "0"
      }
    } ]
  }
}
```

