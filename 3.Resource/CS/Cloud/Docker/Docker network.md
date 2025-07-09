
### 1.Example 

```bash

6096dd036a6f   nginx:alpine                  "/docker-entrypoint.…"   20 hours ago   Up 20 hours             0.0.0.0:80->80/tcp, :::80->80/tcp             nginx-proxy
93fc6d5b07ff   guacamole/guacamole           "/opt/guacamole/bin/…"   21 hours ago   Up 21 hours             0.0.0.0:8080->8080/tcp, :::8080->8080/tcp     guacamole
bc1c587f029d   guacamole/guacd               "/opt/guacamole/entr…"   22 hours ago   Up 22 hours (healthy)   4822/tcp                                      guacd
212bc9317e3c   one_integration_test:latest   "/opt/tomcat/bin/cat…"   3 weeks ago    Up 3 weeks              0.0.0.0:8090->8080/tcp, [::]:8090->8080/tcp   test
f0213b23a912   clovirone_portal              "/opt/tomcat/bin/cat…"   7 weeks ago    Up 7 weeks              0.0.0.0:8083->8080/tcp, [::]:8083->8080/tcp   clovirone2.0_test
1120185b31d0   clovirone_portal              "/opt/tomcat/bin/cat…"   7 weeks ago    Up 11 days              0.0.0.0:8086->8080/tcp, [::]:8086->8080/tcp   clovirone2.0
334af27df33a   clovirone_db:latest           "docker-entrypoint.s…"   8 months ago   Up 8 weeks              0.0.0.0:3306->3306/tcp, :::3306->3306/tcp     clovirone_db


```