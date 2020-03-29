# elasticsearch-kibana

以下のコマンドでelasticsearchとkibanaが立ち上がる
```
docker-compose up -d
```

立ち上がったら 、、 

## elastic search へのアクセス
http://localhost:9200/   

## kibana へのアクセス
http://localhost:5601/

## 参考URL

https://medium.com/eureka-engineering/%E5%9F%BA%E7%A4%8E%E7%B7%A8-elasticsearch%E3%81%AE%E6%A4%9C%E7%B4%A2%E3%82%AF%E3%82%A8%E3%83%AA%E3%82%92%E4%BD%BF%E3%81%84%E3%81%93%E3%81%AA%E3%81%9D%E3%81%86-ace3e18c2174

https://dev.classmethod.jp/articles/elasticsearch-getting-started-07/

## コマンドメモ

リソース作成・変更
```
curl -XPUT "http://localhost:9200/customer/external/1" \
-H "Content-Type: application/json" \
-d '{
  "query": {
    "terms": {
      "name": "taro", "cook_time_min": [10, 15, 20]
    }
  }
}'
```

```
# リソース作成にあたってURLのID指定がない場合は自動でIDが割り当てられる
curl -XPOST "http://localhost:9200/customer/external" \
-H "Content-Type: application/json" \
-d '{
  "query": {
    "terms": {
      "name": "taro3", "cook_time_min": [10, 15, 20]
    }
  }
}'
```

```
curl -XPOST "http://localhost:9200/test/recipes/2" \
-H "Content-Type: application/json" \
-d @./data/basil-and-pesto-hummus.json
```

リソース削除

```
curl -XDELETE "http://localhost:9200/customer/external/2"
```

検索

```

```

## バッチプロセッシング

```
curl -XPOST "http://localhost:9200/customer/external/_bulk" \
-H "Content-Type: application/json" \
-d '
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe2" }
{"index":{"_id":"3"}}
{"name": "Jane Doe3" }
'
```

```
curl -XPOST "http://localhost:9200/customer/external/_bulk" \
-H "Content-Type: application/json" \
-d '
{"update":{"_id":"1"}}
{"doc": {"name": "John Doe becomes Jane Doe"}}
{"delete":{"_id":"2"}}
'
```