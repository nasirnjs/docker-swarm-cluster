# Docker Swarm Cheat Sheet

**Initializing a Swarm**\
Initialize Swarm\
`docker swarm init`

Initialize Swarm with specific address\
`docker swarm init --advertise-addr <MANAGER-IP>`

**Joining Nodes to Swarm**\
Join as a worker
`docker swarm join --token <TOKEN> <MANAGER-IP>:<PORT>`

**Managing Nodes**
List Nodes\
`docker node ls`\
Inspect Node\
`docker node inspect <NODE-ID>`\
Promote Node to Manager\
`docker node promote <NODE-ID>`\
Demote Manager to Worker\
`docker node demote <NODE-ID>`\
Remove Node from Swarm\
`docker node rm <NODE-ID>`
