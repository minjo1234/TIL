reference document  
>  https://guacamole.apache.org/doc/gug/guacamole-docker.html



### Guecamole docker 

| Container                      | Role                                     | 예시 이미지                       |
| ------------------------------ | ---------------------------------------- | ---------------------------- |
| 1️⃣ `guacd` (Guacamole Daemon) | SSH/RDP/VNC  Connection process daemon   | `guacamole/guacd`            |
| 2️⃣ `guacamole` (Webapp)       | HTML5 + REST API Server                  | `guacamole/guacamole`        |
| 3️⃣ `DB` (MySQL or PostgreSQL) | User account, Connection Info, Authority | `mysql:5.7` or `postgres:13` |
|                                |                                          |                              |



----

{"resourceType":"VM","hostName":"huhguyw6qa2","datastoreName":"gooddi-work01-domain-work01-cluster01-vsan01","networkName":"min_project 내부망 Subnet","cpu":2000.0,"memory":1024.0,"diskList":[{"uuid":"841fe507-7cb1-4309-8b16-f8e99e1cfa45","name":"huhguyw6qa2.huhguyw6.gooddi.lab-boot-disk","size":10240.0,"type":"HDD"},{"uuid":"5de1192c-ea35-40db-a1fd-4bcc505e9eec","name":"CD/DVD drive 1","size":0.0,"type":"CDROM"},{"uuid":"8ffd1aee-4a24-4f7b-982d-d41b053dde79","name":"Floppy drive 1","size":0.0,"type":"CDROM"}],"status":"POWER_ON","ip":"10.100.101.4","osName":"ubuntu","segmentUuids":["b2947929-f130-42cc-8ef6-86702e16bd71"],"firewallName":null,"networkProfileUuid":"cd6e9243-df8e-447b-8689-0691ac8acfed","installedSoftWares":[],"totalDiskSize":10240.0,"billingInfo":{"resourceType":"ARIA_VM","cpu":2000.0,"memory":1024.0,"disk":10240.0,"packages":[],"osType":"ubuntu"},"totalDisk":10240.0}


{"resourceType":"VM","hostName":"huhguyw6qa2","datastoreName":"gooddi-work01-domain-work01-cluster01-vsan01","networkName":"min_project 내부망 Subnet","cpu":2000.0,"memory":1024.0,"diskList":[{"uuid":"841fe507-7cb1-4309-8b16-f8e99e1cfa45","name":"huhguyw6qa2.huhguyw6.gooddi.lab-boot-disk","size":10240.0,"type":"HDD"},{"uuid":"5de1192c-ea35-40db-a1fd-4bcc505e9eec","name":"CD/DVD drive 1","size":0.0,"type":"CDROM"},{"uuid":"8ffd1aee-4a24-4f7b-982d-d41b053dde79","name":"Floppy drive 1","size":0.0,"type":"CDROM"}],"status":"POWER_ON","ip":"10.100.101.4","osName":"ubuntu","segmentUuids":["b2947929-f130-42cc-8ef6-86702e16bd71"],"firewallName":null,"networkProfileUuid":"cd6e9243-df8e-447b-8689-0691ac8acfed","installedSoftWares":[],"totalDiskSize":10240.0,"billingInfo":{"resourceType":"ARIA_VM","cpu":2000.0,"memory":1024.0,"disk":10240.0,"packages":[],"osType":"ubuntu"},"totalDisk":10240.0}