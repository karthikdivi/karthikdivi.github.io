---
title: Redis
description: 
created: 2018-09-22
---

## Hash

```sh
HSET colors white fffff
HSET colors black 000000
HGET colors white
HDEL colors white
```

## Ship
Push docker image
```sh
docker push user_id/my_image
```
## List

```sh
LPUSH jobs job1
LPUSH jobs job2
RPUSH jobs job3
RPOP jobs
LPOP jobs
```

## Set

```sh
SADD colors white
SADD colors black
SADD colors black
SMEMBERS myset
```

## SortedSets

```
Takes score and sort by that
```

## String

```sh
SET masterServer host1 EX 60 NX
```

## MISC

```sh
FLUSHALL
FLUSHDB
```

## Use Cases

* Cache
* Distributed Locking
* Pub/Sub
* Async communication
* Batch processing (Jobs in queues)
* session
* Redis + Elasticsearch