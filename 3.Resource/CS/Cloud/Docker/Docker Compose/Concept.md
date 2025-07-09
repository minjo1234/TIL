
## Advantage 

### 1.Multi Container Management 

- complicated service(example: web server + db + cash) defines one file (docker-compose.yml)
- multi container run and stop using docker compose up 

### 2. Environment Consistency 

- develop/test/production reuse 
- all of the team member can develop same environment 

### 3.Easy Setting Management 

- Network, Volume, Dependency declare `yml` file -> not use `docker run`
- ray all of the contents that affected by application 

### 4.Dependency Minimize 

 - DB, Redis, Mq external system easy append to `compose`

### 5.Scaling Apply 

- `docker compose up --scale` option makes the several instance of the same service 

