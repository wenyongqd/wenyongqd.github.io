---
title: 'What is cache penetration, cache breakdown and cache avalanche?'
date: 2020-07-30 19:57:23
tags:
---

>When designing and developing highly available system, cache is an very important consideration. It is useful to cache some frequently accessed data so that they can be accessed quickly and also cache can protect the downstream system like DB from being hit too often. 

To provide better cache design in large systems, some problems may need to be considered first. In this post, we will talk about some frequently discussed cache problems and mitigation plans.

### Cache penetration
Cache penetration is a scenario where the data to be searched doesn't exist at DB and the returned empty result set is not cached as well and hence every search for the key will hit the DB eventually. If a hacker tries to initiate some attack by launching lots of searches with such key, the underlying DB layer will be hit too often and may eventually be brought down.

In such cases, there are a few mitigation plans.

1. If there is no data for the key in DB, just return an empty result and cache it for a short period of time(Don't set a long expiration time)
2. Using Bloom filter. Bloom filter is similar to hbase set which can be used to check whether a key exists in the data set. If the key exists, go to the cache layer or DB layer, if it doesn't exists in the data set, then just return.

If the searched key has high repeat rate, then can adopt the first solution. Otherwise if the searched key has low repeat rate and the searched keys are too many, can adopt the second solution to filter most of them first.

### Cache breakdown
Cache breakdown is a scenario where the cached data expires and at the same time there are lots of search on the expired data which suddenly cause the searches to hit DB directly and increase the load to the DB layer dramatically.

This would happen in high concurrency environment. Normally in this case, there needs to be a lock on the searched key so that other threads need to wait when some thread is trying to search the key and update the cache. After the cache is updated and lock is released, other threads will be able to read the newly cached data.

Another feasible method is to asynchronously update the cached data through a worker thread so that the hot data will never expire.

### Cache avalanche
Cache avalanche is a scenario where lots of cached data expire at the same time or the cache service is down and all of a sudden all searches of these data will hit DB and cause high load to the DB layer and impact the performance.

To mitigate the problem, some methods can be adopted.

1. Using clusters to ensure that some cache server instance is in service at any point of time. If Redis is used, can have redis clusters.
2. Some other approaches like hystrix circuit breaker and rate limit can be configured so that the underlying system can still serve traffic and avoid high load
3. Can adjust the expiration time for different keys so that they will not expire at the same time.

All the mitigation methods need to be implemented based on real use cases and system design requirements.