---
title: Sync Elasticsearch index to another Elasticsearch using logstash
description: logstash script to sync data between two elasticsearch indexes
tags: logstash, elasticsearch, index
created: 2018-08-28
---

```javascript
input {
  elasticsearch {
    hosts => [ "http://source_host:9200" ]
    index => "physicians"
    size => 1000
    scroll => "5m"
    docinfo => true
  }
}

output {
  elasticsearch {
    hosts => [ "http://destination_host:9200" ]
    index => "%{[@metadata][_index]}"
    document_type => "%{[@metadata][_type]}"
    document_id => "%{[@metadata][_id]}"
  }
  stdout {
    codec => "dots"
  }
}
```

```sh
logstash -f logstash-es-sync.conf
```