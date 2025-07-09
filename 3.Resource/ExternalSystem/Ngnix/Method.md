
```bash
docker network create <network-name>

docker network create clovirone_network 
```


### Nginx 

```
docker run -d \
  --name nginx-proxy \
  --network clovirone_network \
  -p 80:80 \
  -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro \
  -v /root/nginx/log:/var/log/nginx \
  nginx:alpine
  
```


```
docker run -d   --name nginx-proxy   --network clovirone_network   -p 80:80   -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro   -v /root/nginx/log:/var/log/nginx   nginx:alpine
```



### TEst 

```
 docker run -d   --name test   --network clovirone_network   -p 8090:8080   one_integration_test:latest
```

### Guacamole 

```
docker run -d   --name guacamole   --network clovirone_network   -p 8080:8080   guacamole/guacamole
```


Internal": false


docker run -d \ --name guacamole \ --network clovirone_network \ -e GUACD_HOSTNAME=guacd \ -p 8080:8080 \ -v /root/guac/user-mapping.xml:/etc/guacamole/user-mapping.xml \ guacamole/guacamole