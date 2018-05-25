# 엘라스틱서치 서치 쿼리 예제(Elasticserch Search Query Example)


## 다중 쿼리 예제

현재 시간으로부터 5분 전까지 발생한 데이터 중에 **container** term 이 **member** 인 데이터에 대하여 log 필드 목록만 offset 으로 정렬하여 조회한다.

### Bool


```bash
curl --request POST \
  --url http://localhost:9200/_search \
  --header 'Content-Type: application/json' \
  --data '{
    "query": {
    	"bool" : {
    		"must" : {
    			"range" : {
            		"@timestamp" : {
                		"gte" : "now-5m",
                		"lt" :  "now"
            		}
        		}
    		},
    		"should" : [
    			{"term": {"container": "member"} }
    			]
    	}
    },
    "_source" : ["log"],
    "sort": ["offset"]
}'
```
