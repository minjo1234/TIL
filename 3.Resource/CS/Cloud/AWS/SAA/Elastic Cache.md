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

**Patterns for ElasticCache** 

 - Lazy loading : when the cache does not exists, application read from db 
 - Write Through 
 - Session Store 


**Redis Use Case** 

- Gaming Leaderboards are computationally complex 
- Redis Sorted sets guarantee both uniqueness and element ordering 
- Each time a new element added, it's ranked in real time, then added in correct order 

**중요한 포트:**

- FTP: 21
- SSH: 22
- SFTP: 22 (SSH와 같음)
- HTTP: 80
- HTTPS: 443

**vs RDS 데이터베이스 포트:**

- PostgreSQL: 5432
- MySQL: 3306
- Oracle RDS: 1521
- MSSQL Server: 1433
- MariaDB: 3306 (MySQL과 같음)
- Aurora: 5432 (PostgreSQL와 호환될 경우) 또는 3306 (MySQL과 호환될 경우)


---

1.because read replicas replicate async, user don't read recent data, read past data 
2.multi AZ don't has to changed multiple string 
3.AWS region level vs AZ level 

---

The company use RDS MySQL 5.6 that plan to process analyzing workload 
What's the most cost effective solution ? 

- Create a Read only Replicas other AZ, execute analyzing workload from database replicas 

---

A power outage occurs specific region, I plan to disaster recovery strategy that read and write other aws region

- How to ? : make a read only replicas other region, that activate multi-az