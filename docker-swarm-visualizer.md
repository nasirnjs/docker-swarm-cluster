# Docker Swarm Visualizer

Docker Swarm Visualizer is a tool that provides a visual representation of your Docker Swarm cluster. It shows you the status of your services, containers, and nodes in the cluster in a graphical interface. This visualization can be helpful for understanding the layout of your swarm, identifying any issues, and monitoring the health of your containers and services.

```bash
docker service create \
  --name=viz \
  --publish=8080:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
 dockersamples/visualizer
```
Check Docker Swarm Visualizer service.\
`docker service ls`

Now browse your Swarm manager IP with Port.\
`http://172.17.18.220:8080`

To create an Nginx service in a Docker Swarm.\
```
docker service create \
  --name nginx-service \
  --publish published=80,target=80 \
  --replicas 3 \
  nginx:latest
```

To create a Docker Swarm service using a YAML file.
`vim nginx-svc.yaml`
```bash
version: '3.8'

services:
  nginx:
    image: nginx:latest
    deploy:
      replicas: 2
    ports:
      - "80:80"
```
` docker stack deploy -c nginx-svc.yaml nginx-stack`

`docker service ls`

