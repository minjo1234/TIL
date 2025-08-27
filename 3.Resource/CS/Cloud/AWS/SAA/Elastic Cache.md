- ElasticCache is to get managed Redis or Memcached 
- Caches are in-memory databases with really high performance, low latency 
- Helps reduce load off of databases for read intensive workloads 
- Using ElasticCache involves heavy application code changes 
- Cache must have an invalidation strategy to make sure only the most current data 
  is used in there 

Catch hit  -> elastic cache 
Catch miss  -> rds 


**Elastic Cache Solution Architecture - User Session Store**

Write Session -> Amazon Elastic Cache 
Retrieve Session <- Amazon Elastic Cache 


Elastic Cache - Redis Vs Memcached 

Redis - Replication 
Memcached - sharding 


**ElasticCache - Cache Security** 

- ElasticCache supports IAM Authentication for Redis 
- IAM policies on ElasticCache are only used for AWS API-level security 
- **Redis Auth**
	- SSL in flight encryption
- Memcached 
	- Support SASL-based 

Patterns for ElasticCache 

 - Lazy loading 
 - Write Through 
 - Session Store 