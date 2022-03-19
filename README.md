# docker-cheatsheet
### I want to answer Exercise No.5 in my DevOps class. 

## Task 1:
We pull image of mysql:8 and then specify docker version , ports and volumes by which the image is built.
## Answer:
``` bash

 docker pull mysql:8
 
 docker image inspect mysql:8
 
```
for example we use the output json and specify mentioned items:
```json
"DockerVersion": "20.10.7"

"ExposedPorts": {
            "3306/tcp": { },
            "33060/tcp": { }
                }
                                                        
   "Volumes": {
            "/var/lib/mysql": { }
              }
```

## Task 2:
we pull nginx:latest image and save it to a local tar file. then we load the file using load and import commands. in the second section we specify difference between load and import commands:
```bash
docker pull nginx:latest  

docker image save nginx my_nginx.tar

docker image import my_nginx.tar my_nginx:latest

docker image inspect my_nginx:latest 
   
```
the Layers key of output will be like this :
```json
"Layers": [
          "sha256:c1211ae5268ac54d86a5e4c05aa1816e81294f8a3c194d6642c01a8194a5ba0d"
          ]
```
and then we run this codes:
```bash
   docker image load -i my_nginx.tar 
   
   docker image inspect nginx:latest 

```
the Layers key of output will be like this :

```json
"Layers": [
  "sha256:7d0ebbe3f5d26c1b5ec4d5dbb6fe3205d7061f9735080b0162d550530328abd6",
  "sha256:9a3a6af98e18f06f2a233aa2b2374a5d83d3812e2784b0ab8db949f34cd1a7d6",
  "sha256:9a94c4a55fe4c8a5cfea7fbac1dde94c38973dbdab17a6314f0c8b35b68aba95",
  "sha256:6173b6fa63db8be9be756acf32a7beea0e8115f4e932d7de50b6071e7c55ee50",
  "sha256:235e04e3592ae74b04d0f29af65312be4c50c259b23b74698e35d42b2a4430ab",
  "sha256:762b147902c09d1860cccdaf4c5b28f5dea3760cb35c213c60ba2315950cbdaa"
]
```
we can see difference between load and import commands is in layers key of output, in fact import command merges all the layers.

## Task 3:
We Run a nginx container and bind it to port 8081 of the host.
```bash
docker run -d --name nginx -p 8081:80 nginx
```
 ## Task 4:
 Find the number of running processes of the container run in the previous section:
 
 ```bash
  docker top nginx
 ```

 ## Task 5:
 what is the use of docker-proxy ?
 The docker-proxy operates in userland, and simply receives any packets arriving at the host's specified port, 
 that the kernel hasn't 'dropped' or forwarded, and redirects them to the container's port.
 
 ## Task 6:
 Dangling images are layers that have no relationship to any tagged images and have <none> as their tag. 
 We can remove Dangling images by this command:
 ```bash
 docker image prune
 ```


[@dwsclass](https://github.com/dwsclass)dws-ops-005-docker
[@dwsclass](https://github.com/dwsclass)dws-ops-006-docker
