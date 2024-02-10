# Docker Swarm Cheat Sheet

**Initializing a Swarm**\
Initialize Swarm\
`docker swarm init`

Initialize Swarm with specific address\
`docker swarm init --advertise-addr <MANAGER-IP>`

Generate tocken for node join as manager.\
`docker swarm join-token manager`

Generate tocken for node join as worker.\
`docker swarm join-token worker`

Forcely advertise a cluster.
`docker swarm init --force-new-cluster --advertise-addr <MANAGER-IP>`

**Joining Nodes to Swarm**\
Join as a worker
`docker swarm join --token <TOKEN> <MANAGER-IP>:<PORT>`

**Managing Nodes**\
List Nodes\
`docker node ls`

Inspect Node\
`docker node inspect <NODE-ID>`

Promote Node to Manager, this CMD from master node\
`docker node promote <NODE-ID>`

Demote Manager to Worker\
`docker node demote <NODE-ID>`

Remove Node from Swarm\
`docker node rm <NODE-ID>`

Node itself Leave from cluster.\
`docker swarm leave`

