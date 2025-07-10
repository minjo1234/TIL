**full name :** Nexus Repository Manager 

**function** : 
- Maven, npm, PyPI, NuGet  package store 
- Docker registry  ( Docker image storage )
- Proxy Role 


**why use nexus :** 
- install is very simple 
- volume has a data maintenance function 


### 1.docker run 

```bash
docker run -d \
  -p 8081:8081 \
  --name nexus \
  sonatype/nexus3
```


### 1.docker - volumn
```docker 
```
