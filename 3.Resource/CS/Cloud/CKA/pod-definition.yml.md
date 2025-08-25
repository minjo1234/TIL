
unit : app > pod > container 

```yml

apiVersion: v1
kind: Pod
metadata:
	name: myapp-pod 
	labels:
		app: myapp
		type: front-end
spec:
	containers:
		- name: nginx-container 
		- image: nginx 
```


`kubectl get pods`

`kubectl describe pod myapp-pod`

