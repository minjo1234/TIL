- ElasticCache is to get managed Redis or Memcached 
- Caches are in-memory databases with really high performance, low latency 
- Helps reduce load off of databases for read intensive workloads 
- Using ElasticCache involves heavy application code changes 
- Cache must have an invalidation strategy to make sure only the most current data 
  is used in there 

Catch hit  -> elastic cache 
Catch miss  -> rds 