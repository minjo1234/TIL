
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
